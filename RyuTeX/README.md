# RyuTeX: a LaTeX template for Ryukyuan–Japanese dictionaries

**Version:** v1.0  
**Status:** Stable initial release  
**Last updated:** 2026-03

**RyuTeX** is part of the **RyuLex (“Ryukyuan Lexicography”)** framework, which is designed to support the curation,  
validation, and publication of Ryukyuan–Japanese bilingual lexicographic data using a unified data model.

This repository provides a publishable LaTeX template in book format  
for compiling a full Ryukyuan–Japanese bilingual dictionary from data curated in the  
**Ryukyuan Tabular Schema (RyuTab)**.

RyuTeX operates as part of the following workflow:
RyuTab (Excel) → converter (tab2tex.py) → TeX data → RyuTeX → PDF

The template can be applied not only to Ryukyuan data,  
but also to other Japanese dialect–Japanese bilingual dictionaries.

---

## Author

Kenan Celik  
https://researchmap.jp/miyako

---

## Engine

- **LuaLaTeX** (required)
- Japanese support via `luatexja`
- Two-column dictionary pages via `multicols*`
- Tested on Overleaf and local LuaLaTeX environments
- Local compilation should work with a standard LuaLaTeX environment, but has not been tested

---

## File Structure
```
├── main.tex # Main document file (book structure)
├── main.bib # Dummy Bibliography (mainly on Ryukyuan Research)
├── README.md # This file
│
├── settings/
│ ├── typesetting.tex # Engine + typography policy
│ │ (fonts, 禁則処理, float-page behavior)
│ ├── d_commands.tex # Dictionary-specific macros
│ │ (entry layout, letter headings, etc.)
│ └── bib-config.tex # bibliography settings 
│
├── chapters/
│ ├── 1_kaisetsu.tex # 辞書の概説（『みんなふつ語彙集』より）
│ ├── 2_bibliography.tex # 参考文献
│ ├── 3_hanrei.tex # 凡例
│ ├── 4_atogaki.tex # あとがき
│ ├── 5_shaji.tex # 謝辞
│ └── 6_okuzuke.tex # 奥付
│
├── data/
│ ├── hateruma_sample_260321.tex
│ │   # sample data of Ryukyuan-Japanese entries
│ │   # (output by tab2tex.py)
│ └── hateruma_sample_reverse_260321.tex
│      # sample data of Japanese-Ryukyuan reverse lookup
│      # (output by tab2tex.py)
│
└── example_output/
  └── RyuTex_example.pdf
      # PDF output based on chapters and data
```


## Design Principles of the LaTeX Template

- **Separation of structure and typesetting**  
  `main.tex` defines document structure only.

- **Centralized typography control**  
  Fonts, Japanese layout rules (禁則処理), and page behavior are defined in  
  `settings/typesetting.tex`.

- **Isolated dictionary logic**  
  Entry formatting and letter headings are defined in  
  `settings/d_commands.tex`.

- **Centralized bibliography configuration**  
  All bibliography-related settings are handled in  
  `settings/bib-config.tex`.

- **Externally generated data**  
  The files in `data/` are generated automatically from RyuTab-formatted data  
  using the RyuLex conversion tools.

  These files should normally **not be edited manually**.  
  Manual modification should be limited to exceptional edge cases.

---

## Customization

- Fonts / Japanese layout  
  → `settings/typesetting.tex`

- Bibliography  
  → `settings/bib-config.tex`

- Dictionary layout  
  → `settings/d_commands.tex`

- Dictionary content  
  → regenerate `data/*.tex` from RyuTab data

---

## Data Conversion

Dictionary data is generated from RyuTab (Excel) using conversion scripts.

The converter:
- resolves entry/meaning structure
- applies markup interpretation
- outputs TeX-ready dictionary entries

Users are not expected to edit TeX data directly.

---

## License

This template is released under the MIT License.

(The MIT License applies only to the template and associated scripts.  
Dictionary contents generated using this template are not subject to this license.)

If you use this template, citation or acknowledgement is appreciated but not required.

### Suggested citation

**EN**  
Celik, Kenan (2026). *RyuTeX: A LaTeX template for Ryukyuan–Japanese dictionaries*.  
Version 1.0. https://github.com/USERNAME/REPOSITORY

**JP**  
セリック・ケナン（2026）『RyuTeX：琉和辞典用のLaTeXテンプレート』  
Version 1.0. https://github.com/USERNAME/REPOSITORY