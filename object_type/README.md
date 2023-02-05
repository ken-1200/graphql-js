# 手順

## GraphQL のスキーマでは独自の振る舞いを持ったオブジェクトを定義することができる

オブジェクト型を返す API に対して GraphQL クエリを発行すると、GraphQL フィールド名をネストすることで、オブジェクトの複数のメソッドを一度に呼び出すことができる。

```javascript
// 独自の振る舞いを持った RandomDie を定義
type RandomDie {
  roll(numRolls: Int!): [Int]
}

type Query {
  // RandomDie を返す API
  getDie(numSides: Int): RandomDie
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
    var sides = 6;
    var rolls = 3;

    var query = `query GetDie($sides: Int!, $rolls: Int!) {
    getDie(numSides: $sides) {
        rollOnce
        roll(numRolls: $rolls)
    }
    }`;

    fetch('/graphql', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
        'Accept': 'application/json',
    },
    body: JSON.stringify({
        query,
        variables: { sides, rolls },
    })
    })
    .then(r => r.json())
    .then(data => console.log('data returned:', data));
    ```

    or

    ```javascript
    fetch('/graphql', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ query: '{ getDie(numSides: 6) { rollOnce } }' }),
    })
    .then(res => res.json())
    .then(data => console.log(data))
    .catch(error => console.error(error));
    ```
