# Integração dos sensores

```cpp

#include <msp430.h>
#include <stdio.h>

volatile unsigned int tempo_rc = 0;
volatile unsigned char flag_captura = 0;

void setupGPIO();
void setupTimerCapture();
void setupADC();
void setupUART();

unsigned int medirOleosidade();
void iniciarMedicaoHidratacao();
void uart_print(char *str);
const char* classificarHidratacao(float tempo_us);
const char* classificarOleosidade(float tensao);

void main(void) {
    WDTCTL = WDTPW | WDTHOLD;   // Para watchdog
    BCSCTL1 = CALBC1_1MHZ;      // Clock 1 MHz
    DCOCTL = CALDCO_1MHZ;

    setupGPIO();
    setupUART();
    setupTimerCapture();
    setupADC();

    __enable_interrupt();

    char buffer[64];

    while (1) {
        // === Medição de hidratação ===
        iniciarMedicaoHidratacao();
        __delay_cycles(50000); // Aguarda um pouco (descarga capacitor)
        while (!flag_captura); // Espera captura do timer
        flag_captura = 0;

        // === Medição de oleosidade ===
        unsigned int adc_value = medirOleosidade();

        float tempo_us = (float)tempo_rc; // 1 ciclo = 1us @1MHz
        float tensao = adc_value * 3.3 / 1023.0;

        const char* classificacaoH = classificarHidratacao(tempo_us);
        const char* classificacaoO = classificarOleosidade(tensao);

        // === Exibição UART ===
        sprintf(buffer, "\r\nHidratacao: %d us (%s)\r\n", tempo_rc, classificacaoH);
        uart_print(buffer);

        int parte_int = (int)tensao;
        int parte_decimal = (int)((tensao - parte_int) * 100); // 2 casas decimais

        sprintf(buffer, "Oleosidade: %d.%d V (%s)\r\n", parte_int, parte_decimal, classificacaoO);
        uart_print(buffer);

        __delay_cycles(2000000); // Aguarda ~2 segundos
    }
}

// === Configurações ===
void setupGPIO() {
    P1DIR |= BIT0; // LED para debug
    P1OUT &= ~BIT0;

    // UART TX (P1.1)
    P1DIR |= BIT1;
    P1SEL |= BIT1;
    P1SEL2 |= BIT1;

    // UART RX (P1.2)
    P1DIR &= ~BIT2;
    P1SEL |= BIT2;
    P1SEL2 |= BIT2;

    // Timer capture P1.3 (TA0.2) como entrada para hidratação
    P1DIR &= ~BIT3;
    P1SEL |= BIT3;

    // Controle carga capacitor em P1.4 (saida digital)
    P1DIR |= BIT4;
    P1OUT &= ~BIT4;

    // ADC entrada P1.5 (A1)
    P1DIR &= ~BIT5;
    P1SEL |= BIT5;
}

// Timer capture em TA0CCR2 - P1.3
void setupTimerCapture() {
    TA0CTL = TASSEL_2 | MC_2 | TACLR; // SMCLK, modo contínuo
    TA0CCTL2 = CM_1 | CCIS_0 | SCS | CAP | CCIE; // Captura borda de subida no CCR2
}

// Configura ADC no canal A1 (P1.5)
void setupADC() {
    ADC10CTL1 = INCH_1; // Canal A1 (P1.5)
    ADC10CTL0 = SREF_0 | ADC10SHT_3 | ADC10ON;
}

// Configura UART 9600 bauds
void setupUART() {
    UCA0CTL1 |= UCSWRST;             // Reset UART
    UCA0CTL1 |= UCSSEL_2;            // SMCLK

    UCA0BR0 = 104;                   // 1MHz / 9600 baud
    UCA0BR1 = 0;
    UCA0MCTL = UCBRS_1;              // Modulação

    UCA0CTL1 &= ~UCSWRST;            // Libera UART
}

// Função para medir oleosidade via ADC
unsigned int medirOleosidade() {
    ADC10CTL0 |= ENC | ADC10SC;         // Inicia conversão
    while (ADC10CTL1 & ADC10BUSY);      // Aguarda fim
    return ADC10MEM;
}

// Função para iniciar medição de hidratação (descarga e carga capacitor)
void iniciarMedicaoHidratacao() {
    TA0CTL |= TACLR;       // Zera timer

    P1OUT &= ~BIT4;        // Descarrega capacitor (P1.4=0)
    __delay_cycles(50000); // Aguarda descarga (~50ms)

    P1OUT |= BIT4;         // Começa carga capacitor (P1.4=1)
}

// Envia string via UART
void uart_print(char *str) {
    while (*str) {
        while (!(IFG2 & UCA0TXIFG)); // Aguarda buffer TX livre
        UCA0TXBUF = *str++;
    }
}

// Classificação da hidratação (tempo de carga em us)
const char* classificarHidratacao(float tempo_us) {
    if (tempo_us < 100)
        return "Pele seca";
    else if (tempo_us < 180)
        return "Pele normal";
    else
        return "Pele hidratada";
}

// Classificação da oleosidade pela tensão (em volts)
const char* classificarOleosidade(float tensao) {
    if (tensao < 1.1)
        return "Pele seca";
    else if (tensao < 1.5)
        return "Pele normal";
    else
        return "Pele oleosa";
}


// ISR do timer (captura TA0CCR2)
#pragma vector = TIMER0_A1_VECTOR
__interrupt void TIMER0_A1_ISR(void) {
    switch (TA0IV) {
        case TA0IV_TACCR2: {
            tempo_rc = TA0CCR2;
            flag_captura = 1;
            P1OUT &= ~BIT4; // Para carga capacitor (pino P1.4 = 0)

            P1OUT ^= BIT0; // Toggle LED para debug
            break;
        }
        default:
            break;
    }
}

