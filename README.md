# solana-token2022-sample-code
Solana上で発行するToken2022のサンプルコード

## Solana Dapp開発環境セットアップ

### キーペア作成

```bash
mkdir ~/.solana_keypairs
cd ~/.solana_keypairs

solana config set --url https://api.devnet.solana.com

solana-keygen new -o ./sol.json
solana config set --keypair ./sol.json
```

以下のようになればOK！

```bash
Config File: /home/vscode/.config/solana/cli/config.yml
RPC URL: https://api.devnet.solana.com 
WebSocket URL: wss://api.devnet.solana.com/ (computed)
Keypair Path: ./sol.json 
Commitment: confirmed 
```

### アドレス確認

```bash
solana address
```

### Faucetで取得

https://faucet.solana.com/ にアクセスして開発用のSOLを取得する

## Token 2022の発行

### Tokenの発行

```bash
spl-token --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb create-token --enable-metadata
```

```bash
Address:  AqYMCt2NkZftjuMTU3GQG4FDtcbtGi4oPZsazUSVT61K
Decimals:  9

Signature: FCJuN6EqcgPAQKw9dRyeFzph5mC1NEUsQpb7CwawqmwJDnbfPkFaUxjpTuQ6QUxVyYnH9B7WQFWwUZUZNERt8Ao
```

[AqYMCt2NkZftjuMTU3GQG4FDtcbtGi4oPZsazUSVT61K](https://explorer.solana.com/address/AqYMCt2NkZftjuMTU3GQG4FDtcbtGi4oPZsazUSVT61K?cluster=devnet)

### Token Accountの作成

```bash
spl-token create-account AqYMCt2NkZftjuMTU3GQG4FDtcbtGi4oPZsazUSVT61K
```

```bash
Creating account EgBnGZAecez8AfGQ8gL2uQqt3EGixTUjy3Pgr2tdcXwt

Signature: 4D9G7LpMAFj7odcKVqFaTR1D5TFw5TnVzygoKUmviHKRWeq3RivPELsLb9LUgBz4EDDFdCNwmAbrZKGUMipMgQDY
```

### 残高確認

```bash
spl-token balance AqYMCt2NkZftjuMTU3GQG4FDtcbtGi4oPZsazUSVT61K
spl-token accounts --verbose
solana balance
```

### サンプル用のメタデータ

```json
{
  "name": "Some Token",
  "symbol": "STKN",
  "description": "This is a test token",
  "image":"http://raw.githubusercontent.com/Kevinscki/stkn/main/image.png"
}
```

### 初期化

```bash
spl-token initialize-metadata AqYMCt2NkZftjuMTU3GQG4FDtcbtGi4oPZsazUSVT61K "Some Token" "STKN" "https://raw.githubusercontent.com/Kevinscki/stkn/main/metadata.json"
```

```bash
Signature: g8tY1gFSzSo1Eog1yt6XoqUVQsNScfHTyYxC7mDQDo5YFZnVkHwnERUaw9reB2J7qxsRVGSVAv8LHoBWc7PeCi9
```

するとメタデータが割り当てられる

[AqYMCt2NkZftjuMTU3GQG4FDtcbtGi4oPZsazUSVT61K](https://explorer.solana.com/address/AqYMCt2NkZftjuMTU3GQG4FDtcbtGi4oPZsazUSVT61K?cluster=devnet)

## Tokenの操作

### ミント

```bash
spl-token mint AqYMCt2NkZftjuMTU3GQG4FDtcbtGi4oPZsazUSVT61K 100
```

別のアドレスに対してミントする場合には以下を実行

```bash
spl-token mint AqYMCt2NkZftjuMTU3GQG4FDtcbtGi4oPZsazUSVT61K 100 -- Hmyk3FSw4cfsuAes7sanp2oxSkE9ivaH6pMzDzbacqmt
```

### 送金

```bash
spl-token transfer AqYMCt2NkZftjuMTU3GQG4FDtcbtGi4oPZsazUSVT61K 10 4Bb5ea2KjCzXoU9ViBuvK3jj7WKKFwbvdeMbKwAxaDg7
```

```bash
Transfer 10 tokens
  Sender: EgBnGZAecez8AfGQ8gL2uQqt3EGixTUjy3Pgr2tdcXwt
  Recipient: 4Bb5ea2KjCzXoU9ViBuvK3jj7WKKFwbvdeMbKwAxaDg7
  Recipient associated token account: HorrG86cJQhVthdJw75L3MV9vmvvhNWquPvkQDrtsQJy
```

## 参考文献
- [token-2022](https://github.com/mashharuki/token-2022/tree/main/clients/js)
- [Making a Solana Token (Token-2022) Guide](https://medium.com/@kelvinrutatina/making-a-solana-token-token-2022-guide-7d5a7747cd87)
- [Solana Token 公式開発者向けドキュメント](https://solana.com/ja/docs/tokens/basics)