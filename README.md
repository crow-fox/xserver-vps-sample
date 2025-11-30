# XServer VPS Sample

最初に登録する時に、秘密鍵をダウンロード

接続テスト

```bash
ping <your-vps-ip-address>
```

XServer VPS の設定画面からパケットフィルターを設定して、port 22 (SSH) を許可

ssh が開いているか

```bash
nc -vz <your-vps-ip-address> 22
```

秘密鍵を.ssh/<your-key-file> に保存して、パーミッションを 600 に設定

```bash
mv <downloaded-key-file> ~/.ssh/<your-key-file>
chmod 600 ~/.ssh/<your-key-file>
```

SSH 接続

```bash
ssh -i ~/.ssh/<your-key-file> root@<your-vps-ip-address>
```

公開鍵が登録されているかを一応確認

```bash
cat ~/.ssh/authorized_keys
```

nginx インストール

```bash
apt update
apt install -y nginx
```

nginx サービス起動

```bash
systemctl start nginx
systemctl enable nginx
```

nginx デフォルトの公開ディレクトリ作成

```bash
mkdir -p /var/www/html
```

github actions の変数設定

secrets に以下を登録

| Name            | Value                        |
| --------------- | ---------------------------- |
| SSH_PRIVATE_KEY | ダウンロードした秘密鍵の中身 |

variables に以下を登録

| Name           | Value                   |
| -------------- | ----------------------- |
| SSH_USER       | root                    |
| SSH_HOST       | <your-vps-標準ホスト名> |
| SSH_PORT       | 22                      |
| SSH_REMOTE_DIR | /var/www/html           |
