# Motivação dos Sensores e Microcontrolador

## Microcontrolador MSP430xxxx: 
A definição do microcontrolador a ser utilizado no projeto foi pela necessidade de garantir precisão e estabilidade na aquisição de sinais analógicos provenientes dos sensores. Optou-se por um microcontrolador que oferece recursos adequados para esse tipo de aplicação, como conversor analógico-digital (ADC) de 12 bits, timer no modo de captura e quantidade suficiente de pinos de entrada e saída, essenciais para a conexão direta com os sensores e o display LCD.


## Sensor de Hidratação – Circuito RC: 

A hidratação da pele pode ser estimada por meio de sua permissividade elétrica, que está relacionada à quantidade de água presente. Sensores capacitivos são
capazes de detectar essa variação, pois a pele mais hidratada apresenta maior constante dielétrica. O funcionamento é baseado na geração de um campo capacitivo.
Esta capacitância é formada por duas placas metálicas carregadas com cargas elétricas que tem o seu campo elétrico alterado na aproximação do material a ser detectado, alterando assim a capacitância das placas

A capacitância pode ser medida indiretamente através do tempo de carga de um capacitor em um circuito RC. O tempo que um capacitor leva para carregar até 
certo nível de tensão depende da constante de tempo τ=R⋅C. Aplicando uma entrada, a tensão no capacitor tem o seguinte formato:

VC​(t)=Vin​⋅(1−e^(−t/RC)).

Com o timer do microcontrolador em modo de captura, é possível detectar o tempo que o capacitor leva para atingir uma tensão conhecida

## Sensor de Oleosidade - Fotodiodo: 

A oleosidade da pele influencia a forma como a pele reflete ou absorve luz. Quanto mais oleosa, mais luz tende a ser refletida, e menos absorvida. Essa propriedade pode ser medida usando um sistema óptico.
Esse sistema vai ser composto por LED infravermelho e um fotodiodo que consegue detectar a luz que é refletida nele. 
Quando a luz incide sobre a camada de depleção com energia suficiente, ela ioniza os átomos na estrutura do cristal e gera pares elétron-lacuna. O campo elétrico existente, devido a polarização, fará com que os elétrons
se movam para o cátodo e as lacunas se movam para o ânodo,dando origem a uma fotocorrente. Quanto maior a intensidade da luz, maior a fotocorrente
