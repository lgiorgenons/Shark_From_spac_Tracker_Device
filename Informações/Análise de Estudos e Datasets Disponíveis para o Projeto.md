# Análise de Estudos e Datasets Disponíveis para o Projeto

## Desafios na Obtenção de Datasets de Sons de Alimentação de Tubarões

A busca por *datasets* públicos e diretamente focados em sons de alimentação de tubarões revelou que tais recursos são escassos. No entanto, a pesquisa identificou estudos e fontes que confirmam a existência e a possibilidade de gravação desses sons, o que é crucial para a validação da ideia da *tag*.

## Estudos Relevantes e Fontes de Dados Potenciais

1.  **"Implanted Tags Record Acoustic Environment of Sharks" e "Use of an implanted sound recording device (Bioacoustic Probe) to document the acoustic environment of a blacktip reef shark (Carcharhinus melanopterus)" [Webpage 4, Scholar 6]:**
    *   Estes estudos são altamente relevantes, pois afirmam explicitamente que uma *tag* implantada em um tubarão-galha-preta (*Carcharhinus melanopterus*) registrou com sucesso o "som da alimentação do tubarão".
    *   Embora o *dataset* bruto não esteja diretamente disponível nas páginas, a existência dessa gravação valida a premissa de que os sons de alimentação são detectáveis e podem ser isolados.
    *   **Implicação para o Projeto:** Sugere que a coleta de dados primários, possivelmente através de colaborações com pesquisadores que utilizam *tags* bioacústicas, será fundamental para construir um *dataset* de treinamento.

2.  **"Evidence of active sound production by a shark" [Webpage 1, Webpage 6]:**
    *   Este estudo, e seu *dataset* associado no Figshare, foca na produção ativa de sons por uma espécie de tubarão (*Mustelus lenticulatus*) quando manuseado.
    *   Embora não seja diretamente sobre sons de alimentação, o *dataset* pode conter gravações acústicas de tubarões em diferentes contextos, o que pode ser útil para entender o "ruído" de fundo ou outros sons produzidos por tubarões.
    *   **Implicação para o Projeto:** Pode servir como um ponto de partida para análise de sons relacionados a tubarões, mesmo que não sejam de alimentação. A metodologia de coleta e análise pode ser replicada.

3.  **Repositórios de Dados Acústicos Subaquáticos [Webpage 12, Webpage 14]:**
    *   O "Passive Acoustic Data | National Centers for Environmental Information (NOAA)" e "Open Access Underwater Acoustics Data" são repositórios gerais de dados acústicos subaquáticos.
    *   Eles contêm sons de mamíferos marinhos, peixes e embarcações. Embora não específicos para alimentação de tubarões, podem ser úteis para construir um *dataset* de "não-alimentação" ou para entender o ambiente acústico marinho geral.
    *   **Implicação para o Projeto:** Podem fornecer dados para treinar modelos a distinguir sons de alimentação de outros sons ambientais.

4.  **Estudos sobre Classificação de Comportamento de Tubarões [Scholar 1, Scholar 2]:**
    *   Artigos como "Feature extraction, selection, and K-nearest neighbors algorithm for shark behavior classification based on imbalanced dataset" e "Classification of shark behaviors using K-nearest neighbors" discutem a classificação de comportamentos de tubarões, incluindo alimentação, usando dados de sensores.
    *   Eles destacam o desafio de *datasets* desbalanceados, onde os eventos de alimentação são menos frequentes, e sugerem técnicas como *oversampling*.
    *   **Implicação para o Projeto:** Fornecem *insights* sobre as metodologias de classificação e os desafios de *datasets* para o reconhecimento de padrões de alimentação.

## Recomendações para a Coleta e Análise de Dados

*   **Colaboração com Pesquisadores:** Dada a escassez de *datasets* públicos específicos, uma abordagem eficaz seria buscar colaboração com pesquisadores que já utilizam *tags* bioacústicas em tubarões. Eles podem ter dados brutos de áudio que poderiam ser analisados.
*   **Gravação Controlada:** Se a colaboração não for viável, a gravação de sons de alimentação em ambientes controlados (ex: aquários com tubarões) pode ser uma alternativa para criar um *dataset* inicial.
*   **Análise Espectrográfica:** Utilizar espectrogramas (representações visuais da FFT ao longo do tempo) para identificar visualmente as "assinaturas" dos sons de alimentação. Isso ajudaria na rotulagem manual dos dados e na compreensão das características acústicas.
*   **Técnicas de Machine Learning:** Empregar algoritmos de aprendizado de máquina (SVM, Redes Neurais, Random Forest) para classificar os eventos de alimentação. A atenção deve ser dada ao tratamento de *datasets* desbalanceados.

Esta fase de pesquisa reforça a viabilidade da ideia, mas também destaca a necessidade de um esforço concentrado na aquisição e preparação de dados acústicos de alimentação de tubarões para o treinamento de modelos de reconhecimento de padrões.
