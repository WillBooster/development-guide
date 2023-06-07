# コーディング規約

## 命名

実態を過不足なく表現した名を付ける。
誤解の可能性が低い名を付ける。

References
- [リーダブルコード](https://www.oreilly.co.jp/books/9784873115658/)

### 単数系・複数形

単位が時刻を表すときは単数形（2時は`hour = 2`）、期間を表すときは複数形（2時間は`hours = 2`）を使う。

References
- https://tc39.es/proposal-temporal/docs/

### 略語

略語は基本的に使わない。Allow Listで許可された略語だけを使う。

Allow List

| 略語 | 意味 | 理由 |
|-|-|-|
| `i`, `j`, `k`, `l` | ループカウンタ | 十分に流布しており誤解しないから。小さいスコープでの使用に限定する。 |
| `min`, `max` | minimum, maximum | 十分に流布しており誤解しないから。 |
| `sec` | second（秒） | 補足的な情報だから。変数などが持つ数値の単位を表す接尾辞に限定する。e.g. `timeLimitSec` |
| `ms` | millisecond | 同上。e.g. `timeLimitMs` |
| `prop(s)` | property | Reactの用語だから。 https://ja.reactjs.org/docs/components-and-props.html |

References
- https://github.com/sindresorhus/eslint-plugin-unicorn/blob/main/docs/rules/prevent-abbreviations.md
- https://github.com/sindresorhus/eslint-plugin-unicorn/blob/main/rules/shared/abbreviations.js

### 頭字語

頭字語（e.g., CSV, HTTP）は単語の字数に依らず他の単語と同じように扱う。
つまり、camelCaseならば語の先頭を大文字または小文字に、先頭以外を小文字に（e.g., `Csv`, `Http`）する。

References
- [C#のコーディング規約では、3文字以上はcamelCase](https://learn.microsoft.com/en-us/dotnet/standard/design-guidelines/capitalization-conventions#capitalization-rules-for-identifiers)

### 辞書

辞書のように扱う変数については `keyToValue` という命名にする。`Value`が配列等でなければ、単数形にする。
また、 `Record<Key, Value>` ではなく `Map<Key, Value>` を使う。

### React

`Context.Provider`をラップしたコンポーネントの名の末尾に`Provider`を付ける。
（e.g., `UserProvider`）

References
- [`ChakraProvider`](https://chakra-ui.com/getting-started) (Chakra UI)
- [`ThemeProvider`](https://emotion.sh/docs/theming) (Emotion)

`useContext`をラップしたフックの名の末尾に`Context`を付けない。
（e.g., `useUser`）
ただし、付けないと意味が伝わらない場合は付けてもよい。

References
- [`useTheme`](https://emotion.sh/docs/theming) (Emotion)
- [`useRouter`](https://nextjs.org/docs/api-reference/next/router) (Next.js)
- [`useFormContext`](https://react-hook-form.com/api/useformcontext) (React Hook Form)

[`useContextSelector`](https://github.com/dai-shi/use-context-selector)をラップしたフックの名の末尾に`Selector`を付ける。
（e.g., `useUserSelector`）

## ファイル構造

### Named importを使う

可能な限り Default import よりも、 Named import を使う。

## 依存パッケージ

特に理由がない限り、次のパッケージを採用する。

| 用途 | パッケージ | 理由 |
|-|-|-|
| ログ | [winston](https://github.com/winstonjs/winston) | TBD |
| 日付パース・フォーマット | TBD (Temporal vs [Day.js](https://github.com/iamkun/dayjs/) vs [date-fns](https://github.com/date-fns/date-fns)) | TBD |
| CSVパース・フォーマット | TBD ([PapaParse](https://github.com/mholt/PapaParse) vs [node-csv](https://github.com/adaltas/node-csv)) | TBD |
| スキーマ | [Zod](https://github.com/colinhacks/zod) | 静的型推論に対応しているから。機能が充実しているから。 |
