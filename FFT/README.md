# Análise Acústica para Detecção de Assinatura Sonora

## Objetivo do Projeto

O objetivo deste projeto é localizar a ocorrência de um som específico (a "assinatura" em `assinatura.wav`) dentro de um arquivo de áudio mais longo e ruidoso (`final track.wav`). O processo foi refinado através de várias metodologias para encontrar a abordagem mais robusta e eficiente.

---

## Metodologia Final

Após explorar diferentes técnicas, incluindo a detecção de picos de energia em espectrogramas, concluímos que o método mais eficaz para este caso específico é a **Correlação Cruzada com Filtragem**.

O fluxo de trabalho do script final é o seguinte:

1.  **Carregamento dos Áudios:** O script carrega o áudio principal (`final track.wav`) e o áudio da assinatura (`assinatura.wav`).
2.  **Filtragem Passa-Banda:** Um filtro Butterworth é aplicado ao áudio principal para isolar a faixa de frequência onde a assinatura tem mais energia (determinado através de análise prévia como **43 Hz - 1464 Hz**). Isso reduz ruídos irrelevantes.
3.  **Correlação Cruzada:** O algoritmo então "desliza" a assinatura sobre o áudio principal já filtrado e calcula a semelhança entre os padrões em cada ponto. Este método é ideal para encontrar padrões sutis que não se destacam apenas pela energia.
4.  **Detecção de Picos:** O script identifica os pontos onde a correlação ultrapassa um limiar de 60%, marcando-os como detecções válidas.
5.  **Visualização:** O resultado é salvo em uma imagem (`final_analysis_results.png`) contendo dois gráficos para fácil interpretação.

---

## Estrutura de Pastas

-   `/songs`: Contém os arquivos de áudio originais (`final track.wav`, `assinatura.wav`).
-   `/scripts`: Contém o script de análise final.
-   `/data`: Armazena áudios processados (atualmente vazio, mas pode ser usado no futuro).

---

## Como Executar a Análise

1.  Navegue até a pasta do projeto no seu terminal.
2.  Execute o script principal usando o seguinte comando:

    ```sh
    C:\Users\lucas\OneDrive\Documentos\Projetos\Nasa_space_apps\Tubaroes_do_Espaco\.venv\Scripts\python.exe C:\Users\lucas\OneDrive\Documentos\Projetos\Nasa_space_apps\Devices\FFT\scripts\run_correlation_analysis.py
    ```

---

## Saída Esperada

A execução do script irá gerar um arquivo de imagem na pasta `FFT/` chamado `final_analysis_results.png`.

-   **Gráfico de Cima (Cross-Correlation Result):** Mostra a força da correlação ao longo do tempo. Os picos marcados com "x" vermelho indicam os momentos exatos onde o padrão da assinatura foi encontrado.
-   **Gráfico de Baixo (Original Spectrogram):** Mostra o espectrograma do áudio original, com retângulos vermelhos destacando visualmente a localização dos eventos detectados.
