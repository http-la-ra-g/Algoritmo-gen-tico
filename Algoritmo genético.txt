
# Algoritmo Genético para Regressão Linear

# Limpando o ambiente
rm(list=ls())

# Funções auxiliares

# Função de fitness (erro quadrático)
fitness <- function(b0, b1, dados) {
  erro <- sum(((dados[, 2]) - (b0 + b1 * dados[, 1]))^2)
  return(erro)
}

# Parâmetros do algoritmo
# Limites dos parâmetros
li <- -7  # limite inferior
ls <- 7   # limite superior

# Parâmetros da população
tam_pop <- 48      # tamanho da população arbritário
num_selecao <- 10  # número de indivíduos selecionados arbritário
num_geracoes <- 30 # número de gerações arbritário
itera <- 1000      # número de iterações por geração arbritário

# Importação dos dados
dados <- read.table("dados.txt", header = TRUE, dec = ",")

# Inicialização da população

# Matriz população
mpop <- matrix(nrow = tam_pop, ncol = 3, 0)
mpop[1:tam_pop, 1] <- runif(tam_pop, li, ls)  # b0
mpop[1:tam_pop, 2] <- runif(tam_pop, li, ls)  # b1

# Matrizes auxiliares
msel <- matrix(nrow = num_selecao, ncol = 3, 0)
mfilho <- matrix(nrow = num_selecao, ncol = 3, 0)

# Cálculo inicial do fitness
for (i in 1:tam_pop) {
  mpop[i, 3] <- fitness(mpop[i, 1], mpop[i, 2], dados)
}

# Execução do algoritmo
resultado_AG <- matrix(nrow = num_geracoes, ncol = 3, 0)

for (geracao in 1:num_geracoes) {
  # Ordenando população pelo fitness
  mpop[1:tam_pop,] <- mpop[order(mpop[1:tam_pop, 3]),]
  resultado_AG[geracao,] <- mpop[1,]
  
  for(j in 1:itera) {
    # Seleção por Torneio
    vetor_numerico <- 1:tam_pop
    msel <- matrix(nrow = num_selecao, ncol = 3, 0)
    
    for (i in 1:num_selecao) {
      selecionados <- sample(vetor_numerico, 2, replace = FALSE)
      ind1 <- selecionados[1]
      ind2 <- selecionados[2]
      
      vetor_numerico <- setdiff(vetor_numerico, selecionados)
      
      msel[i, ] <- if(mpop[ind1, 3] < mpop[ind2, 3]) mpop[ind1, ] else mpop[ind2,]
    }
    
    # Crossover
    for (i in seq(1, num_selecao, by = 2)) {
      pai1 <- msel[i, ]
      pai2 <- msel[i + 1, ]
      
      coluna_selecionada <- sample(1:2, 1)
      
      filho1 <- pai1
      filho2 <- pai2
      
      filho1[coluna_selecionada] <- pai2[coluna_selecionada]
      filho2[coluna_selecionada] <- pai1[coluna_selecionada]
      
      filho1[3] <- fitness(filho1[1], filho1[2], dados)
      filho2[3] <- fitness(filho2[1], filho2[2], dados)
      
      mfilho[i, ] <- filho1
      mfilho[i + 1,] <- filho2
    }
    
 
    # Mutação

    l <- sample(1:nrow(mfilho), 1)
    filho <- mfilho[l,]
    
    coluna_selecionada <- sample(1:2, 1)
    filho[coluna_selecionada] <- runif(1, li, ls)
    filho[3] <- fitness(filho[1], filho[2], dados)
    
    mfilho[l, ] <- filho
    
    # Atualização da população
    mpop <- rbind(mpop[1:tam_pop,], mfilho)
    mpop <- mpop[order(mpop[,3]),][1:tam_pop,]
  }
}

# Resultados

# Melhor solução encontrada
cat("Melhor solução:\n")
cat("b0 =", resultado_AG[num_geracoes, 1], "\n")
cat("b1 =", resultado_AG[num_geracoes, 2], "\n")
cat("Erro =", resultado_AG[num_geracoes, 3], "\n")

# Plot da evolução do erro
plot(1:num_geracoes, resultado_AG[,3], 
     type = "l", 
     xlab = "Geração", 
     ylab = "Erro",
     main = "Evolução do Erro ao Longo das Gerações") 