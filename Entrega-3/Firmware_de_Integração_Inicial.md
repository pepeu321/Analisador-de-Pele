# Integração dos sensores

```cpp

#include <msp430.h>

// === Variáveis globais ===
volatile unsigned int tempo_rc = 0;
volatile unsigned char flag_captura = 0;

// === Protótipos ===
void setupGPIO();
void setupTimerCapture();
void setupADC();
void setupUART();
unsigned int medirOleosidade();
void iniciarMedicaoHidratacao();
void uart_print(const char *str);
void uart_print_int(unsigned int num);
const char* classificarHidratacao(unsigned int tempo_us);
const char* classificarOleosidade(unsigned int tensao_mV);

void main(void) {
WDTCTL = WDTPW | WDTHOLD; // Para o Watchdog
BCSCTL1 = CALBC1_1MHZ; // Clock 1 MHz
DCOCTL = CALDCO_1MHZ;

setupGPIO();
setupUART();
setupTimerCapture();
setupADC();

__enable_interrupt();

while (1) {
// === Medição de hidratação ===
iniciarMedicaoHidratacao();
__delay_cycles(50000); // Espera descarga do capacitor
while (!flag_captura); // Espera captura
flag_captura = 0;

unsigned int tempo_us = tempo_rc;

// === Medição de oleosidade ===
unsigned int adc_value = medirOleosidade();
unsigned int tensao_mV = adc_value * 3300 / 1023; // mV

// === Classificações ===
const char* classificacaoH = classificarHidratacao(tempo_us);
const char* classificacaoO = classificarOleosidade(tensao_mV);

// === UART: Hidratacao ===
uart_print("\r\nHidratacao: ");
uart_print_int(tempo_us);
uart_print(" us (");
uart_print(classificacaoH);
uart_print(")\r\n");

// === UART: Oleosidade ===
uart_print("Oleosidade: ");
uart_print_int(tensao_mV / 1000);
uart_print(".");
uart_print_int((tensao_mV % 1000) / 10); // 2 casas decimais
uart_print(" V (");
uart_print(classificacaoO);
uart_print(")\r\n");

__delay_cycles(2000000); // Atraso ~2s
}
}

// === Configurações ===

void setupGPIO() {
P1DIR |= BIT0; // LED debug
P1OUT &= ~BIT0;

// UART TX (P1.1)
P1DIR |= BIT1;
P1SEL |= BIT1;
P1SEL2 |= BIT1;

// UART RX (P1.2)
P1DIR &= ~BIT2;
P1SEL |= BIT2;
P1SEL2 |= BIT2;

// Timer Capture entrada (P1.3)
P1DIR &= ~BIT3;
P1SEL |= BIT3;

// Controle do capacitor (P1.4)
P1DIR |= BIT4;
P1OUT &= ~BIT4;

// ADC entrada A1 (P1.5)
P1DIR &= ~BIT5;
P1SEL |= BIT5;
}

void setupTimerCapture() {
TA0CTL = TASSEL_2 | MC_2 | TACLR; // SMCLK, modo contínuo
TA0CCTL2 = CM_1 | CCIS_0 | SCS | CAP | CCIE; // Captura borda de subida
}

void setupADC() {
ADC10CTL1 = INCH_1; // A1 (P1.5)
ADC10CTL0 = SREF_0 | ADC10SHT_3 | ADC10ON;
}

void setupUART() {
UCA0CTL1 |= UCSWRST;
UCA0CTL1 |= UCSSEL_2;

UCA0BR0 = 104; // 1MHz / 9600
UCA0BR1 = 0;
UCA0MCTL = UCBRS_1;

UCA0CTL1 &= ~UCSWRST;
}

// === Funções principais ===

void iniciarMedicaoHidratacao() {
TA0CTL |= TACLR;
P1OUT &= ~BIT4; // descarga
__delay_cycles(50000);
P1OUT |= BIT4; // carga
}

unsigned int medirOleosidade() {
ADC10CTL0 |= ENC | ADC10SC;
while (ADC10CTL1 & ADC10BUSY);
return ADC10MEM;
}

// === UART ===

void uart_print(const char *str) {
while (*str) {
while (!(IFG2 & UCA0TXIFG));
UCA0TXBUF = *str++;
}
}

void uart_print_int(unsigned int num) {
char buf[6];
int i = 0;
if (num == 0) {
uart_print("0");
return;
}
while (num > 0) {
buf[i++] = (num % 10) + '0';
num /= 10;
}
int j;
for (j = i - 1; j >= 0; j--) {
while (!(IFG2 & UCA0TXIFG));
UCA0TXBUF = buf[j];
}
}

// === Classificações ===

const char* classificarHidratacao(unsigned int tempo_us) {
if (tempo_us < 100)
return "Pele seca";
else if (tempo_us < 180)
return "Pele normal";
else
return "Pele hidratada";
}

const char* classificarOleosidade(unsigned int tensao_mV) {
if (tensao_mV < 1100)
return "Pele seca";
else if (tensao_mV < 1500)
return "Pele normal";
else
return "Pele oleosa";
}

// === Interrupção do Timer Capture ===

#pragma vector = TIMER0_A1_VECTOR
__interrupt void TIMER0_A1_ISR(void) {
switch (TA0IV) {
case TA0IV_TACCR2:
tempo_rc = TA0CCR2;
flag_captura = 1;
P1OUT &= ~BIT4; // Para carga
P1OUT ^= BIT0; // Toggle LED
break;
default:
break;
}
}
