# Testes individuais dos Sensores 

## OLEOSIDADE

### Sensor de Oleosidade:

O sensor de oleosidade é responsável por identificar a quantidade de óleo presente na superfície da pele, atuando como um indicador do nível de oleosidade. Esse sensor é composto por um emissor de luz (LED Infravermelho) e um fototransistor encapsulados juntos em uma estrutura opaca, de forma que o LED ilumina diretamente a pele e o fototransistor detecta a luz refletida. A quantidade de luz refletida varia conforme as propriedades da pele, quanto mais oleosa, maior a reflexão, permitindo inferir o nível de oleosidade.

Funcionamento Básico:
* Emissão de Luz: O LED Infravermelho emite luz direcionada à superfície da pele.
* Reflexão e Detecção: Parte dessa luz é refletida de volta pela pele. O fototransistor, posicionado ao lado do LED, capta a intensidade dessa luz refletida. Mas entre o fototransistor e o LED tem uma barreira para um não interferir no outro
* Variação de Sinal: A quantidade de luz refletida altera a corrente conduzida pelo fototransistor. 
* Leitura da Tensão: A tensão de saída do circuito é monitorada. Quanto maior o nível de reflexão da pele, maior a tensão de saída.

<img src="https://github.com/user-attachments/assets/c0b63acd-4973-4f88-a44e-d2b86c7ad8c5" width="400">

<img src="https://github.com/user-attachments/assets/463a3d83-a938-4d63-9ef3-5844629f3552" width="400">

<br>
<br>

**Pele sem óleo**  
<img src="https://github.com/user-attachments/assets/09280e50-2357-422d-b35c-59f849c60f2c" width="400">

**Pele com pouco óleo**  
<img src="https://github.com/user-attachments/assets/584d0fc5-bb4e-43cf-98ea-72a5269ba30d" width="400">

**Pele com um pouco mais de óleo**  
<img src="https://github.com/user-attachments/assets/f38e8578-8f4e-4123-ab84-68ae72efefed" width="400">

**Pele com muito óleo**  
<img src="https://github.com/user-attachments/assets/71a4995e-f0bf-43bf-b40e-8926ebaa1121" width="400">

Durante os testes práticos com o sensor de oleosidade, foram realizadas medições de tensão correspondentes a diferentes condições da pele. Os valores obtidos foram:

| | Tensão (V) |
| -------- | -------- |
| Pele sem óleo | 990m |
| Pele com pouco óleo   | 1,07   |
| Pele com um pouco mais de óleo   | 1,35   |
| Pele com muito óleo | 1,60 |

Observa-se que a tensão de saída aumenta proporcionalmente ao nível de oleosidade presente na pele. Isso ocorre porque a superfície mais oleosa reflete mais luz, fazendo com que o fototransistor conduza mais corrente e, consequentemente, aumente a tensão na saída do circuito.

## HIDRATAÇÃO

### Sensor de Hidratação:

No projeto, o sensor de hidratação tem como objetivo detectar a umidade da pele por meio da variação da capacitância entre dois eletrodos paralelos. Esses eletrodos formam um capacitor de placas, cuja capacitância muda conforme a condutividade e o teor de água presentes na pele. A medição é feita utilizando um circuito RC simples, onde a constante de tempo depende diretamente da capacitância formada pelos eletrodos em contato com a pele.
Funcionamento Básico:
* Eletrodos em Paralelo: Dois terminais metálicos são posicionados em paralelo com um capacitor de 100pF, formando um capacitor cuja capacitância varia conforme a pele entra em contato com eles.
* Circuito RC: Um resistor de 10kΩ é ligado em série com capacitor , formando um circuito RC.
* Leitura da Tensão: A tensão no terminal comum entre o resistor e os eletrodos é monitorada. Quanto maior a hidratação da pele, maior a capacitância entre os eletrodos, e mais lenta será a carga do capacitor, resultando em uma tensão mais baixa.

**Circuito RC**  
<img src="https://github.com/user-attachments/assets/042996c4-1e62-4679-a959-658a7dee9f7d" width="400">

**Sem toque na pele**  
<img src="https://github.com/user-attachments/assets/424c17da-8860-4a20-8a14-cd851ede3ad5" width="400">

**Com toque da pele**  
<img src="https://github.com/user-attachments/assets/6f341fa0-5b25-405f-8ad7-0c2c33bf4516" width="400">

**Pele com hidratante**  
<img src="https://github.com/user-attachments/assets/5c79cd74-7432-4af8-b610-0cdad731db5a" width="400">

**Pele molhada**  
<img src="https://github.com/user-attachments/assets/4e9ff4b0-4954-463e-acca-a22753675720" width="400">


Durante os testes práticos com o sensor de hidratação, foram realizadas medições  correspondentes a diferentes condições da pele. Os valores obtidos foram:

| |Tempo de carga em tau (τ) | Tensão (V) |
| -------- | -------- | -------- |
| Sem toque | 54 µs | 2,64 |
| Com toque | 176 µs | 2,56 |
| Pele com hidratante | 440 µs | 2,12 |
| Pele molhada | 452 µs | 1,64 |

Durante os testes com o osciloscópio, foi possível observar variações claras na curva de carga do circuito RC ao se aplicar a pele com diferentes níveis de hidratação sobre os eletrodos. A resposta do circuito seguiu o comportamento teórico, com curvas de subida mais lentas em peles mais hidratadas, confirmando a variação da capacitância em função da umidade.

