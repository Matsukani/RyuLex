# RyuLex

**RyuLex** (Ryukyuan Lexicography) is a framework for the collection, curation, and publication of Ryukyuan–Japanese lexical data.

It provides a unified workflow covering:

- field data collection  
- structured data curation  
- dictionary compilation and publication  

The framework is built around a small set of interoperable components.

---

## Overview

RyuLex is organized as a modular pipeline:
```Questionnaire → RyuTab → conversion tools → RyuTeX → publication```

Each component can be used independently, but together they provide a complete lexicographic workflow.

---

## Components

### 1. Questionnaire

A lexical elicitation questionnaire for Ryukyuan languages.

- structured by semantic fields  
- includes example sentences  
- designed for fieldwork use  
- adaptable depending on context  

The questionnaire facilitates the systematic collection of lexical and usage data.

---

### 2. RyuTab

**RyuTab** (Ryukyuan Tabular Schema) is the data model used to structure lexical data.

- relational model (entry / meaning / example)  
- Excel-based editing format  
- minimal markup system  
- strict separation of gloss and semantic description  

RyuTab enables consistent data curation and compatibility with downstream tools.

---

### 3. tools

Tools for transforming RyuTab data into publication formats.

#### tab2tex.py

- converts RyuTab Excel data into TeX source  
- generates:
  - dictionary entries  
  - reverse index  
- applies:
  - orthography normalization  
  - markup processing  
  - gojūon-based sorting  

These tools bridge the gap between structured data and typeset output.

---

### 4. RyuTeX

**RyuTeX** is a LaTeX template for producing Ryukyuan–Japanese dictionaries.

- book-format output  
- two-column dictionary layout  
- Japanese typography via `luatexja`  
- fully automated integration with RyuTab data  

RyuTeX handles the typesetting and publication stage.

---

## Design principles

RyuLex is based on the following principles:

- **Separation of concerns**  
  data collection, structuring, and publication are handled by distinct components

- **Structured data over ad hoc annotation**  
  lexical data are stored in a normalized format (RyuTab)

- **Minimal but expressive markup**  
  only essential markup conventions are used

- **Practical workflow**  
  Excel-based editing is used to lower the barrier to data creation

- **Reproducibility**  
  outputs are generated automatically from structured data

---

## Scope

RyuLex is designed primarily for:

- Ryukyuan language documentation  
- dialect lexicography  
- bilingual dictionary compilation  

However, the framework can be adapted to other Japanese dialect lexicographic projects.

---

## Philosophy

RyuLex is conceived as a set of interoperable components centered on a shared data model
and adopts a deliberately constrained design.

Rather than attempting to accommodate all possible types of information,  
it focuses on the core components of lexical description:

- form  
- meaning  
- usage  
- phonology  

This constraint ensures structural consistency, comparability, and long-term usability of the data.

---

## Repository structure
```
RyuLex/
├── Questionnaire/ # Lexical elicitation questionnaire (fieldwork tool)
├── RyuTab/ # Data model (schema, documentation, samples)
├── RyuTeX/ # LaTeX template for dictionary publication
├── tools/ # Conversion and utility scripts (e.g. tab2tex.py)
└── README.md # This file
```

---

## License

Each component of RyuLex is released under the MIT License unless otherwise specified.

(The license applies to code and templates.  
Lexical data themselves are subject to their respective data licenses.)

---

## Author

Kenan Celik  
https://researchmap.jp/miyako