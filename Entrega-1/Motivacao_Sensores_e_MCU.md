# Motivação dos Sensores e Microcontrolador

## Microcontrolador MSP430xxxx: 
Controla os sensores e processa os dados de hidratação e oleosidade, exibindo as informações no display LCD.

ADC de 12 bits; 

Timer com modo de captura;

Número suficiente de pinos;

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
