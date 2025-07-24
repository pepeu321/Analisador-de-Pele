# Esquematico Eletrônico 

<img width="1115" height="766" alt="image" src="https://github.com/user-attachments/assets/be6ef602-beb6-4531-b34a-b2448d1ec82b" />


## Sensor de Hidratação

<img width="822" height="542" alt="image" src="https://github.com/user-attachments/assets/05ca86e0-e62e-41b4-868e-61ec3172c166" />

O sensor de hidratação foi desenvolvido com base na application note da Texas Instruments, que implementa os periféricos Comparator_A+ e Timer_A do MSP430G2553. Um capacitor é carregado e, em seguida, descarregado através de uma resistência selecionável entre uma referência fixa (R_REF) e a resistência da pele (R_MEAS). A tensão do capacitor é monitorada pelo comparador analógico, que gera uma transição lógica quando ela atinge menos que 0,25 × Vcc, porque o comparador tem que disparar na descida. Esse evento é capturado por uma entrada de captura do Timer_A (CCI1B), permitindo a medição precisa do tempo de descarga. Como a constante de tempo RC é diretamente proporcional à resistência, o tempo medido reflete a resistência conectada, viabilizando medições com alta resolução utilizando apenas componentes internos do microcontrolador e um capacitor externo.

## Sensor de Oleosidade

<img width="425" height="298" alt="image" src="https://github.com/user-attachments/assets/c7f38bee-c7b9-43f0-a236-ead251fa263e" />

O sensor de oleosidade da pele é implementado por meio de um sensor óptico infravermelho conectado ao conector J3. A leitura do sinal analógico refletido pela pele é feita pelo pino OILINESS_SENSE do MSP430, que está ligado a um canal do ADC interno. Um capacitor de desacoplamento (C4) é incluído para atenuar ruídos e garantir estabilidade da leitura. A intensidade do sinal IR refletido varia conforme a oleosidade da superfície da pele, permitindo estimar esse parâmetro fisiológico com base na variação da tensão analógica capturada pelo microcontrolador.

## Display

<img width="397" height="304" alt="image" src="https://github.com/user-attachments/assets/2cfa5826-75df-4343-9ba3-d0345ebcfff7" />

A interface de exibição OLED utiliza comunicação I2C, com o display conectado ao MSP430 por meio dos sinais DISP_SCL (clock) e DISP_SDA (dados), expostos no conector J2. Os resistores de pull-up R2 e R3 garantem os níveis lógicos corretos nas linhas do barramento. Essa interface é para exibir os resultados das medições dos parâmetros da pele, status do sistema ou outras informações relevantes para o usuário.


## Bloco de programação

<img width="316" height="303" alt="image" src="https://github.com/user-attachments/assets/ff93eaae-6645-4deb-a54d-8d01fb5a5c79" />

O bloco de programação e depuração do MSP430 é baseado na interface Spy-Bi-Wire, acessível pelo conector J5. Os sinais SBWTCK e SBWTDIO são conectados diretamente ao microcontrolador e acompanhados por resistores de pull-up R5 e R6 para garantir níveis estáveis durante o processo de gravação.

## Fonte de alimentação (USB-C)

<img width="298" height="312" alt="image" src="https://github.com/user-attachments/assets/c83981c3-8eda-42ce-b52c-ac5ef24b200d" />

A fonte de alimentação via USB-C é implementada com o conector J6, responsável por fornecer os 5V de entrada do sistema. Os resistores R4 e R5, de 5,1 kΩ, são conectados aos pinos CC1 e CC2 do USB-C, sinalizando ao carregador a solicitação de energia conforme o padrão USB Power Delivery. A linha VBUS resultante fornece 5V estabilizados, que são encaminhados tanto para o circuito de carregamento da bateria quanto para o regulador de tensão responsável por alimentar o restante do sistema.

## Sistema de Gerenciamento de bateria 

<img width="884" height="407" alt="image" src="https://github.com/user-attachments/assets/6ceb09d2-8dbe-444e-9413-59e2417be417" />


O sistema de gerenciamento de bateria utiliza o circuito integrado HT4928S (U2) para controlar o carregamento de uma célula de íon de lítio conectada aos terminais BAT+ e BAT–. O CI realiza controle de corrente e tensão para garantir o carregamento seguro da bateria, além de fornecer indicação visual do estado de carga por meio dos LEDs D1 e D2. Além da função de carga, o HT4928S também incorpora um conversor boost, elevando a tensão da bateria para 5V quando necessário. Essa tensão é então regulada para 3,3V por meio do regulador linear AMS1117-3.3 (U3), que alimenta o MSP430 e seus periféricos, garantindo estabilidade e operação contínua mesmo com variações na tensão da bateria.

## Microcontrolador

<img width="1033" height="593" alt="image" src="https://github.com/user-attachments/assets/1193e60a-c515-4e73-b430-959917dbacdd" />

O microcontrolador MSP430G2553, posicionado como unidade central do sistema, coordena todas as funções de aquisição, controle e comunicação. Ele é alimentado com 3,3V e o oscilador interno para simplificar a aplicação. Suas entradas e saídas digitais controlam a carga e descarga do capacitor, realizam leituras analógicas do sensor óptico, interagem com o display OLED via I2C e processam eventos do comparador analógico.
