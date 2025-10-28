# Modelagem de Nicho Ecológico utilizando Machine Learning

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![R](https://img.shields.io/badge/R-4.1.0+-blue.svg)](https://www.r-project.org/)
[![QGIS](https://img.shields.io/badge/QGIS-3.16+-green.svg)](https://qgis.org)
[![Maxent](https://biodiversityinformatics.amnh.org/open_source/maxent/ban2.png)](https://biodiversityinformatics.amnh.org/open_source/maxent/)

## Sobre

Utilizei o algoritmo de machine learning "Maxent" - Maximum Entropy - na modelagem de nicho ecológico (ENM) de duas espécies aquáticas nativas de interesse econômico:

- ***Holothuria grisea*** (pepino do mar)
- ***Crassostrea tulipa*** (ostra)
  
**Objetivo Principal:** Inferir áreas ambientalmente adequadas para o cultivo  dessas espécies  no litoral brasileiro para promover a aquicultura sustentável e reduzir a dependência de espécies exóticas.

## Como funciona?

<center>Visão esquemática do processo de Modelagem de Nicho Ecológico (ENM)</center>

![Modelagem de Nicho Ecológico]([images/Marcelino_ENM.png](https://raw.githubusercontent.com/LucasBods/Modelagem-de-Nicho-Ecologico/refs/heads/dev/images/Marcelino_ENM.png))
<small>Fonte: MARCELINO, Vanessa R.; VERBRUGGEN, Heroen. Ecological niche models of invasive seaweeds. Journal of Phycology, v. 51, n. 4, p. 606-620, 2015 (fig. 2).</small>
```mermaid
graph TB

    subgraph "⚙️ Fase 1: Entrada de Dados"
        TS1[ ]:::invisible
        TS1 -->A1[" "]
        A1@{ shape: docs, label: "🛰️ Camadas de variáveis Bio-climáticas"} --> A3
        A2[📌Pontos de Ocorrência da Espécie] --> A3{💻 Sobreposição Espacial}
        A3 --> A4[📊 Dados de Treino/Teste para implementação do algoritmo de Machine Learning ''MaxEnt'']
    end
    
    subgraph "⚙️ Fase 2: Processamento ML"
        TS2[ ]:::invisible
        TS2 -.->B1[" "]
        B1[🤖 Algoritmo MaxEnt] --> B2[Treinamento do Modelo]
        B2 --> B3[📈 Validação]
        B3 --> B4{✅ AUC satisfatório?}
        B4 -->|Sim| B5[Modelo Final]
        B4 -->|Não| B1
    end
    
    subgraph "⚙️ Fase 3: Output Visual"
        TS3[ ]:::invisible
        TS3 -.->C1[" "]
        C1[🌍 Projeção Espacial] --> C2[🗺️ 🔥 Resultado: Mapa de calor das áreas inferidas de adequação do nicho da espécie]
        
    end
   
    A4 -.- TS2
    B5 -.- TS3
    
    style A1 fill:#1F6427
    style A2 fill:#D32C31
    style B1 fill:#C2A740
    style B4 fill:#18328e
    style C2 fill:#a5193c
    classDef invisible fill:none,stroke:#none,color:#none,height:0px
    linkStyle 0 stroke:transparent,stroke-width:0px
```


## Síntese dos Resultados

- **Modelagem com o algoritmo Maxent**: foram utilizados 117 pontos de ocorrência da espécie *H. grisea* e 21 pontos da espécie *C. tulipa*.

- **Seleção de variáveis**: foram selecionadas cuidadosamente 21 variáveis ambientais que não apresentavam multicolinearidade para *H. grisea* e 18 para *C. tulipa*.

- **Validação estatística**: foram utilizadas as métricas de área sob a curva (AUC), e o índice de Boyce contínuo (CBI), que atestaram um bom desempenho preditivo:
  - *Holothuria grisea*: AUC 0.990, e CBI entre 0.862 e 0.990
  - *Crassostrea tulipa*: AUC 0.996, e CBI entre 0.647 e 0.928

- **Identificação das áreas ambientalmente adequadas**: Resultados visuais através de mapas gerados pelo software do algoritmo.

- **Contribuição**: Incentivo da aquicultura de espécies nativas, alternativa mais sustentavelmente apropriada e com grande potencial econômico.
