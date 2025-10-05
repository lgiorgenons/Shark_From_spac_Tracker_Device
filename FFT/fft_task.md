# Análise Acústica para Detecção de Alimentação de Tubarões (Revisado)

## Resumo da Abordagem
O objetivo é desenvolver um software em Python para analisar o áudio `final track.wav` (o áudio principal) e encontrar eventos de interesse usando um arquivo de amostra, `assinatura.wav` (a assinatura). Para isso, combinaremos duas técnicas principais:
1.  **Análise de Frequência (FFT):** Para visualizar os áudios e projetar um filtro que reduza o ruído de fundo.
2.  **Correlação Cruzada:** Para localizar com precisão os momentos em que a assinatura ocorre no áudio principal.

## Sugestão de Software Python

### 1. Carregar os Arquivos de Áudio
- **Principal:** Carregar o áudio ruidoso de `final track.wav`.
- **Assinatura:** Carregar a amostra de áudio limpa de `assinatura.wav`.

### 2. Análise Visual com Espectrogramas
A geração de espectrogramas separados é o primeiro passo para entender as características de cada áudio.

- **2.1. Espectrograma do Áudio Principal (`final track.wav`)**
  - **O que faz:** Gera uma imagem que mostra as frequências presentes no áudio ao longo do tempo.
  - **Objetivo:** Permite uma inspeção visual de todo o arquivo, ajudando a identificar ruídos constantes (linhas horizontais contínuas) e eventos sonoros distintos (manchas de cor mais intensa).

- **2.2. Espectrograma da Assinatura (`assinatura.wav`)**
  - **O que faz:** Gera a mesma visualização, mas focada apenas no som de interesse.
  - **Objetivo:** Revela a "impressão digital" de frequência da assinatura. Ao analisar este gráfico, podemos ver claramente em qual faixa de frequência (ex: entre 200 Hz e 800 Hz) o som de alimentação tem mais energia.

### 3. Como Usar a Análise FFT para Filtrar Ruído
Com base na análise anterior, podemos projetar um filtro para "limpar" o áudio principal, destacando os sons que se parecem com a assinatura.

- **Passo 1: Analisar o Espectro da Assinatura**
  - Calcule a FFT (Transformada Rápida de Fourier) do áudio da `assinatura.wav`. Isso gera um gráfico que mostra a intensidade de cada frequência.
  - Identifique a faixa de frequência onde a assinatura tem mais energia. Por exemplo, podemos notar que a maior parte do som está concentrada entre uma frequência mínima (F_min) e máxima (F_max).

- **Passo 2: Projetar um Filtro Passa-Banda (Band-pass Filter)**
  - Um filtro passa-banda é um filtro digital que permite que apenas as frequências dentro de um determinado intervalo (no caso, de F_min a F_max) passem, enquanto atenua (reduz o volume) de todas as outras.
  - Usando `scipy.signal`, podemos projetar este filtro com base nas frequências que identificamos no passo anterior.

- **Passo 3: Aplicar o Filtro ao Áudio Principal**
  - Processe o áudio `final track.wav` com o filtro passa-banda. O resultado será um novo áudio, "filtrado", onde os ruídos de fundo (que ocorrem em frequências fora da faixa da assinatura) foram removidos ou reduzidos.

- **Passo 4: Verificar o Resultado**
  - Gere um novo espectrograma, desta vez do áudio *filtrado*. Visualmente, ele deve parecer mais "limpo", com os eventos de interesse mais destacados.

### 4. Detecção Precisa com Correlação Cruzada
Embora a filtragem FFT ajude a limpar o áudio, a melhor técnica para **localizar** o sinal continua sendo a **Correlação Cruzada**.

- **Como funciona:** A correlação "desliza" a `assinatura.wav` sobre o áudio principal (seja o original ou o filtrado) e produz um gráfico de semelhança. Picos altos nesse gráfico indicam uma forte correspondência.
- **Vantagem:** Aplicar a correlação no áudio *filtrado* (do passo 3) pode gerar resultados ainda mais precisos, pois o ruído que poderia causar falsos positivos já foi reduzido.

## Bibliotecas Python Recomendadas
- **`scipy`**: Para carregar arquivos `.wav` (`scipy.io.wavfile`) e, crucialmente, para projetar e aplicar filtros digitais (`scipy.signal`).
- **`numpy`**: Para todos os cálculos numéricos, incluindo a FFT (`numpy.fft`) e a correlação (`numpy.correlate`).
- **`matplotlib`**: Para gerar os espectrogramas e outros gráficos de análise.

## Próximos Passos Sugeridos
1.  **Análise da Assinatura:** Criar um script para gerar e salvar o espectrograma e o gráfico de FFT da `assinatura.wav` para identificar sua faixa de frequência principal.
2.  **Filtragem:** Criar um segundo script que projeta e aplica o filtro passa-banda no `final track.wav` e salva o resultado como `final_track_filtrado.wav`.
3.  **Verificação:** Executar novamente o script de correlação cruzada (`find_signature.py`), mas usando o áudio filtrado como entrada principal, e comparar os resultados.
