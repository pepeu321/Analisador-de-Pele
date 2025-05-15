# Comunicação dos sensores : 

Tanto o sensor de hidratação como o de oleosidade, possuem  saídas analógicas. 

## Hidratação : 
O sensor de hidratação é composto pelo circuito RC, quando aplicado uma tensão o capacitor, sua tensão cresce de forma exponencial onde o tempo para ele carregar pode ser calculado como 𝛕 = R*C , quando entrar em contato com a pele esse valor irá mudar, já que a resistência do circuito também irá mudar.
O MSP430 possui timers configuráveis em modo de captura, que podem registrar o instante exato em que a tensão no capacitor ultrapassa um determinado valor lógico. Conectando a saída do circuito RC a um pino de captura, o microcontrolador mede o tempo entre o início da carga e a transição lógica alta.
Esse tempo está diretamente relacionado à hidratação da pele, logo a comunicação entre o sensor e o microcontrolador ocorre por meio da detecção de borda digital em uma entrada de captura, que interpreta um valor analógico (carga de capacitor) como um tempo digital proporcional.

## Oleosidade: 
Como sensor de oleosidade é feito com um fototransistor, onde a tensão varia de acordo com a intensidade de luz refletida na pele. Pelo fato de ser uma tensão analógica contínua. Sua comunicação com o microcontrolador será feita por meio do ADC de 12bits, a tensão será convertida em um valor digital, que vai ser usada para definir o nível de oleosidade da pele. 
O ADC12 é configurado para converter o valor de tensão (de 0 a 3,3 V) em um valor digital entre 0 e 4095. Com isso, o microcontrolador consegue interpretar o nível de oleosidade da pele onde a leitura vai ser feita em um intervalo periódico.
