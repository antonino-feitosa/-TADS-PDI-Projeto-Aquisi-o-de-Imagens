
# [TADS][PDI] Projeto Contagem de Moedas com Aquisição Controlada

Projeto da disciplina de Processamento Digital de Imagens do curso de Análise e Desenvolvimento de Sistemas da UFRN aplicando técnicas básicas de aquisição, análise de imagens e segmentação por cor.

## Descrição

Deve-se desenvolver e analisar um sistema de contagem automática de moedas utilizando imagens adquiridas pelos alunos, considerando controle do processo de aquisição.

Como objetivos específicos, deve-se:

- comparar três cores diferentes de EVA utilizado como plano de fundo;
- avaliar qual cor produz menor ruído na aquisição;
- verificar estabilidade tonal entre imagens adquiridas;
- implementar um algoritmo de contagem de moeda automática usando técnicas simples;
- avaliar experimentalmente os resultados obtidos.

Espera-se que, ao final do trabalho, os alunos sejam capazes de:

- planejar experimentos de aquisição de imagens;
- identificar fontes de ruído na aquisição;
- avaliar estabilidade de aquisição;
- interpretar variações na aquisição;
- aplicar técnicas básicas de segmentação por cor;
- avaliar empiricamente algoritmos em imagens reais;

## Aquisição

O experimento será dividido em três fases:

1. Selecionar três cores diferentes de EVA. Para cada cor: adquirir 10 imagens em condições de aquisição controladas.
2. Avaliar a estabilidade tonal entre imagens.
    2.1 comparar tonalidades entre imagens diferentes para o EVA de mesma cor.
    2.2 a estabilidade tonal será avaliada pela variação (desvio padrão) das médias dos canais RGB entre as imagens adquiridas.
3. Adquirir imagens com moedas utilizando o fundo selecionado: adquirir 30 imagens contendo moedas em disposições diferentes.
    3.1 variar a quantidade de moedas entre imagens, entre 1 e 10;
    3.2 evitar sobreposição entre as moedas, elas devem estar totalmente visíveis e separadas entre si;
    3.3 manter condições de aquisição controladas;
    3.4 as imagens devem conter apenas moedas sobre o fundo EVA, sem presença de outros objetos.

Neste caso, condições controladas significam manter constantes posição da câmera, distância do objeto, iluminação, resolução e orientação durante a aquisição.

Em todas as aquisições, a imagem deve capturar a área representada pelo EVA, isto é, não deve haver bordas, a imagem corresponde à área do EVA, de modo que as métricas devem ser calculadas considerando todos os pixels da imagem.

Para o experimento, a iluminação deve permanecer idêntica ou o mais estável possível durante aquisição das três cores. Observe que imagens desfocadas ou com iluminação instável podem invalidar o experimento. Além disso, recomenda-se desativar ajustes automáticos da câmera sempre que possível. Quando não for possível desativar ajustes automáticos, isso deve ser informado no relatório.

## Metodologia

Sugere-se os seguintes passos:

1. planejamento das condições de aquisição;
2. para cada cor de EVA:
    - aquisição de 10 imagens;
    - gere uma tabela de resultados com uma entrada para cada imagem:
        - colunas para médias por canal: média(R(imagem)), média(G(imagem)), média(B(imagem)).
        - colunas para desvio padrão por canal: desvio(R(imagem)), desvio(G(imagem)), desvio(B(imagem)).
        - coluna da média do canal R pelo canal G;
        - coluna da média do canal B pelo canal G;
    - estime o ruído do EVA como a soma das médias dos desvios padrão dos canais RGB ao longo das 10 imagens;
        - ruído = média(desvio(R(imagem)) + desvio(G(imagem)) + desvio(B(imagem)));
        - onde a média é calculada sobre as 10 imagens adquiridas;
    - gerar uma imagem em escala de cinza onde cada pixel representa o desvio padrão daquele pixel ao longo das 10 aquisições;
        - intensidade em cada pixel i será: média(desvio(Ri), desvio(Gi), desvio(Bi)) nas 10 imagens;
        - regiões mais claras indicam maior variabilidade entre aquisições e possível instabilidade de captura;
    - apresentar gráficos comparativos entre as três cores de EVA para cada métrica calculada;
3. analise e interpretação da tabela, estabilidade tonal, estimativa do ruído e da imagem de desvio padrão;
4. escolha da cor do EVA para a etapa final, considerando o menor ruído estimado e maior estabilidade tonal;
    - em caso de conflito entre os critérios, justificar a escolha adotada;
5. aquisição das 30 imagens com as moedas em quantidade e posições diferentes;
6. implementação do algoritmo de contagem;
7. analise e comparação da quantidade real com a quantidade encontrada pelo algoritmo.


Para o planejamento das condições de aquisição deve ser reportado o dispositivo utilizado e suas configurações, resolução adotada, tipo de representação das imagens, distância e ângulos estimados de captura, condições de iluminação. Também devem ser informados configurações de ISO, velocidade do obturador, abertura da câmera e configurações adicionais de aquisição. Caso o dispositivo não permita acesso a esses parâmetros, isso deve ser informado no relatório.

Na etapa 2, deve-se analisar se houve ajuste automático de parâmetros da câmera, como brilho, exposição, balanço de branco, etc. Também deve-se analisar a magnitude e estabilidade do ruído observado e a estabilidade tonal. Observe que o desvio padrão medido inclui ruído do sensor e variações da textura do material, pois ele não é totalmente uniforme.

As razões R/G e B/G no item 2 permitem detectar possíveis ajustes automáticos de balanço de branco entre imagens, indicado pela variação dos valores entre as imagens.

A solução deve ser desenvolvida na linguagem Python. Devem ser utilizadas apenas bibliotecas básicas como OpenCV, numpy e matplotlib e não devem ser utilizados métodos avançados. A estratégia para contagem deve se basear em métodos simples, considerando limiarizações e vizinhança de pixels. A estratégia deve ser explicada e documentada. Ao longo da disciplina, estudaremos técnicas mais adequadas para essa identificação e contagem.

## Entrega

A entrega será realizada via github classroom, assim, é importante que sejam feitos commits regulares no repositório, com comentários descrevendo o que foi feito. Deve conter as imagens adquiridas, o código fonte da aplicação e um arquivo no formato markdown descrevendo o algoritmo e os resultados.

O relatório deve:
- descrever o ambiente experimental e parâmetros utilizados;
- tabela das métricas calculadas;
- discussão da análise e interpretação da tabela (cada coluna e seus valores), estimativa do ruído e da imagem de desvio padrão;
- justificativa para escolha da cor do EVA;
- explicação do algoritmo;
- apresentar exemplos de imagens das etapas utilizadas no processo de contagem: originais, limiarizadas e do resultado final da contagem;
- tabela de resultados finais indicando a quantidade de moedas em cada imagem, a quantidade determinada pelo algoritmo e o erro absoluto;
- determinar o erro médio absoluto do conjunto de imagens;
- discussão dos erros e possíveis melhorias do método.


## Avaliação

A avaliação considerará os itens solicitados na seção de entrega, no entanto, a atribuição da nota é condicionada à comprovação da autoria por meio de perguntas durante a apresentação, em que poderão ser solicitadas explicações, justificativas e modificações no código apresentado.

Desse modo, haverá apresentação oral obrigatória no dia 6 de abril.

## Prazo

O trabalho deve ser finalizado até o final do dia 4 de abril. Após essa data, vocês não terão permissão de escrita no github.

Não serão aceitas submissões por outros meios.

O prazo não será prorrogado.