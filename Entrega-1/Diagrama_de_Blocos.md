# Diagrama de Blocos

## Descrição básica do diagrama de blocos:  
Os sinais serão extraídos da camada mais superficial da pele, a epiderme. Para o sensor de umidade/ressecamento, que utiliza um circuito RC, será considerada a variação da impedância elétrica, com ênfase na capacitância, a qual se altera conforme a pele se apresenta mais úmida ou ressecada.

Já para o sensor de oleosidade, baseado em um fotodiodo, será considerada a variação da intensidade luminosa no espectro do infravermelho próximo, que muda conforme o nível de oleosidade da pele.

O sinal proveniente do sensor de umidade será processado por um conversor analógico-digital (ADC), integrado ao microcontrolador da família MSP430. Posteriormente, será utilizado um timer interno para medir o tempo de carga e descarga do circuito RC, o qual está relacionado à umidade da pele.

O sinal do sensor de oleosidade também será convertido por um ADC, permitindo a coleta de dados analógicos com precisão.

Por fim, os níveis de oleosidade e umidade da pele serão exibidos de forma quantitativa e simultânea em um display LCD, expressos em percentual (%), facilitando a interpretação dos dados pelo usuário.


#### ![Diagrama de blocos](https://github.com/user-attachments/assets/5bc94487-e463-4839-9487-04b369517917)

