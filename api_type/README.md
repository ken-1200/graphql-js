# 手順

## API を作成する方法

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
    var id = "a"
    var query = `query user($id: String) {
    user(id: $id) {
        id
        name
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
        variables: { id },
    })
    })
    .then(r => r.json())
    .then(data => console.log('data returned:', data));
    ```
