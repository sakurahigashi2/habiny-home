# Nginxの公式イメージを使用
FROM nginx:alpine

# 作業ディレクトリを設定
WORKDIR /usr/share/nginx/html

# デフォルトのnginxコンテンツを削除
RUN rm -rf /usr/share/nginx/html/*
RUN rm -rf /etc/nginx/conf.d/default.conf

# srcディレクトリの内容をnginxのドキュメントルートにコピー
COPY src/ /usr/share/nginx/html/

# カスタムnginx設定ファイルをコピー（オプション）
COPY docker/nginx.conf /etc/nginx/nginx.conf

# ポート80を公開
EXPOSE 80

# nginxをフォアグラウンドで起動
CMD ["nginx", "-g", "daemon off;"]
