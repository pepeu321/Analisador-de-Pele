
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
