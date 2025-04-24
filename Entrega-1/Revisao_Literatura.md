# Revisão de Literatura

O projeto propõe o desenvolvimento de um analisador eletrônico portátil de pele, com foco na medição de hidratação e oleosidade, utilizando o microcontrolador MSP430xxxx. A proposta visa preencher uma lacuna existente no acesso a ferramentas acessíveis e objetivas de diagnóstico da pele, substituindo dispositivos de alto custo como Corneometer® e Sebumeter®. O produto permitirá o acompanhamento da saúde da pele de forma prática, com potencial aplicação clínica e cosmética.

## 1. Sensores Comerciais de Oleosidade e Hidratação:
Segundo Oliveira et al. (2023), o conhecimento preciso do tipo de pele é fundamental para a escolha de produtos cosméticos e procedimentos dermatológicos adequados. Equipamentos como o Corneometer®, que mede capacitância da pele para avaliar hidratação, e o Sebumeter®, que analisa a transparência de uma fita para quantificar a oleosidade, são amplamente reconhecidos no mercado, mas inacessíveis ao público pelo seu alto custo. 

## 3. Aplicação de Fotodiodos em Sensores de Pele:
Os fotodiodos, segundo a DigiKey (s.d.), são componentes sensíveis à luz capazes de detectar variações mínimas na intensidade da luz refletida ou absorvida. Quando combinados a uma fonte de luz controlada, permitem inferir propriedades da pele com base na refletância óptica — característica diretamente influenciada pela oleosidade e hidratação. Essa abordagem é vantajosa por ser não invasiva, de baixo custo e fácil integração em sistemas embarcados.

## 4. Circuito RC e Caracterização Elétrica da Pele: 
A resposta elétrica da pele também pode ser analisada através de circuitos RC, os quais permitem medir variações de capacitância e condutância superficial. Essas propriedades estão diretamente associadas ao conteúdo hídrico e à presença de lipídios na pele. O tempo de carga/descarga do circuito RC fornece um parâmetro indireto da composição da pele, complementando os dados ópticos captados pelo fotodiodo.

## 5. Interface com Usuário:
O usuário irá ver os dados por meio de um LCD, onde serão mostrados valores medidos de hidratação e oleosidade e mensagens de feedback em relação à pele. Além do display, LEDs de diferentes cores irão sinalizar o de acordo com o resultado da medição, como um LED verde para quando estiver com a pele boa, um LED amarelo para uma pele intermediaria e um vermelho para ruim, um buzzer também sinalizará quando a medição começar e terminar e por fim um botão para começar a medição.
