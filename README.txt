==============================================
ALGORITMO GENÉTICO PARA REGRESSÃO LINEAR
==============================================

DESCRIÇÃO
---------
Este algoritmo genético foi desenvolvido para encontrar os coeficientes (β0 e β1) de uma regressão linear simples que relaciona altura de árvores em função da idade. O modelo busca minimizar a soma dos erros quadráticos entre os valores observados e preditos.

MODELO
------
hd = β0 + β1 * I

PARÂMETROS DO ALGORITMO
----------------------
- População: 48 indivíduos (arbritário) 
- Gerações: 30 (arbritário)
- Iterações por geração: 1000 (arbritário)
- Limite dos parâmetros: -7 a 7 (arbritário)
- Seleção: Torneio com 10 indivíduos (arbritário)
- Operadores: Crossover e Mutação

ESTRUTURA DOS DADOS
------------------
O arquivo "dados.txt" deve conter duas colunas:
- Coluna 1: Altura
- Coluna 2: Idade
Obs: Use vírgula como separador decimal

FUNCIONAMENTO
------------
1. Inicialização: Cria população aleatória de soluções
2. Avaliação: Calcula o erro quadrático para cada solução
3. Seleção: Escolhe as melhores soluções por torneio
4. Crossover: Combina soluções para gerar novos indivíduos
5. Mutação: Aplica mudanças aleatórias para manter diversidade
6. Repetição: Processo se repete por 30 gerações (arbritário)

RESULTADOS
----------
O algoritmo retorna:
- Melhor β0 encontrado
- Melhor β1 encontrado
- Erro quadrático da melhor solução
- Gráfico da evolução do erro ao longo das gerações

COMO USAR
---------
1. Prepare seu arquivo "dados.txt" com as colunas idade e altura
2. Coloque o arquivo de dados no mesmo diretório do script
3. Execute o script no R
4. Os resultados serão exibidos no console e um gráfico será gerado

REQUISITOS
----------
- R instalado
- Arquivo de dados no formato correto
- Permissões de leitura/escrita no diretório

OBSERVAÇÕES
-----------
- O algoritmo pode ser adaptado para outros tipos de regressão
- Os parâmetros podem ser ajustados conforme necessidade
- Recomenda-se múltiplas execuções para verificar a consistência dos resultados 