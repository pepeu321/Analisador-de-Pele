# Diagrama Eletrônico Preliminar

O esquemático foi desenvolvido para atender a todas as exigências do projeto 
físico da placa de circuito impresso. O uso do microcontrolador em formato standalone 
(apenas o chip) exige cuidados específicos para garantir seu funcionamento adequado. Os 
sensores e o display foram substituídos por conectores de três e quatro pinos, 
respectivamente, do tipo Molex, devido à posição física dos sensores, localizados na 
extremidade de um case com 15 cm de comprimento. Embora o circuito esquemático seja 
simples e resulte em uma placa menor que o case, essa diferença de tamanho justifica o uso 
dos conectores, permitindo a ligação por fios até os sensores e a interface homem-máquina 
(display). Para facilitar o entendimento, o esquemático foi dividido em blocos funcionais. O 
esquemático está ilustrado abaixo.

<img src="https://github.com/user-attachments/assets/6a11df59-0fff-46d8-9f59-b53c959bfdaf" width="600">

O primeiro bloco corresponde ao sensor de hidratação, que utiliza um circuito RC 
conectado em série. Esse circuito altera sua impedância conforme o nível de hidratação 
presente na pele. A alimentação é feita por meio de dois pinos: um conectado ao VCC (pino 1) e outro ao GND (pino 2). A saída será o ponto de junção entre o resistor 
e o capacitor, envia a tensão do capacitor em relação ao GND ao microcontrolador. Essa 
leitura é feita através do pino P1.2, configurado como entrada para o TIMER0, 
responsável por medir o tempo de carga/descarga do capacitor.

<img src="https://github.com/user-attachments/assets/6d2235bb-ab02-45aa-b8ab-b476d049a44c" width="200">

O bloco do sensor de oleosidade segue o mesmo princípio do sensor de umidade, 
a diferença está na saída do sinal: a tensão gerada no circuito é enviada ao microcontrolador 
por meio do pino P1.4, onde será convertida por um conversor analógico-digital (ADC) e 
posteriormente interpretada pelo sistema.

<img src="https://github.com/user-attachments/assets/157d8141-3018-48fa-a184-5f0bb6f63962" width="200">

Este bloco representa a progamação via SBW(Spy-Bi-Wire), é a interface de progamação e depuração para o microcontralador, ela permite a comunicação ente o msp430 e o computador a partir de dois pinos, SBWTCK (clock) e SBWTDIO(dados entrada e saída). Possui um diodo schottky para proteger a linha de alimentação contra inversão da polaridade e um resistor de 47kΩ é colocado no pino SBWTDIO para garantir um nível lógico alto quando a linha não esta ociosa.

<img src="https://github.com/user-attachments/assets/12095c71-1ff4-4c0e-adad-62e410ff8643" width="200">

O bloco de alimentação foi projetado com foco na portabilidade do produto, sendo 
utilizada uma bateria tipo moeda. As opções consideradas foram CR2450 (500 mAh) e 
CR2477 (1000 mAh), ambas de 3 V. Inicialmente cogitou-se o uso de uma CR2032, mas sua 
capacidade foi considerada insuficiente diante do consumo contínuo do display e dos 
sensores. Um capacitor de 100 nF foi adicionado em paralelo para filtragem de ruídos e 
estabilização da tensão de alimentação. A bateria será inserida em um soquete apropriado, 
garantindo fácil substituição. Optou-se pelas baterias do tipo moeda por sua praticidade, 
baixo custo e compatibilidade com o perfil do projeto.

<img src="https://github.com/user-attachments/assets/c0e09914-422e-412c-a52c-3c2d4d48eee7" width="200">

 A interface visual do sistema é composta por um display OLED de 0,96 polegadas, 
com resolução de 128x64 pixels e comunicação via protocolo I²C. A conexão com o 
msp é feita através de um conector Molex fêmea de 4 pinos, que fornece as linhas 
de alimentação (VCC e GND) e os sinais de dados (SDA) e clock (SCL). O display é 
alimentado com 3.3 V, compatível com os níveis do microcontrolador. Os pinos P1.6 (SCL) e P1.7 
(SDA) do microcontralador foram utilizados para essa comunicação. Foram incluídos 
resistores de 4.7kΩ nessas linhas, garantindo a integridade dos sinais e evitando estados indefinidos.

<img src="https://github.com/user-attachments/assets/c4aea0c2-9675-4da8-8f02-1e766bb4aaa8" width="200">

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


