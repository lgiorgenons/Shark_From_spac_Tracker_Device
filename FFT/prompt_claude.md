## Prompt para Colar no Claude

(Copie e cole todo o texto abaixo na sua conversa com o Claude e anexe a imagem `comparative_analysis.png`)

---

**Assunto:** Análise de Espectrograma de Áudio para Detecção de Sinal

Olá, Claude. Preciso da sua ajuda para interpretar a imagem em anexo, que contém uma análise de dois arquivos de áudio.

**Contexto do Projeto:**
O objetivo é encontrar um som específico (chamado de "Assinatura" ou "Signature") dentro de uma faixa de áudio mais longa e com ruído (chamada de "Faixa Final" ou "Final Track"). A imagem mostra uma análise comparativa dos dois sons.

**Minha Pergunta:**

Com base na imagem em anexo, por favor, faça o seguinte:

1.  **Analise o gráfico no canto inferior direito ("Signature - Power Spectral Density").** Qual é a faixa de frequência (em Hz, no eixo X) onde a linha laranja mostra a maior concentração de energia? Por favor, me dê um valor aproximado para a frequência mínima e máxima desta faixa principal.

2.  **Analise o gráfico no meio à esquerda ("Final Track - Spectrogram").** Usando a faixa de frequência que você identificou no passo 1, em quais momentos (em segundos, no eixo X) você consegue ver uma "mancha" ou "burst" de energia mais brilhante que corresponda a essa mesma faixa de frequência?

Preciso dessa informação para construir um filtro de áudio e continuar meu projeto. Obrigado!

---

## Meu Questionamento (Explicação para você)

Eu formulei o prompt acima para ser o mais direto possível e guiar o Claude a te dar a resposta exata que precisamos para o próximo passo técnico. 

- **Pergunta 1 (Analisar a Assinatura):** Esta pergunta força o Claude a fazer o que eu pedi para você anteriormente: encontrar a "impressão digital" de frequência do som que queremos. A resposta dele será a faixa de frequência que usaremos para criar nosso filtro (por exemplo, "a faixa principal parece ser de 400 Hz a 1500 Hz").

- **Pergunta 2 (Encontrar a Assinatura no Áudio Principal):** Esta pergunta pede ao Claude para atuar como um "detector visual". Ele vai pegar a resposta da primeira pergunta e procurar por aquele padrão de frequência no espectrograma do áudio completo. A resposta dele nos dará uma estimativa de onde o som do "pão de queijo" está localizado no tempo, o que nos ajudará a validar os resultados do nosso próprio script de detecção no futuro.

Com as respostas do Claude, teremos os parâmetros exatos para construir o algoritmo final.