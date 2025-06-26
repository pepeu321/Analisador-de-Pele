# Diagrama de Blocos

O diagrama de blocos se manteve bem parecido com o desenvolvido inicialmente, alterando apenas o display LCD 16x2 para um do tipo OLED 0.96 I2C, com o objetivo de comportar melhor o protótipo final, já que ele necessita de apenas 4 fios e é bem menor em relação ao tamanho.

O funcionamento do sistema começa a patir do contato direto dos sensores com a pele. O sensor com fototransistor é responsável pela detecção da oleosidade da pele, convertendo a intensidade de luz refletida em um sinal analógico. Esse sinal é enviado para o microcontrolador através da entrada ADC (canal P1.4), onde será digitalizado e posteriormente processado.

Paralelamente, o sensor RC mede a hidratação da pele. Ele se baseia no tempo de carga de um capacitor em contato com a pele, que altera sua constante de tempo de acordo com a umidade. Esse tempo de carga é medido pelo microcontrolador utilizando um timer no modo captura, conectado ao pino P1.2. O valor capturado representa, indiretamente, o nível de hidratação.

Os dados obtidos de ambos os sensores são processados elo microcontrolador, que realiza a conversão para valores interpretáveis como porcentagem de oleosidade e hidratação e os exibe no display OLED, que está conectado via barramento I2C.

<img src="https://github.com/user-attachments/assets/efc14c64-123e-4ef4-a00c-e3ea1f21a52a" width="900">


