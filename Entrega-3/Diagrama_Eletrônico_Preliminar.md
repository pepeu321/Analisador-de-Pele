** Diagrama Eletrônico Preliminar

O esquemático foi desenvolvido para atender a todas as exigências do projeto 
físico da placa de circuito impresso. O uso do microcontrolador em formato standalone 
(apenas o chip) exige cuidados específicos para garantir seu funcionamento adequado. Os 
sensores e o display foram substituídos por conectores de três e quatro pinos, 
respectivamente, do tipo Molex, devido à posição física dos sensores, localizados na 
extremidade de um case com 15 cm de comprimento. Embora o circuito esquemático seja 
simples e resulte em uma placa menor que o case, essa diferença de tamanho justifica o uso 
dos conectores, permitindo a ligação por fios até os sensores e a interface homem-máquina 
(display). Para facilitar o entendimento, o esquemático foi dividido em blocos funcionais. O 
esquemático está ilustrado na Figura 1, abaixo.

<img src="https://github.com/user-attachments/assets/b90740f7-07ac-4269-8522-715f42c57716" width="600">

 O primeiro bloco corresponde ao sensor de umidade, que utiliza um circuito RC 
conectado em série. Esse circuito altera sua impedância conforme o nível de umidade 
presente na pele. A alimentação é feita por meio de dois pinos: um conectado ao VCC (pino 
1) e outro ao GND (pino 3). O pino central (pino 2), ligado ao ponto de junção entre o resistor 
e o capacitor, envia a tensão do capacitor em relação ao GND ao microcontrolador. Essa 
leitura é feita através do pino 2 (P1.0), configurado como entrada para o TIMER0, 
responsável por medir o tempo de carga/descarga do capacitor.

<img src="https://github.com/user-attachments/assets/3f4f1581-72dd-4335-8799-d6ed578cb2e" width="400">

O bloco do sensor de oleosidade segue o mesmo princípio do sensor de umidade, 
a diferença está na saída do sinal: a tensão gerada no circuito é enviada ao microcontrolador 
por meio do pino p1.3, onde será convertida por um conversor analógico-digital (ADC) e 
posteriormente interpretada pelo sistema. O sensor de oleosidade pode ser visto na figura 3 
abaixo.


<img src="https://github.com/user-attachments/assets/aa0a775f-fe12-47d8-ba68-045394d3b007" width="400">

Este bloco representa a interface de programação e depuração do sistema, por 
meio de um conector macho de 2 pinos. Ele está conectado diretamente aos pinos TEST 
(17) e RST (16) do MSP430G2553, permitindo a gravação de firmware e depuração via 
protocolo SBW (Spy-Bi-Wire), padrão da linha MSP430. Para garantir a estabilidade do sinal 
de reset, foi adicionado um resistor pullup de 100 kΩ entre o pino RST e o VCC (3 V), 
mantendo o nível lógico alto durante a operação normal. Um capacitor de 100 nF entre o pino 
RST e o GND funciona como filtro, suprimindo ruídos e transientes que poderiam causar 
reinicializações indesejadas. A solução adotada garante robustez e compatibilidade com 
programadores padrão. A estrutura do bloco de reset e programação pode ser vista na figura 
4 abaixo.

<img src="https://github.com/user-attachments/assets/b64aa6e1-9f6c-42df-a595-ce717baf16c7" width="400">

O bloco de alimentação foi projetado com foco na portabilidade do produto, sendo 
utilizada uma bateria tipo moeda. As opções consideradas foram CR2450 (500 mAh) e 
CR2477 (1000 mAh), ambas de 3 V. Inicialmente cogitou-se o uso de uma CR2032, mas sua 
capacidade foi considerada insuficiente diante do consumo contínuo do display e dos 
sensores. Um capacitor de 100 nF foi adicionado em paralelo para filtragem de ruídos e 
estabilização da tensão de alimentação. A bateria será inserida em um soquete apropriado, 
garantindo fácil substituição. Optou-se pelas baterias do tipo moeda por sua praticidade, 
baixo custo e compatibilidade com o perfil do projeto. A bateria pode ser vista na figura 5 
abaixo.

<img src="https://github.com/user-attachments/assets/6c853dfe-253d-4a7b-8f44-84f1526dafb5" width="400">

 A interface visual do sistema é composta por um display OLED de 0,96 polegadas, 
com resolução de 128x64 pixels e comunicação via protocolo I²C. A conexão com o 
MSP430G2553 é feita através de um conector Molex fêmea de 4 pinos, que fornece as linhas 
de alimentação (VCC e GND) e os sinais de dados (SDA) e clock (SCL). O display é 
alimentado com 3 V, compatível com os níveis do microcontrolador. Os pinos 14 (SCL) e 15 
(SDA) do MSP430G2553 foram utilizados para essa comunicação. Foram incluídos 
resistores pullup de 10 kΩ nessas linhas, conforme exigido pelo padrão I²C, garantindo a 
integridade dos sinais e evitando estados indefinidos. Essa solução oferece uma interface 
gráfica de baixo consumo e boa legibilidade para o usuário. A interface gráfica pode ser vista 
figura 6 abaixo.

<img src="https://github.com/user-attachments/assets/b3ac2ec8-d25e-4678-8949-d0b14e09b885" width="400">

 A distribuição dos pinos do microcontrolador foi cuidadosamente planejada 
conforme as funcionalidades necessárias. Os pinos 16 (RST) e 17 (TEST) são reservados 
para programação e depuração. O pino 1 (VCC) fornece 3 V e o pino 20 (GND) é o terra do 
sistema. O pino 2 (P1.0) é utilizado para leitura do sensor de umidade via TIMER0, e o pino 5 
(P1.3) recebe o sinal analógico do sensor de oleosidade, convertido via ADC3. Os pinos 14 
(P1.6) e 15 (P1.7) foram reservados para a comunicação I²C com o display OLED. Os 
demais pinos não são utilizados neste projeto. As conexões utilizadas do microcontrolador 
podem ser vistas na figura 7 abaixo

<img src="https://github.com/user-attachments/assets/cbaf27f1-5af5-41ae-aaab-1fdce2186f61" width="400">

Para garantir imunidade a ruídos e prevenir consumo indevido ou comportamento 
inesperado, todos os pinos não utilizados do MSP430G2553 foram conectados a resistores 
pulldown de 10 kΩ. Embora seja possível configurar esses pinos em nível baixo via software, 
a solução física foi preferida por confiabilidade adicional. Os resistores foram conectados 
diretamente aos pinos 3, 4, de 6 a 13, além dos pinos 18 e 19, garantindo que esses 
terminais permaneçam em estado definido durante toda a operação do sistema.. A rede de 
resistores pulldown para os pinos não utilizados pode ser vista na figura 8 abaixo.

<img src="https://github.com/user-attachments/assets/16505323-f90a-4ccb-b831-3fc3c5657652" width="400">


