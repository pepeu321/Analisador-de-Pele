## Imagem 2D do Analisador de Pele

![Imagem2D](https://github.com/user-attachments/assets/110d4ac4-fe19-4196-917a-9bceb9a0caa4)

O protótipo do analisador de pele consiste na criação de uma case portátil, com espaço interno para acomodar a placa contendo o microcontrolador (MSP430G2553) e a conexão com os dois sensores desenvolvidos: o sensor de oleosidade e o sensor de hidratação.

Como o objetivo do projeto é realizar medidas simultâneas dos dois parâmetros, os sensores foram posicionados em áreas separadas para garantir o melhor funcionamento de cada um. O sensor de oleosidade, que utiliza um fototransistor, necessita de uma pequena distância em relação à pele para captar corretamente a luz refletida. Por isso, ele é instalado na parte inferior da case, sem contato direto com a pele, evitando interferência na leitura da reflexão luminosa.

Já o sensor de hidratação, baseado em um circuito RC com eletrodos paralelos, exige contato direto com a pele. Isso é necessário porque a hidratação da pele influencia diretamente a impedância do circuito. Com o contato direto, o circuito é capaz de detectar com maior precisão as variações que indicam o nível de umidade presente na pele.

A parte externa do dispositivo conta com um display LCD, onde o microcontrolador exibe, em tempo real, os valores em porcentagem de oleosidade e hidratação, permitindo uma leitura rápida e prática para o usuário.
