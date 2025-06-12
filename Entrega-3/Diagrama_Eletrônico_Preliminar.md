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


![image](https://github.com/user-attachments/assets/b90740f7-07ac-4269-8522-715f42c57716)

 O primeiro bloco corresponde ao sensor de umidade, que utiliza um circuito RC 
conectado em série. Esse circuito altera sua impedância conforme o nível de umidade 
presente na pele. A alimentação é feita por meio de dois pinos: um conectado ao VCC (pino 
1) e outro ao GND (pino 3). O pino central (pino 2), ligado ao ponto de junção entre o resistor 
e o capacitor, envia a tensão do capacitor em relação ao GND ao microcontrolador. Essa 
leitura é feita através do pino 2 (P1.0), configurado como entrada para o TIMER0, 
responsável por medir o tempo de carga/descarga do capacitor.

![image](https://github.com/user-attachments/assets/5e04ad59-0688-4106-bd58-50503d780dec)


O bloco do sensor de oleosidade segue o mesmo princípio do sensor de umidade, 
a diferença está na saída do sinal: a tensão gerada no circuito é enviada ao microcontrolador 
por meio do pino p1.3, onde será convertida por um conversor analógico-digital (ADC) e 
posteriormente interpretada pelo sistema. O sensor de oleosidade pode ser visto na figura 3 
abaixo.
<img src="[https://github.com/user-attachments/assets/c0b63acd-4973-4f88-a44e-d2b86c7ad8c5](https://github.com/user-attachments/assets/11b06461-3b69-4c71-aa1d-ae8c794f2f22)" width="400">

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

