# コーディング規約

## 命名

### 単数系・複数形

単位が時刻を表すときは単数形（2時は`hour = 2`）、期間を表すときは複数形（2時間は`hours = 2`）を使う。

References
- https://tc39.es/proposal-temporal/docs/

### 略語

略語は基本的に使わない。Allow Listで許可された略語だけを使う。

Allow List
- `i`、`j`、`k`、`l`（ループカウンタ）
- `sec`（second、時間の単位）
- `ms`（millisecond、時間の単位）
- `prop(s)`（Reactの用語）

References
- https://github.com/sindresorhus/eslint-plugin-unicorn/blob/main/docs/rules/prevent-abbreviations.md
- https://github.com/sindresorhus/eslint-plugin-unicorn/blob/main/rules/shared/abbreviations.js

### 頭字語

頭字語（e.g., HTTP）は単語の字数に依らずcamelCaseにする。

References
- [C#のコーディング規約では、3文字以上はcamelCase](https://learn.microsoft.com/en-us/dotnet/standard/design-guidelines/capitalization-conventions#capitalization-rules-for-identifiers)

### 辞書

辞書のように扱う変数については `keyToValue` という命名にする。`Value`が配列等でなければ、単数形にする。
また、 `Record<Key, Value>` ではなく `Map<Key, Value>` を使う。

## Named importを使う

可能な限り Default import よりも、 Named import を使う。
