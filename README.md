# オレオレ証明書でnginxにHTTPSで接続する最小構成
1. 秘密鍵の作成
```
openssl genrsa -out ./server.key
```
2. CSR（証明書リクエスト）の作成
```
openssl req -new -key ./server.key -out ./server.csr
```
3. CRT（証明書）の作成（オレオレ証明書）
```
openssl x509 -days 3650 -req -signkey ./server.key -in ./server.csr -out ./server.crt
```
4. nginxの起動
```
docker build .
docker run -p 443:443 <コンテナID>
```

メモ
- オレオレ証明書なので、ブラウザでアラートが表示される。
- Chromeだと見れないかも。
- FireFoxであればOKを押していけば無理やり見れる。