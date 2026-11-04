# crispy-memory
# Contador de Pessoas por Zona - YOLO + OpenCV

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python)
![OpenCV](https://img.shields.io/badge/OpenCV-Computer%20Vision-green?logo=opencv)
![YOLO](https://img.shields.io/badge/YOLO-Ultralytics-purple)
![Status](https://img.shields.io/badge/Status-Em%20desenvolvimento-orange)

## Sobre o projeto

Este projeto consiste no desenvolvimento de um sistema de **Visao Computacional capaz de detectar pessoas em videos e identificar se elas estao dentro ou fora de uma regiao delimitada**.

A aplicacao utiliza o modelo YOLO para detectar pessoas e a biblioteca OpenCV para processar os frames, desenhar as regioes de interesse e apresentar os resultados visualmente.

O projeto e uma versao simplificada de um sistema de monitoramento de ocupacao, inspirado em aplicacoes de contagem de pessoas em ambientes, como hoteis.

## Objetivos

- Estudar os fundamentos da Visao Computacional.
- Compreender o funcionamento do YOLO.
- Aplicar deteccao de pessoas em videos.
- Trabalhar com regioes de interesse (ROI).
- Identificar a posicao das pessoas utilizando o ponto do pe.
- Desenvolver um contador de pessoas por zona.
- Praticar Python e processamento de imagens.

## Tecnologias utilizadas

| Tecnologia | Aplicacao no projeto |
|---|---|
| Python | Linguagem de programacao. |
| YOLO (Ultralytics) | Deteccao de pessoas. |
| OpenCV | Processamento de imagens e videos. |
| NumPy | Manipulacao de coordenadas e matrizes. |

## Conceitos de Visao Computacional

### 1. YOLO - Deteccao de objetos

YOLO significa *You Only Look Once*.

E um modelo de Deep Learning utilizado para identificar objetos em imagens e videos.

Neste projeto, o YOLO identifica pessoas e retorna tres informacoes principais:

- **Classe:** categoria do objeto identificado, neste caso, pessoa.
- **Bounding Box:** caixa delimitadora que representa a posicao da pessoa.
- **Confidence:** nivel de confianca estimado pelo modelo na deteccao.

### 2. OpenCV - Processamento de imagens

OpenCV e uma biblioteca utilizada para trabalhar com imagens e videos.

No projeto, e responsavel por:

- Capturar os frames do video.
- Desenhar caixas delimitadoras.
- Criar e desenhar a zona monitorada.
- Calcular e verificar coordenadas.
- Exibir o resultado em tempo real.

### 3. ROI - Regiao de Interesse

ROI significa *Region of Interest*.

E uma area especifica da imagem que sera monitorada pelo sistema.

Neste projeto, a ROI e representada por um poligono que delimita a zona onde queremos contar as pessoas.

A funcao utilizada e:

```python
cv2.pointPolygonTest(poligono, ponto, False)
```

Ela verifica se determinado ponto esta dentro, fora ou na borda do poligono.

### 4. Ponto do pe

O ponto do pe e calculado utilizando as coordenadas da caixa delimitadora da pessoa.

```python
pe_x = int((x1 + x2) / 2)
pe_y = y2
```

Onde:

- `x1` e `y1`: coordenadas superiores da caixa.
- `x2` e `y2`: coordenadas inferiores da caixa.
- `pe_x`: posicao horizontal do ponto do pe.
- `pe_y`: posicao vertical do ponto do pe.

Esse ponto representa aproximadamente onde a pessoa esta apoiada no chao.

Ele e utilizado para verificar se a pessoa esta dentro da regiao monitorada.

## Como funciona o contador?

O programa possui cinco etapas principais:

**1. Conversao da zona para pixels**

As coordenadas proporcionais da regiao sao convertidas para as dimensoes reais do video.

**2. Deteccao de pessoas com YOLO**

O modelo analisa cada frame e identifica as pessoas presentes.

**3. Verificacao do ponto do pe**

O sistema calcula o ponto inferior central da caixa e verifica se ele esta dentro da ROI.

**4. Desenho dos resultados**

O OpenCV desenha as caixas delimitadoras e apresenta a situacao de cada pessoa.

**5. Repeticao para cada frame**

O processo acontece continuamente ate o video terminar ou o usuario encerrar a execucao.

## Interpretacao dos resultados

| Cor | Significado |
|---|---|
| Verde | Pessoa dentro da zona. |
| Vermelho | Pessoa fora da zona. |
| Amarelo | Delimitacao da regiao monitorada. |
| Azul | Ponto do pe utilizado na verificacao. |

O contador apresenta a quantidade de pessoas identificadas dentro da regiao em cada frame.

## Demonstracao do projeto

### Resultado esperado

O sistema deve apresentar:

- Deteccao de pessoas pelo YOLO.
- Caixas delimitadoras coloridas.
- Regiao de interesse delimitada.
- Ponto do pe de cada pessoa.
- Quantidade de pessoas dentro da zona.

### GIF ou video demonstrativo

Apos executar o projeto e gravar uma demonstracao, adicione o arquivo a pasta `docs/imagens_resultado/`.

Exemplo de incorporacao de um GIF:

```markdown
![Demonstracao do contador](docs/imagens_resultado/demo.gif)
```

O GIF demonstrativo sera adicionado apos a gravacao da execucao real do programa.

## Como executar o projeto

### 1. Clonar o repositorio

```bash
git clone https://github.com/SEU-USUARIO/contador-pessoas-yolo.git
```

Entre na pasta:

```bash
cd contador-pessoas-yolo
```

### 2. Criar ambiente virtual

```bash
python -m venv .venv
```

Ativar no Windows:

```bash
.venv\Scripts\activate
```

### 3. Instalar as dependencias

```bash
pip install -r requirements.txt
```

### 4. Adicionar o video

Coloque um video de teste na pasta principal com o nome:

```text
video.mp4
```

### 5. Executar o programa

```bash
python src/contador_pessoas.py
```

O modelo YOLO sera baixado automaticamente na primeira execucao, caso ainda nao esteja disponivel localmente.

Para encerrar a execucao, pressione `ESC`.

## Estrutura do projeto

```text
contador-pessoas-yolo/
|
|-- README.md
|-- requirements.txt
|-- .gitignore
|
|-- src/
|   |-- contador_pessoas.py
|
|-- videos/
|   |-- video.mp4
|
|-- docs/
    |-- imagens_resultado/
        |-- demo.gif
```

## Aprendizados

Durante o desenvolvimento deste projeto, os principais conhecimentos trabalhados foram:

- Fundamentos da Visao Computacional.
- Processamento de imagens com OpenCV.
- Deteccao de objetos utilizando YOLO.
- Manipulacao de coordenadas e matrizes.
- Criacao de regioes de interesse (ROI).
- Segmentacao e analise de imagens.
- Processamento de videos por frames.
- Desenvolvimento de aplicacoes utilizando Python.

## Proximas melhorias

- [ ] Implementar rastreamento de pessoas com ByteTrack.
- [ ] Atribuir IDs temporarios para cada pessoa.
- [ ] Contabilizar entradas e saidas da regiao.
- [ ] Evitar contagens repetidas da mesma pessoa.
- [ ] Implementar historico de ocupacao.
- [ ] Criar uma interface visual para monitoramento.
- [ ] Adaptar o sistema para cameras em tempo real.

## Limitacoes da versao atual

A contagem representa as pessoas detectadas dentro da zona em cada frame, e nao a quantidade de individuos unicos que passaram pelo ambiente.

O sistema ainda nao utiliza rastreamento por IDs nem registra entradas e saidas.

## Sobre o desenvolvimento

Projeto desenvolvido para estudo pessoal no Laboratorio de Computacao, com foco em Visao Computacional, Inteligencia Artificial e processamento de imagens.

**Objetivo:** transformar conhecimentos teoricos em uma aplicacao pratica utilizando Python, YOLO e OpenCV.

---

Se este projeto despertou seu interesse, acompanhe sua evolucao pelo repositorio!
