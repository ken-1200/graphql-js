# 手順

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

    ```curl
    curl -X POST \
    -H "Content-Type: application/json" \
    -d '{"query": "{ hello }"}' \
    http://localhost:4000/graphql
    ```

    or

    ```javascript
    fetch('/graphql', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'Accept': 'application/json',
    },
        body: JSON.stringify({query: "{ hello }"})
    })
    .then(r => r.json())
    .then(data => console.log('data returned:', data));
    ```
