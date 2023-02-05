# 手順

## GraphQLでの基本型とJSでの対応は以下

```text
String : 文字型 → string

Int : 整数型 → number

Float : 不動小数点 → number

Boolean : 真偽 → boolean

ID : ユニークな識別子 → string
    GraphQLクライアントはこのIDをもとにキャッシュなどを行なってくれるらしい

基本型は全て Nullable。

Nullを許容しない場合は末尾に ! (eg. String!)

リスト型の場合は [] で囲む (eg. [String])
```

1. 初期化とモジュールのインストール

    ```sh
    npm init
    npm install express express-graphql graphql --save
    ```

2. 起動

    ```sh
    node server.js
    ```

3. HTTP リクエスト

    ```javascript
    var query = `{
    quoteOfTheDay,
    random,
    rollThreeDice
    }`;

    fetch('/graphql', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
        'Accept': 'application/json',
    },
    body: JSON.stringify({ query })
    })
    .then(r => r.json())
    .then(data => console.log('data returned:', data));
    ```
