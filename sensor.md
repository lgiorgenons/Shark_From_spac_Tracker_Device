# B-AMPT: Bio-Acoustic Motion and Profiling Tag

## 1. Resumo

A B-AMPT (Tag de Bio-Acústica, Movimento e Perfilamento) é um dispositivo de biologging não invasivo projetado para ser acoplado a grandes espécies marinhas, como tubarões. O objetivo principal da tag é identificar e registrar eventos de alimentação em tempo real através de uma metodologia de fusão de sensores, combinando dados acústicos, de movimento e ambientais. Os dados coletados servem como "verdade de campo" para validar e aprimorar modelos de previsão de habitat baseados em dados de satélite.

---

## 2. Componentes de Hardware

A tag integra um conjunto de sensores de baixo consumo para construir um perfil comportamental completo do animal.

-   **Hidrofone de Alta Sensibilidade:** O sensor primário, responsável por capturar um amplo espectro de sons do ambiente subaquático. É o componente chave para a detecção da assinatura acústica de um evento de alimentação.

-   **Acelerômetro de 3 Eixos:** Mede a aceleração dinâmica e a orientação estática do animal. É fundamental para identificar padrões de movimento bruscos, como ataques, mordidas e arrancadas, que são característicos da alimentação.

-   **Sensor de Temperatura e Pressão:** Coleta dados contextuais do ambiente. O sensor de pressão é usado para determinar a profundidade, enquanto o de temperatura registra as condições da coluna de água. Juntos, eles ajudam a construir um perfil do habitat onde a alimentação ocorre.

-   **Unidade de Microprocessamento (MCU):** O "cérebro" da tag. Um microcontrolador de baixo consumo responsável por executar o algoritmo de detecção, gerenciar a coleta de dados e controlar o estado dos sensores para economizar energia.

-   **Módulo de Armazenamento:** Uma memória flash não volátil para armazenar os dados dos eventos detectados para recuperação posterior.

-   **Bateria e Gerenciamento de Energia:** Fonte de alimentação otimizada para missões de longa duração, com um sistema que coloca os sensores em estado de baixo consumo quando nenhum evento de interesse está ocorrendo.

---

## 3. Metodologia de Detecção e Algoritmo

A detecção de um evento de alimentação é um processo de múltiplos estágios projetado para maximizar a precisão e minimizar falsos positivos. O algoritmo é baseado no protótipo desenvolvido (`run_correlation_analysis.py`).

#### Estágio 1: Análise Acústica e Filtragem
-   O áudio capturado pelo hidrofone é continuamente analisado.
-   Um **filtro passa-banda digital**, baseado na análise de frequência (FFT/PSD) de assinaturas de alimentação conhecidas, é aplicado para isolar a faixa de frequência mais relevante (ex: 43 Hz - 1464 Hz, como determinado em nossos testes).

#### Estágio 2: Detecção de Padrão por Correlação Cruzada
-   Este é o núcleo da detecção acústica. O script utiliza um algoritmo de **Correlação Cruzada** (`np.correlate`) para comparar o áudio filtrado com um padrão de assinatura pré-carregado na memória da tag.
-   Este método se provou mais robusto que a simples detecção de picos de energia, pois ele busca a "forma de onda" ou o padrão temporal exato do som, sendo eficaz mesmo para eventos sutis.
-   Quando a correlação ultrapassa um limiar pré-definido (ex: 65%), um "evento acústico candidato" é registrado.

#### Estágio 3: Análise de Movimento
-   Paralelamente, o MCU monitora os dados do acelerômetro.
-   O algoritmo é treinado para reconhecer "padrões de movimento" associados à alimentação, como um pico súbito de aceleração ou uma mudança brusca de orientação.

#### Estágio 4: Fusão de Sensores e Validação do Evento
-   A etapa final para confirmar uma alimentação. Um evento só é validado e registrado como "alimentação de alta confiança" se:
    > **Evento Acústico Candidato** (do Estágio 2) + **Padrão de Movimento Compatível** (do Estágio 3) ocorrem dentro da mesma janela de tempo.
-   Quando um evento é validado, a tag registra o som, os dados de movimento e os dados ambientais (temperatura e profundidade) daquele momento.

---

## 4. Fluxo de Dados e Otimização de Energia

Para maximizar a vida útil da bateria, a tag opera em um modo de "escuta" de baixo consumo. A análise completa de correlação e movimento só é ativada quando um pico de energia preliminar no áudio ou um movimento anômalo é detectado. Apenas os eventos de alimentação validados são armazenados em detalhe, economizando espaço de memória e energia.