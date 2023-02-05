# 手順

## GraphQLでもエンドポイントに引数を持たせることが可能

```text
Int : 整数型 → number

Float : 不動小数点 → number

Boolean : 真偽 → boolean

ID : ユニークな識別子 → string
    GraphQLクライアントはこのIDをもとにキャッシュなどを行なってくれるらしい

基本型は全て Nullable。

Nullを許容しない場合は末尾に ! (eg. String!)

リスト型の場合は [] で囲む (eg. [String])
```

```javascript
// 引数には名前と型を指定する
type Query {
    rollDice(numDice: Int!, numSides: Int): [Int]
}
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
    var dice = 3;
    var sides = 6;
    var query = `query RollDice($dice: Int!, $sides: Int) {
    rollDice(numDice: $dice, numSides: $sides)
    }`;

    fetch('/graphql', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
        'Accept': 'application/json',
    },
    body: JSON.stringify({
        query,
        variables: { dice, sides },
    })
    })
    .then(r => r.json())
    .then(data => console.log('data returned:', data));
    ```
