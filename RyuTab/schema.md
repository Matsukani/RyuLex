# RyuTab schema

RyuTab is based on a relational model consisting of three logical layers:

- **entry** table
- **meaning** table
- **example** table

For ease of curation in Excel, the **entry** table and the **meaning** table are conflated into a single editing table (`goi`).  
At export time (for example, for TeX generation or database registration), this conflation is resolved and the underlying relational structure is restored.

---

## Logical relational model

### 1. Entry table
- Primary key: `項目ID`
- Contains information belonging to the lexical entry as a whole

### 2. Meaning table
- Primary key: `意味ID`
- Foreign key: `項目ID`
- Contains meaning-specific information linked to an entry

### 3. Example table
- Foreign key: `意味ID`
- Contains example sentences linked to a meaning

---

## Editing tables in RyuTab

### `goi`
Editing table in which entry-level and meaning-level information are stored together.

### `reibun`
Example table linked to `意味ID`.

---

## Markup conventions

RyuTab uses a deliberately lightweight markup system.

### 1. Ruby in glosses / equivalent expressions
A dedicated ruby column is provided for glosses such as 相当語・訳語 when exporting to a printed dictionary.


### 2. Ruby in Japanese prose
Use:

`｜漢字〔かんじ〕`

This is used in Japanese prose fields such as:
- 解説
- 備考
- 例文の和訳

### 3. Embedded Ryukyuan forms in Japanese prose
Use:

`〈...〉`

This is used when a Ryukyuan form is embedded inside Japanese prose.

No other inline markup is assumed.

---

## Design principles

- The underlying model is relational.
- Entry-level and meaning-level data are conflated only at the editing stage for ease of curation in Excel.
- Column-level data typing is used to encourage valid and consistent input.
- The markup language is intentionally minimal.
- The format remains simple, but can support rich output when used carefully.

## Notes on glossing

In RyuTab, glossing is strongly normalized.

The fields `意味`, `ルビ`, `読み`, and `解説` have distinct functions:

- `意味` contains the Japanese equivalent expression / gloss (相当語・訳語).
- `読み` contains the reading of `意味` in hiragana and is obligatory.
- `ルビ` contains ruby information for the gloss when needed.
- `解説` is reserved for semantic description, usage notes, or other explanatory content.

This separation is essential for:
- automatic generation of reverse lookup entries
- sorting by meaning
- compatibility with online database publication

## ID Principles

`項目ID` (entry ID) and `意味ID` (meaning ID) follow the principles below:

1. IDs are arbitrarily assigned identifiers and do not carry semantic information.
2. Once assigned, IDs must never be changed.

In particular, even when entries are deleted, added, or reordered during the editing process, existing IDs must remain unchanged.
Changing IDs will break external references and data interoperability; the RyuTab model therefore presupposes that IDs remain stable.

## Table schema

## `goi`（項目／意味テーブル）

| 欄名 | タイプ | 記述 | 所属 | 必須 |
|---|---|---|---|---|
| 項目ID | 数字 | 項目ID | 項目 | ● |
| 地点 | 文字 | 項目が所属している地点（方言） | 項目 | |
| 意味順 | 数字 | 意味番号 | 意味 | ● |
| 意味ID | 数字 | 意味ID | 意味 | ● |
| 仮名表記 | 文字 | 見出しの仮名表記 | 項目 | ● |
| ローマ字表記 | 文字 | ローマ字表記 | 項目 | |
| 拍数 | 数字 | 項目の拍数 | 項目 | |
| 型 | 文字 | 項目のアクセント情報 | 項目 | |
| 品ID | 数字 | 項目の品詞ID | 項目 | |
| 品詞 | 文字 | 項目の品詞 | 項目 | |
| 活用類 | 文字 | 項目の活用クラス | 項目 | |
| 意味 | 文字 | 意味記述の相当語 | 意味 | ● |
| ルビ | 文字 | 意味記述の相当語のルビ | 意味 | |
| 読み | 文字 | 意味記述の相当語の読み | 意味 | ● |
| 解説 | 文字 | 意味記述の解説 | 意味 | |
| 備考 | 文字 | 項目に関する備考 | 項目 | |
| 同 | 数字 | 異形態番号 | 項目 | |
| 類 | 数字 | 類義語番号 | 項目 | |

The column `所属` in the tables above indicates whether a field logically belongs to:

- **項目**: entry-level information
- **意味**: meaning-level information

This distinction is important because `goi` is an editing-layer conflation of entry and meaning data, not the logical relational structure itself.

## `reibun`（例文テーブル）

| 欄名 | タイプ | 記述 | 必須 |
|---|---|---|---|
| 意味ID | 数字 | 意味ID | ● |
| 例文番号 | 数字 | 例文の番号 | ● |
| 仮名表記 | 文字 | 例文の仮名表記 | ● |
| ローマ字表記 | 文字 | 例文のローマ字表記 | |
| 和訳 | 文字 | 例文の和訳 | |
| 備考 | 文字 | 例文に関する備考  | |
| 話者 | 文字 | 音声ファイルがあれば、その発話者の略号 |
| ファイル名 | 文字 | あれば、例文を発話してる音声ファイル名 | |

※「●」が付された項目は必須項目である。

## 音声テーブル（onsei）

音声データは項目IDに紐づけて管理される。

| 欄名 | タイプ | 記述 |
|---|---|---|
| 項目ID | 数字 | 項目ID |
| 話者 | 文字 | 発話者の略号 |
| タイプ | 文字 | 音声のタイプ（X: 単独発音、X+: 拡張音声） |
| 枠文 | 文字 | アクセント資料の枠文 |
| 仮名表記 | 文字 | 音声の書き起こし（仮名表記） |
| ローマ字表記 | 文字 | 音声の書き起こし（ローマ字表記） |
| 型 | 文字 | ピッチ実現に基づくアクセント型 |
| 備考 | 文字 | 音声に関する備考 |
| ファイル名 | 文字 | 音声ファイル名 |

Audio data are treated as information associated with entries rather than meanings.  
This is because audio materials describe entry-level properties such as phonological form and accent.

---

## Sample data

See the `sample/` directory for example files in RyuTab format.