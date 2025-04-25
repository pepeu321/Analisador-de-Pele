# Diagrama de Blocos

## Descrição básica do diagrama de blocos:  
Os sinais serão extraídos diretamente da superfície da pele do usuário, podendo ser coletados em diferentes regiões do rosto ou do corpo. Para a medição da hidratação ou ressecamento, será utilizado um circuito RC. A capacitância do sensor varia conforme o teor de umidade da pele, aumentando em condições de maior hidratação. Um timer interno do microcontrolador da família MSP430 será empregado para medir o tempo que o capacitor leva para atingir uma tensão conhecida, o qual sera diretamente relacionado ao nível de umidade da pele.

A análise da oleosidade será realizada por meio de um fotodiodo sensível à radiação no espectro do infravermelho próximo. A intensidade luminosa refletida varia de acordo com o nível de oleosidade da pele. O sinal gerado será convertido por um conversor analógico digital integrado ao microcontrolador, permitindo a aquisição precisa dos dados analógicos.

Por fim, os valores obtidos de hidratação e oleosidade serão exibidos de forma simultânea em um display LCD. Os resultados serão apresentados em formato percentual (%), facilitando a interpretação dos dados pelo usuário.

#### ![Diagrama de blocos4](https://github.com/user-attachments/assets/ed6b1f71-28f2-44c7-9729-fe29639f3942)

Para facilitar a visualização do protótipo desenvolvido, foi incluída uma referência de produto semelhante disponível no mercado: o analisador digital de pele facial e corporal Skin Analyser, acessível através do link [https://produto.mercadolivre.com.br/MLB-1951446111-skin-up-analisador-limpeza-pele-facial-corporal-oleosidade-_JM?matt_tool=18956390&utm_source=google_shopping&utm_medium=organic]

