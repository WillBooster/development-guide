# コーディング規約

## 略語

略語は基本的に使わない。Allow Listで許可された略語だけを使う。
Allow List: `prop(s)`, `i,j,k,l`, 

- References
  - https://github.com/sindresorhus/eslint-plugin-unicorn/blob/main/docs/rules/prevent-abbreviations.md
  - https://github.com/sindresorhus/eslint-plugin-unicorn/blob/main/rules/shared/abbreviations.js
  
## 頭字語

頭字語（e.g., HTTP）は単語の字数に依らずcamelCaseにする。

- References
  - C#のコーディング規約では、3文字以上はcamelCase [要出典]
  
## 辞書の命名

辞書のように扱う変数については `keyToValue` という命名にする。`Value`が配列等でなければ、単数形にする。
また、 `Record<Key, Value>` ではなく `Map<Key, Value>` を使う。

## Named importを使う

可能な限り Default import よりも、 Named import を使う。
