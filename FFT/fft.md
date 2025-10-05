# Resumo da Análise Acústica com FFT

## Objetivo
O objetivo desta análise foi detectar uma assinatura de áudio específica (o som de uma mordida, simulado comendo um pão de queijo) dentro de um arquivo de áudio mais longo e ruidoso (`final track.wav`), utilizando técnicas de processamento de sinais em Python.

## Processo e Descobertas

### 1. Análise Inicial e Detecção por Correlação
- **Ação:** A primeira tentativa de detecção foi feita usando a **Correlação Cruzada** entre o áudio principal (`final track.wav`) e a assinatura (`assinatura.wav`).
- **Resultado:** Sucesso. Encontramos **1 correspondência** em aproximadamente **2.05 segundos**. Isso provou que a detecção era viável.

### 2. Tentativa de Filtragem por Baixa Frequência
- **Ação:** Para tentar melhorar o resultado e reduzir o ruído, analisamos o espectro de frequência da assinatura. A análise revelou um pico de energia em **49 Hz**. Com base nisso, projetamos um filtro passa-banda (20-200 Hz) para isolar os sons graves.
- **Resultado:** Falha. Ao aplicar a correlação no áudio filtrado, **nenhuma correspondência foi encontrada**.
- **Conclusão:** A característica principal da assinatura não estava nos sons graves. O pico em 49 Hz era provavelmente um ruído de fundo comum a ambos os arquivos, e o filtro acabou removendo as frequências que realmente importavam.

### 3. Tentativa de Filtragem por Média Frequência (Refinamento)
- **Ação:** Com base na conclusão anterior, levantamos a hipótese de que as características da assinatura estariam nas frequências médias. Projetamos um novo filtro passa-banda na faixa de **300 Hz a 3000 Hz**.
- **Resultado:** **Sucesso total.** Ao aplicar a correlação no novo áudio filtrado:
  - Encontramos **2 correspondências** claras em **1.95s** e **3.39s**.
  - A primeira detecção foi consistente com a análise inicial, e a segunda foi uma nova descoberta que antes estava mascarada pelo ruído.

### 4. Visualização Final
- Para consolidar os resultados, geramos um espectrograma do áudio original com as duas detecções marcadas por retângulos vermelhos, e um segundo espectrograma mostrando todo o ruído que foi efetivamente removido pelo filtro.

## Conclusão Final
O processo iterativo de análise e filtragem foi crucial. A combinação da **Análise de Frequência (FFT)** para projetar um filtro eficaz e da **Correlação Cruzada** para a detecção precisa do padrão se provou uma estratégia robusta e bem-sucedida para encontrar a assinatura desejada.
