# B-AMPT: Bio-Acoustic Motion and Profiling Tag

*Versão 2.0 - Modelo Conceitual*

## 1. Resumo

A B-AMPT (Tag de Bio-Acústica, Movimento e Perfilamento) é um dispositivo de biologging conceitual, não invasivo, projetado para ser acoplado a grandes espécies marinhas. O objetivo da tag é identificar e transmitir dados sobre eventos de alimentação em tempo real. A metodologia se baseia na fusão de dados de múltiplos sensores para validar um evento, focando na detecção de uma assinatura acústica seguida por um período de baixa atividade motora, inferindo um ciclo de caça e saciedade.

---

## 2. Componentes de Hardware (Conceitual)

-   **Hidrofone de Alta Sensibilidade:** O sensor primário para capturar o áudio do ambiente, essencial para a detecção da assinatura acústica da alimentação.

-   **Acelerômetro de 3 Eixos:** Com uma nova função estratégica, este sensor monitora os níveis de atividade do tubarão. Sua principal finalidade no conceito atual é **detectar períodos de baixa atividade (movimento lento e estável)**, que, ocorrendo após um evento acústico, podem inferir um estado de saciedade e digestão.

-   **Sensor de Temperatura e Pressão:** Coleta dados ambientais essenciais (temperatura da água e profundidade) para contextualizar o comportamento de caça e validar os modelos de previsão de habitat.

-   **Unidade de Microprocessamento (MCU):** O cérebro da tag. A arquitetura é baseada em um MCU de baixíssimo consumo da **linha NXP MCX**. Estes processadores são ideais por seu baixo gasto energético em modo de espera e poder de processamento suficiente para executar os algoritmos de FFT e correlação em "bursts" quando um som candidato é detectado.

-   **Módulo de Comunicação (Modem Ultrassônico):** Responsável pela transmissão de dados debaixo d'água. A comunicação via rádio (como LoRa) é ineficaz na água salgada, tornando o ultrassom a escolha ideal.

-   **Bateria e Gerenciamento de Energia:** Fonte de energia de longa duração, provavelmente baseada em células de Lítio-Tion, com um sistema de gerenciamento avançado que mantém a tag em estado de "sono profundo" a maior parte do tempo.

---

## 3. Metodologia de Detecção (Fluxo Lógico)

1.  **Modo de Escuta:** A tag opera em um modo de baixíssimo consumo, com o hidrofone amostrando o áudio em intervalos ou de forma contínua com um limiar de energia muito baixo.
2.  **Ativação por Som:** Ao detectar um som que ultrapassa um limiar de energia na faixa de frequência de interesse (ex: 43-1464 Hz), o MCU é "acordado" e inicia a análise completa.
3.  **Detecção por Correlação:** O algoritmo principal (`run_correlation_analysis.py`) é executado no trecho de áudio capturado, buscando o padrão da assinatura de alimentação pré-carregada.
4.  **Confirmação pelo Movimento:** Se uma correspondência acústica é encontrada, o MCU começa a monitorar intensivamente os dados do acelerômetro. Se, nos minutos seguintes à detecção acústica, for registrado um período de **baixa atividade motora** (indicando um possível estado de repouso/digestão), o evento é validado como "Ciclo de Alimentação Concluído".
5.  **Transmissão de Dados:** Um pacote de dados consolidado é transmitido via ultrassom.

---

## 4. Arquitetura de Comunicação

A comunicação é projetada em duas etapas para superar as limitações do ambiente marinho.

-   **Etapa 1: Tag para Receptor (Ultrassom)**
    -   **Tecnologia:** A tag utiliza um modem acústico que converte pacotes de dados digitais em pulsos de som de alta frequência (ultrassom).
    -   **Velocidade e Dados:** A comunicação acústica subaquática tem baixa largura de banda. As velocidades típicas variam de **100 a 2000 bits por segundo (aproximadamente 12 a 250 bytes/s)**. Devido a essa limitação, a tag não transmite o áudio bruto, mas sim um **pacote de dados compacto** contendo:
        -   ID da Tag
        -   Timestamp do Evento
        -   Tipo de Evento (ex: Alimentação Confirmada)
        -   Nível de Confiança da Detecção (ex: 85%)
        -   Profundidade e Temperatura no momento do evento.
    -   **Alcance:** O alcance efetivo pode variar de centenas de metros a alguns quilômetros, dependendo da frequência, potência e condições da água (ruído, temperatura, salinidade).

-   **Etapa 2: Receptor para Satélite**
    -   **Conceito:** Receptores acústicos autônomos (boias ou unidades ancoradas no fundo do mar) são posicionados em "hotspots" conhecidos de tubarões.
    -   **Função:** Essas unidades "escutam" os sinais ultrassônicos das tags. Ao receber um pacote de dados, o receptor utiliza seu próprio transmissor de satélite (ex: Iridium, Argos) para retransmitir a informação quase em tempo real para os centros de pesquisa.

---

## 5. Design Físico e Materiais (Conceitual)

-   **Invólucro (Enclosure):** Para suportar a extrema pressão em grandes profundidades, o invólucro é o componente mais crítico. Ele seria construído em **Titânio Grau 5** ou **Cerâmica de Alumina**, materiais conhecidos por sua altíssima resistência à compressão e corrosão. O design seria hidrodinâmico para minimizar o arrasto e o impacto no comportamento do animal.

-   **Proteção Interna:** Todos os componentes eletrônicos, incluindo a **bateria e a placa do MCU**, seriam encapsulados em uma **resina epóxi ou poliuretano** de grau marinho. Este processo, chamado de "potting", preenche todo o espaço vazio, tornando o interior um bloco sólido. Isso impede que os componentes se deformem ou que as soldas se quebrem sob a flexão do invólucro em alta pressão, respondendo à sua dúvida sobre a segurança da bateria e da placa.

-   **Acoplamento:** A tag seria acoplada à barbatana dorsal do tubarão usando um método comprovado e seguro, projetado para se soltar após um período pré-determinado para permitir a recuperação do dispositivo ou minimizar o impacto a longo prazo no animal.