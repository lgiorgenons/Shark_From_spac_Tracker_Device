# Projeto: Sharks from Space - NASA Space Apps 2025

## 1. Visão Geral do Projeto

Este projeto é uma resposta ao desafio "Sharks from Space" do NASA Space Apps 2025. O objetivo é duplo:

1.  **Criar um framework matemático** para identificar e prever os habitats de forrageamento de tubarões utilizando dados de satélite da NASA.
2.  **Propor um modelo conceitual de uma *tag* inovadora** que possa monitorar não apenas a localização dos tubarões, mas também seus padrões de alimentação, transmitindo esses dados em tempo real.

Este documento foca na segunda parte do desafio: a concepção da *tag* inovadora.

## 2. A *Tag* Inovadora: Detecção Acústica de Alimentação

A nossa solução proposta é uma *tag* de tubarão que utiliza a detecção acústica para identificar quando um tubarão está se alimentando.

### 2.1. Conceito

A *tag* será equipada com um hidrofone (microfone subaquático) para capturar os sons do ambiente do tubarão. Um microcontrolador embarcado analisará esses sons em tempo real usando uma **Transformada Rápida de Fourier (FFT)** para identificar a "assinatura" acústica única de um evento de alimentação (por exemplo, o som de uma mordida).

Um modelo de aprendizado de máquina pré-treinado classificará os sons capturados como "alimentação" ou "não alimentação". Quando um evento de alimentação for detectado, a *tag* transmitirá essa informação, juntamente com a localização GPS do tubarão, para uma estação base ou diretamente via satélite.

### 2.2. Componentes da *Tag*

| Componente | Especificação Sugerida | Justificativa |
| --- | --- | --- |
| **Hidrofone** | Piezoelétrico de banda larga com alta sensibilidade em baixas frequências (< 2 kHz). | Os sons de interesse (alimentação, presas) ocorrem em baixas frequências. |
| **Microcontrolador** | Com capacidade de Processamento de Sinal Digital (DSP). | Para executar a FFT e os algoritmos de classificação em tempo real. |
| **Memória** | Memória flash. | Para armazenar o modelo de classificação e amostras de áudio. |
| **Comunicação** | Módulo de baixa potência (ex: LoRaWAN ou satélite). | Para a transmissão dos dados de alimentação em tempo real. |
| **Bateria** | Longa duração, otimizada para baixo consumo de energia. | Para maximizar o tempo de vida da *tag* no ambiente marinho. |
| **GPS** | Módulo de GPS. | Para registrar a localização do tubarão durante os eventos de alimentação. |

### 2.3. Fluxo de Trabalho

1.  **Captura Contínua:** O hidrofone grava o som ambiente.
2.  **Análise FFT:** O microcontrolador aplica a FFT ao sinal de áudio.
3.  **Extração de Características:** São extraídas características do espectrograma resultante.
4.  **Classificação:** Um modelo de aprendizado de máquina classifica o evento.
5.  **Transmissão:** Se for um evento de alimentação, a *tag* transmite os dados.

## 3. Viabilidade e Desafios

### 3.1. Viabilidade

A proposta é tecnicamente viável. A tecnologia necessária existe e estudos anteriores já validaram a capacidade de gravar sons de alimentação de tubarões com *tags* implantadas.

### 3.2. Desafios

O principal desafio é a **falta de um *dataset* público de sons de alimentação de tubarões**. Este *dataset* é crucial para treinar o modelo de aprendizado de máquina.

**Soluções Propostas:**

*   **Colaboração:** Buscar parcerias com pesquisadores que possuam dados acústicos de tubarões.
*   **Gravação em Cativeiro:** Realizar gravações de alimentação de tubarões em aquários ou centros de pesquisa.

## 4. Próximos Passos

1.  **Desenvolvimento do Protótipo:** Construir um protótipo da *tag* com os componentes listados.
2.  **Coleta de Dados:** Iniciar a coleta de dados acústicos para treinar o modelo.
3.  **Treinamento do Modelo:** Desenvolver e treinar o modelo de classificação.
4.  **Testes e Validação:** Testar a *tag* em ambientes controlados e, posteriormente, em campo.

## 5. Documentos de Referência

*   Análise de Estudos e Datasets Disponíveis para o Projeto.md
*   Análise dos Documentos Fornecidos.md
*   Investigação de Padrões de Alimentação de Tubarões e Detecção Acústica.md
*   Pesquisa sobre Tecnologias FFT e Monitoramento Acústico Subaquático.md
*   Relatório e Recomendações\_ Desafio NASA Space Apps 2025 - Sharks from Space.md
*   UltrasonicShark-tagLocatorSystemforIVER2AUV.pdf
