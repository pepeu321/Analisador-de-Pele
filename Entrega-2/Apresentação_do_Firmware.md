# Sensor de Oleosidade

O código a seguir exemplifica a integração de um sensor de oleosidade com o microcontrolador MSP430. A principal função do sistema é medir a intensidade da luz refletida pela pele, captada por um fototransistor conectado a uma entrada analógica (canal A1). Esse sinal analógico é convertido em valor digital por meio do conversor analógico-digital (ADC) interno do MSP430. O valor convertido é então formatado e transmitido via UART para um terminal serial, permitindo a monitorização em tempo real da resposta do sensor. Essa comunicação é fundamental para a validação e calibração do sensor antes de sua integração ao sistema completo. O processo de leitura e transmissão é repetido automaticamente a cada segundo.



```cpp
// SENSOR_OLEOSIDADE


#include <msp430.h>
#include <stdio.h>

void uart_init(void) {
    P1SEL |= BIT2;         // Apenas TX (P1.2)
    P1SEL2 |= BIT2;

    UCA0CTL1 |= UCSSEL_2;  // SMCLK
    UCA0BR0 = 104;         // 1MHz 9600 baud
    UCA0BR1 = 0;
    UCA0MCTL = UCBRS0;
    UCA0CTL1 &= ~UCSWRST;
}

void uart_send_string(const char *str) {
    while (*str) {
        while (!(IFG2 & UCA0TXIFG));
        UCA0TXBUF = *str++;
    }
}

void adc_init(void) {
    ADC10CTL1 = INCH_1;              // Canal A1
    ADC10CTL0 = SREF_0 + ADC10SHT_3 + ADC10ON;
    __delay_cycles(1000);            // Espera ADC estabilizar
}

unsigned int read_adc(void) {
    ADC10CTL0 |= ENC + ADC10SC;      // Inicia conversão
    while (ADC10CTL1 & ADC10BUSY);   // Espera finalizar
    return ADC10MEM;                 // Retorna resultado
}

void delay_ms(unsigned int ms) {
    while (ms--) {
        __delay_cycles(1000); // 1ms se clock = 1MHz
    }
}

int main(void) {
    WDTCTL = WDTPW | WDTHOLD;

    uart_init();
    adc_init();

    char buffer[32];

    while (1) {
        unsigned int adc_value = read_adc();

        // Converte para string e envia
        sprintf(buffer, "ADC: %d\r\n", adc_value);
        uart_send_string(buffer);

        delay_ms(1000);  // Lê a cada 1s
    }
}
```

# Sensor de Hidratação

Para o sensor de hidratação, foi desenvolvido e testado um código baseado na medição do tempo de carga de um circuito RC, utilizando o Timer_A do MSP430 em modo de captura. O tempo registrado foi transmitido via UART para um terminal serial, permitindo a observação em tempo real dos valores durante a execução. Assim como no sensor de oleosidade, a comunicação serial foi essencial para validar o comportamento do circuito de forma isolada, antes da integração final dos sensores ao sistema completo. O funcionamento do programa consiste em aguardar um pulso digital (borda de subida) no pino P1.2. Quando o pulso é detectado, o Timer salva o valor atual do contador no registrador TA0CCR1. Uma interrupção é então acionada, e o tempo entre o pulso atual e o anterior é calculado. Esse tempo, representando o intervalo entre eventos, é então enviado via UART ao terminal. O ciclo se repete a cada 1 segundo. O Timer opera em modo contínuo, contando de 0 até 65535 e reiniciando automaticamente após atingir esse valor.

```cpp
// SENSOR HIDRATAÇÃO 

#include <msp430.h>
#include <stdio.h>

volatile unsigned int start_time = 0;
volatile unsigned int captured_time = 0;
volatile int captured = 0;

void uart_init(void) {
    P1SEL |= BIT1 + BIT2;  // P1.1 = RXD, P1.2 = TXD
    P1SEL2 |= BIT1 + BIT2;

    UCA0CTL1 |= UCSSEL_2;  // SMCLK
    UCA0BR0 = 104;         // 1MHz 9600
    UCA0BR1 = 0;
    UCA0MCTL = UCBRS0;
    UCA0CTL1 &= ~UCSWRST;
}

void uart_send_string(const char *str) {
    while (*str) {
        while (!(IFG2 & UCA0TXIFG));
        UCA0TXBUF = *str++;
    }
}

void timer_init(void) {
    TA0CTL = TASSEL_2 + MC_2 + TACLR;       // SMCLK, modo contínuo
    TA0CCTL1 = CM_1 + CCIS_0 + SCS + CAP + CCIE;  // Captura borda de subida, CC1, sincrono, interrupção
    P1DIR &= ~BIT2;                         // P1.2 como entrada (TA0.1)
    P1SEL |= BIT2;                          // Função alternativa: TA0.1
}

#pragma vector=TIMER0_A1_VECTOR
__interrupt void Timer_A(void) {
    if (TA0IV == TA0IV_TACCR1) {
        captured_time = TA0CCR1 - start_time;
        captured = 1;
    }
}

void delay_ms(unsigned int ms) {
    while (ms--) {
        __delay_cycles(1000); // Aproximado para 1MHz
    }
}

int main(void) {
    WDTCTL = WDTPW | WDTHOLD;

    uart_init();
    timer_init();

    __enable_interrupt();

    while (1) {
        captured = 0;
        start_time = TA0R;

        // Aguardar captura
        while (!captured);

        char buffer[32];
        sprintf(buffer, "Tempo: %d us\r\n", captured_time);
        uart_send_string(buffer);

        delay_ms(1000);
    }
}
```



