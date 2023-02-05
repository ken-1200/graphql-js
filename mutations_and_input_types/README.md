# 手順

## データの挿入やデータの変更などを行うAPIでは Query ではなく Mutation として定義する

```javascript
// メッセージの更新と取得するAPIのスキーマ
type Mutation {
  setMessage(message: String): String
}

type Query {
  getMessage: String
}
```

```javascript
// 同じ入力パラメータを複数のAPIで使う時などは input キーワードを使って入力型としてまとめることができる
input MessageInput {
  content: String
  author: String
  # message: Message  -> オブジェクト型はダメ
}

type Message {
  id: ID!
  content: String
  author: String
}

type Query {
  getMessage(id: ID!): Message
}

type Mutation {
  createMessage(input: MessageInput): Message
  updateMessage(id: ID!, input: MessageInput): Message
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
    // getMessages
    var query = `query getMessages {
    getMessages {
        id
        content
        author
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
    })
    })
    .then(r => r.json())
    .then(data => console.log('data returned:', data));
    ```

    ```javascript
    // getMessage
    var id = "68e7f5e405552bedd36d";
    var query = `query getMessage($id: ID!) {
    getMessage(id: $id) {
        id
        content
        author
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

    ```javascript
    // CreateMessage
    var author = "andy"
    var content = "hope is a good thing"
    var query = `mutation CreateMessage($input: MessageInput) {
    createMessage(input: $input) {
        id
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
        variables: {
            input: {
                author,
                content,
            }
        },
    })
    })
    .then(r => r.json())
    .then(data => console.log('data returned:', data));
    ```

    ```javascript
    // updateMessage
    id = "2a7899e9b53d752d15cc"
    var author = "machida"
    var content = "machida!"
    var query = `mutation updateMessage($id: ID!, $input: MessageInput) {
    updateMessage(id: $id, input: $input)  {
        id
        content
        author
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
        variables: {
            id,
            input: {
                author,
                content,
            }
        },
    })
    })
    .then(r => r.json())
    .then(data => console.log('data returned:', data));
    ```

    ```javascript
    // deleteMessage
    id = "2a7899e9b53d752d15cc"
    var query = `mutation deleteMessage($id: ID!) {
    deleteMessage(id: $id)
    }`;

    fetch('/graphql', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
        'Accept': 'application/json',
    },
    body: JSON.stringify({
        query,
        variables: {
            id,
        },
    })
    })
    .then(r => r.json())
    .then(data => console.log('data returned:', data));
    ```
