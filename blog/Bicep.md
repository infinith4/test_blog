Bicepは、Azureリソースを宣言的にデプロイするためのドメイン固有言語（DSL）であり、ARMテンプレートの記述を簡素化することを目的としています。以下では、Bicepの重要な概念である`param`、`var`、`module`、`secure`、`output`について説明します。

### 1. **param（パラメータ）**
`param`は、実行時に値をBicepテンプレートに渡すためのパラメータを定義するために使用されます。これにより、テンプレートの再利用が可能になり、値のハードコーディングを避けることができます。

例:
```bicep
param storageAccountName string = 'mystorageacct'
```
ここでは、`storageAccountName`という名前の`string`型のパラメータが定義されており、デフォルト値が設定されています。

- **型**: `string`、`int`、`bool`、`array`などの型を指定できます。
- **デフォルト値**: パラメータにデフォルト値を設定することも可能です。

### 2. **var（変数）**
`var`は、テンプレート内で中間的な値や計算結果を保持するための変数を定義するために使用されます。変数を使うことで、コードの重複を避け、読みやすくなります。

例:
```bicep
var location = 'EastUS'
```
これは、`location`という変数に`EastUS`を設定し、テンプレート内で再利用する例です。

- **式**: 変数は、式や文字列の連結、計算などを保持できます。
- **スコープ**: 変数はテンプレート内でのみ使用可能で、外部には公開されません。

### 3. **module（モジュール）**
`module`は、他のBicepテンプレートを参照して再利用するために使用されます。これにより、大規模なテンプレートを分割して、より管理しやすくすることができます。

例:
```bicep
module storageModule './storage.bicep' = {
  name: 'storageModule'
  params: {
    storageAccountName: storageAccountName
  }
}
```
この例では、別のテンプレートである`storage.bicep`をインポートして再利用しています。

- **モジュール化**: 複雑なインフラを整理し、リソースをモジュールにグループ化するのに役立ちます。
- **再利用**: モジュールは、異なるデプロイメントで再利用可能です。

### 4. **secure（セキュアパラメータ）**
Bicepでは、パスワードやAPIキーのような機密情報を取り扱う場合、セキュアなパラメータを定義できます。これにより、デプロイメント中に値が安全に処理されます。

例:
```bicep
param adminPassword string {
  metadata: {
    description: 'VMの管理者パスワード'
  }
  secure: true
}
```
- **セキュリティ**: `secure`とマークされた値は暗号化され、ログや出力に表示されません。

### 5. **output（出力）**
`output`は、デプロイメントが完了した後にBicepテンプレートから値を返すために使用されます。リソースIDや接続文字列のような情報をデプロイ後に返す場合に役立ちます。

例:
```bicep
output storageAccountId string = storageAccount.id
```
この例では、作成されたストレージアカウントのリソースIDを返します。

- **データの返却**: 出力された値は、後続のデプロイメントや追加のアクションで使用できます。
- **複数の出力**: 1つのBicepファイルに複数の`output`ステートメントを含めることができます。

### 全体の例
これらの要素をまとめたシンプルなBicepテンプレートの例を以下に示します。

```bicep
param storageAccountName string
param adminPassword string {
  secure: true
}
var location = 'EastUS'

resource storageAccount 'Microsoft.Storage/storageAccounts@2021-04-01' = {
  name: storageAccountName
  location: location
  sku: {
    name: 'Standard_LRS'
  }
  kind: 'StorageV2'
}

module networkModule './network.bicep' = {
  name: 'networkModule'
  params: {
    location: location
  }
}

output storageAccountId string = storageAccount.id
```

このテンプレートでは：
- `storageAccountName`とセキュアな`adminPassword`という2つのパラメータを受け取ります。
- `location`という変数を使って地域を指定します。
- ストレージアカウントをデプロイし、別の`network.bicep`モジュールを呼び出します。
- ストレージアカウントのリソースIDを出力します。

この記事では、これらのセクションをより詳細に説明し、例やユースケースを追加することで、読者がBicepを理解しやすくすることができます。
