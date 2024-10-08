# コーディング規約

## 命名

実態を過不足なく表現した名を付ける。
誤解の可能性が低い名を付ける。

References
- [リーダブルコード](https://www.oreilly.co.jp/books/9784873115658/)

### ケース（複合語の連結）

| 言語 | 命名対象 | ケース | 備考 |
|-|-|-|-|
| TypeScript | 変数 | `camelCase` | |
|^ | 定数 | `SNAKE_CASE` | イミュータブルなオブジェクトを含む。 |
|^ | 関数 | `camelCase` | |
|^ | クラス | `PascalCase` | メンバ変数・メソッドは`camelCase`。 |
|^ | 型・インターフェース | `PascalCase` | フィールドは`camelCase`。 |
|^ | Reactコンポーネント | `PascalCase` | |
|^ | ファイル | `camelCase` | |
|^ | ファイル（Reactコンポーネント）| `PascalCase` | Reactコンポーネント名と同一の文字列を付ける。 |

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
| `diff` | difference | コマンド名やIT用語として十分に流布しているから。形容詞（different）や別の語（difficultyなど）の意味で使用してはならない。 |

References
- https://github.com/sindresorhus/eslint-plugin-unicorn/blob/main/docs/rules/prevent-abbreviations.md
- https://github.com/sindresorhus/eslint-plugin-unicorn/blob/main/rules/shared/abbreviations.js

### 頭字語

頭字語（e.g., AI, CSV, HTTP）は単語の字数に依らず他の単語と同じように扱う。
つまり、camelCaseならば語の先頭を大文字または小文字に、先頭以外を小文字に（e.g., `Ai`, `Csv`, `Http`）する。

References
- [C#のコーディング規約では、3文字以上はcamelCase](https://learn.microsoft.com/en-us/dotnet/standard/design-guidelines/capitalization-conventions#capitalization-rules-for-identifiers)

### 辞書

辞書のように扱う変数については`keyToValue`という命名にする。`Value`が配列等でなければ、単数形にする。
また、`Record<Key, Value>`ではなく`Map<Key, Value>`を使う。

### 関数

関数名の先頭の語は動詞にする。

| 動作 | 動詞（動詞句） | 理由・備考 |
|-|-|-|
| 変換する | `convert` | `aToB`、`a2b`（先頭の語を動詞にしていない。）ではなく`convertAToB`と命名する。 |
| Page object model（POM）で、UIを操作して画面遷移する | `navigateTo` | `goTo`よりも複雑な手順を踏んでいる印象が強いから。 |
| Page object model（POM）で、URLを変更して画面遷移する | `open` | `goTo`よりも`navigateTo`と混同しづらいから。（`open`であるべき理由が足りない問題、新しいウィンドウ・タブを開く印象を受ける問題が残っているため、再検討する。） |

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

## コーディングスタイル

### TypeScript

#### Named importを使用する

可能な限り Default import よりも、 Named import を使う。

#### 列挙型（`enum`）を使用しない

`enum`を使用すると、TypeScriptコンパイラが即時実行関数を生成するのでtree shakingが妨げられる。

代わりにオブジェクトリテラルを使用する。
元々列挙型を使用するほどではなかった小規模なコードでは、ユニオン型を使用し続けてよい。
いずれについても、referencesの記事にサンプルコードが記載されている。

References
- [列挙型(enum)の問題点と代替手段 | TypeScript入門『サバイバルTypeScript』](https://typescriptbook.jp/reference/values-types-variables/enum/enum-problems-and-alternatives-to-enums)

#### 必要がない限り`interface`でなく`type`を使用する

`interface`には同名の宣言によってマージできる性質がある。
これはライブラリに拡張性を持たせる目的では有用だが、大抵のアプリケーションの開発においては不要な性質であり、むしろ想定外のマージによって不具合を引き起こしうる欠点のほうが大きくなる。

References
- [interfaceとtypeの違い | TypeScript入門『サバイバルTypeScript』](https://typescriptbook.jp/reference/object-oriented/interface/interface-vs-type-alias)

#### `window`オブジェクトのプロパティを使用するとき、`window`を省略しない

`window`オブジェクトのプロパティか、他の変数・関数かを一目では区別できなくなるので、`window`を省略してはならない。

:x:

```ts
setTimeout()
```

:white_check_mark:

```ts
window.setTimeout()
```

#### ログのメッセージの文末に`.`を付ける

:x:

```ts
logger.info('Deleted items');
```

:white_check_mark:

```ts
logger.info('Deleted items.');
```

#### ログに変数を含めるとき、メッセージの末尾に`:`を付けて埋め込む

ログの途中に変数を埋め込むと、変数の値によってログの文言が変化するので、単純な文字列では検索しづらくなる。
変数をログの末尾に置くことで、文言を不変とし、検索しやすくすることができる。

なお、埋め込んだ変数の末尾に `.` や `。` は記載しない。

:x:

```ts
logger.info('Deleted %d items.', items.length);
```

:white_check_mark:

```ts
logger.info('Deleted items: %o', { count: items.length });
```

#### 未完了の処理をロギングするとき、メッセージの文末（`:`の前）に`...`を付ける

:white_check_mark:

```ts
logger.info('Deleting items ...: %o', { count: items.length });
```

### React

#### Propsを分割代入しない

:x:

```ts
const Component: FC.React<Props> = ({ a, b, c, d }) => {
  // ...
};
```

:white_check_mark:

```ts
const Component: FC.React<Props> = (props) => {
  // ...
};
```

#### アンマウントされたコンポーネントの非同期処理

非同期処理の結果などによって、アンマウント済みのコンポーネントで何らかの処理が実行されることがある。
[`useUnmountPromise`](https://github.com/streamich/react-use/blob/master/docs/useUnmountPromise.md)を使用するとそのような実行を阻止できるが、不具合も重大なパフォーマンス低下も発生しない場合には使用してはならない。

`setState`が実行される場合、React 17以前では警告が発生したので、`useUnmountPromise`が必要だった。
しかし、React 18以降では警告が発生しなくなったので、`setState`の阻止だけを目的とした`useUnmountPromise`の使用を禁止する。

References
- https://github.com/facebook/react/pull/22114

## 推奨パッケージ

特に理由がない限り、次のパッケージを採用する。

| 用途 | パッケージ | 理由 |
|-|-|-|
| ログ | [pino](https://github.com/pinojs/pino) | 超高速かつそれなりに有名だから。 `winston` よりもAsynchronousな処理の対応に優れているから。 |
| 日付時刻 | [Temporal](https://tc39.es/proposal-temporal/docs/ja/index.html) | まだプロポーザルだが、標準ライブラリに入る可能性が高いから。ポリフィルには[@js-temporal/polyfill](https://github.com/js-temporal/temporal-polyfill)を採用する。 |
| 日付時刻パース・フォーマット | TBD ([Day.js](https://github.com/iamkun/dayjs/) vs [date-fns](https://github.com/date-fns/date-fns)) | TBD |
| CSVパース・フォーマット | [node-csv](https://github.com/adaltas/node-csv) | TBD [PapaParse](https://github.com/mholt/PapaParse)よりも……だから。 |
| スキーマ | [Zod](https://github.com/colinhacks/zod) | 静的型推論に対応しているから。機能が充実しているから。 |
