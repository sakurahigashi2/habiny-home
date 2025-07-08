# habiny-home

Nginxを使用して静的なHTMLコンテンツを配信するシンプルなWebサーバーです。

## プロジェクト構成

```
.
├── docker-compose.yml
├── docker
│   ├── .dockerignore
│   ├── Dockerfile
│   └── nginx.conf
├── README.md
├── logs/
└── src
    ├── data/
    |   ├── feed_kr_sample.xml
    |   └── feed_tw_sample.xml
    └── index.html
```

-   **`docker-compose.yml`**: Dockerのサービス、ネットワーク、ボリュームを定義します。
-   **`docker/`**: Docker関連のファイル（Dockerfile, nginx.confなど）を格納します。
-   **`logs/`**: Nginxのアクセスログとエラーログが保存されます。
-   **`src/`**: 静的なウェブサイトのコンテンツ（HTML, サンプルXMLなど）が含まれます。

## 始め方

### 前提条件

-   Docker
-   Docker Compose

### アプリケーションの実行

1.  **リポジトリをクローンします:**

    ```bash
    git clone <repository-url>
    cd habiny-home
    ```

2.  **サーバーを起動します:**

    本番モードでアプリケーションを実行するには、次のコマンドを使用します。

    ```bash
    docker compose up -d
    ```

    アプリケーションは [http://localhost](http://localhost) でアクセスできます。

3.  **開発モードでの実行:**

    開発プロファイル（ポート `3333` で `nginx-dev` サービスを使用）で実行するには、次のコマンドを使用します。

    ```bash
    docker compose --profile dev up -d
    ```

    アプリケーションは [http://localhost:3333](http://localhost:3333) でアクセスできます。

### アプリケーションの停止

```bash
docker compose down
```

## デプロイ

このプロジェクトはAmazon S3で静的ホスティングを行っています。

### デプロイ手順

1. **ファイルの準備**
   
   `src/index.html` ファイルを適切な環境のS3バケットにアップロードします。

2. **アップロード先**

| 環境 | バケットURL |
|------|-------------|
| Production | <https://production-habiny-media-image.s3.ap-northeast-1.amazonaws.com/home/index.html> |
| Development | <https://development-habiny-media-image.s3.ap-northeast-1.amazonaws.com/home/index.html> |

3. **アップロード方法**
   
   AWS CLIやAWSコンソールを使用して、対象の環境に応じたS3バケットの `home/` ディレクトリに `index.html` をアップロードしてください。
