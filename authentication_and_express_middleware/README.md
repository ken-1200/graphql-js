# 手順

## express-graphqlと組み合わせて、Expressミドルウェアを簡単に利用

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
    // getMessages
    var query = `query ip {
    ip
    }`;

    fetch('/graphql', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
        'Accept': 'application/json',
    },
    body: JSON.stringify({
        query,
    })
    })
    .then(r => r.json())
    .then(data => console.log('data returned:', data));
    ```
