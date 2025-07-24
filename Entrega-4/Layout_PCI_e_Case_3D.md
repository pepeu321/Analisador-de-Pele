## Introdução

O layout da placa de circuito impresso (PCI) foi desenvolvido para organizar os componentes do sistema de forma funcional e compacta. O sistema foi projetado para medir dois parâmetros da pele humana: hidratação e oleosidade, por meio de sensores conectados à placa. A disposição dos elementos levou em consideração o posicionamento dos sensores , a alimentação por bateria e a exibição dos dados em um display, buscando eficiência na montagem e no uso do dispositivo. O projeto do layout foi elaborado no software KiCad, e a partir das dimensões e do posicionamento dos componentes na placa, foi possível modelar o gabinete que a acomoda.

## Desenvolvimento - Placa do circuito

A placa foi produzida em fibra de vidro cobreada com dimensões de 9 x 3 cm. A transferência do layout foi feita por meio de prensa térmica, seguida pela corrosão química do cobre para formação das trilhas. Após esse processo, a placa foi estanhada para evitar oxidação e aumentar a durabilidade do circuito. Em seguida, os componentes SMD foram soldados nas posições definidas no layout.

O posicionamento dos componentes segue uma lógica da direita para a esquerda. À direita da placa encontra-se a porta USB-C, responsável pela recarga da bateria de 3,7 V posicionada na parte superior. Ao lado da porta, foi inserido um conversor buck-boost que regula a tensão de alimentação do sistema. A bateria e os componentes de controle de carga foram agrupados próximos a essa região para facilitar a distribuição de energia.

Na parte central está o microcontrolador, montado em um soquete DIP para facilitar reprogramação ou substituição. O display OLED foi fixado na parte superior da placa, diretamente acima do microcontrolador, sendo responsável por exibir as leituras dos sensores. À esquerda da placa estão conectados os sensores. O sensor de oleosidade utiliza um LED infravermelho e um fototransistor posicionados no gabinete, enquanto a leitura de hidratação é realizada por meio de dois conectores metálicos externos que fazem contato direto com a pele do usuário, permitindo a medição capacitiva. O design do gabinete foi desenvolvido com base nas dimensões e pontos de conexão da placa, garantindo encaixe preciso e exposição adequada dos sensores.

<img width="1532" height="556" alt="image" src="https://github.com/user-attachments/assets/421586b8-6a52-4bb1-b414-398731dad987" />

![WhatsApp Image 2025-07-24 at 15 44 23](https://github.com/user-attachments/assets/11c58c22-549e-433c-b818-50e5062d604f)

![WhatsApp Image 2025-07-24 at 15 44 23 (1)](https://github.com/user-attachments/assets/929dc23c-68a1-4125-91f6-bc3fbe644acf)

# Desenvolvimento – Case 3D

O gabinete do dispositivo foi modelado em 3D utilizando o software Onshape, com base no layout da placa desenvolvido no KiCad. A partir da exportação das dimensões e do posicionamento dos componentes da PCI, foi possível projetar uma case com encaixe preciso e funcional.O design inclui aberturas para o display OLED, a porta USB-C e os pinos metálicos do sensor capacitivo, permitindo a interação direta com a pele do usuário. A estrutura foi composta por uma base com dobradiças integradas e uma tampa superior encaixável, facilitando a montagem e o acesso aos componentes internos. Após a impressão do primeiro protótipo, foi adicionada uma extensão frontal para melhorar o acabamento estético da case e aprimorar sua apresentação visual.

<img width="1280" height="599" alt="Captura de tela 2025-07-24 163804" src="https://github.com/user-attachments/assets/0ca98c4e-8b6f-464e-9529-dfdae3bfb350" />
<img width="1142" height="609" alt="image" src="https://github.com/user-attachments/assets/a89c1b9e-ee1a-479f-99de-1a762cdeae54" />
<img width="1233" height="633" alt="image" src="https://github.com/user-attachments/assets/7514d8f2-a449-4274-b381-c8bc8f1886f6" />
<img width="1425" height="641" alt="image" src="https://github.com/user-attachments/assets/43ae6bb7-9121-444e-8215-6ae3c503ecb2" />

A integração entre a placa e o gabinete 3D permitiu a montagem precisa do dispositivo, alinhando a estrutura física ao posicionamento dos componentes. Os dois pinos metálicos utilizados na leitura capacitiva foram fixados na tampa do gabinete e conectados à placa por fios, possibilitando o contato direto com a pele do usuário. Além disso, o encaixe definido no design garantiu uma distância fixa entre o sensor de oleosidade e a superfície da pele, contribuindo para maior consistência nos resultados de medição.

![WhatsApp Image 2025-07-24 at 15 44 25](https://github.com/user-attachments/assets/3b7cd4eb-716c-4674-a4d2-9d66ce590ab9)
![WhatsApp Image 2025-07-24 at 17 09 29](https://github.com/user-attachments/assets/454a57c9-7ec4-434b-9e7d-ac73367a2191)



