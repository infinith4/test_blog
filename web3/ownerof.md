0хас344d02874336701b2fb7612823997816b1f23e

```
import { ethers } from "ethers";

const provider = new ethers.JsonRpcProvider("https://mainnet.infura.io/v3/YOUR_INFURA_PROJECT_ID");
const contractAddress = "0xYourNFTContractAddress";
const tokenId = "12345"; // Token ID

const abi = [
    "function ownerOf(uint256 tokenId) external view returns (address)"
];

const contract = new ethers.Contract(contractAddress, abi, provider);

async function getOwner() {
    try {
        const owner = await contract.ownerOf(tokenId);
        console.log("Owner Address:", owner);
    } catch (error) {
        console.error("Error fetching owner:", error);
    }
}

getOwner();
```


`ethers.js v6` を使用して、特定のコントラクトアドレスに対する `Transfer` イベントを取得する TypeScript のコードを以下に示します。  

### 手順:
1. `ethers.js` をインストール  
   ```sh
   npm install ethers
   ```
2. TypeScript で `Transfer` イベントをリスンするコードを作成  

---

### TypeScript コード (`getTransferEvents.ts`)
```typescript
import { ethers } from "ethers";

// RPC URL (適宜変更してください)
const RPC_URL = "https://mainnet.infura.io/v3/YOUR_INFURA_PROJECT_ID";

// 監視対象のERC-20コントラクトアドレス (例: USDT)
const CONTRACT_ADDRESS = "0xdAC17F958D2ee523a2206206994597C13D831ec7";

// ERC-20 の Transfer イベントのシグネチャ
const TRANSFER_EVENT_SIGNATURE = "event Transfer(address indexed from, address indexed to, uint256 value)";

async function getTransferEvents() {
    // プロバイダーを作成
    const provider = new ethers.JsonRpcProvider(RPC_URL);

    // コントラクトインスタンスを作成
    const contract = new ethers.Contract(CONTRACT_ADDRESS, [TRANSFER_EVENT_SIGNATURE], provider);

    // 過去の `Transfer` イベントを取得 (例: 最新100ブロック分)
    const latestBlock = await provider.getBlockNumber();
    const fromBlock = latestBlock - 100;

    console.log(`Fetching events from block ${fromBlock} to ${latestBlock}...`);

    const events = await contract.queryFilter("Transfer", fromBlock, latestBlock);

    // イベント情報を表示
    events.forEach((event) => {
        console.log(`Transfer detected: From ${event.args?.from} To ${event.args?.to} Amount ${event.args?.value.toString()}`);
    });
}

// 関数を実行
getTransferEvents().catch(console.error);
```

---

### 説明:
1. `ethers.JsonRpcProvider` を用いて RPC プロバイダーを作成。
2. ERC-20 の `Transfer` イベント (`event Transfer(address indexed from, address indexed to, uint256 value)`) を ABI に設定。
3. `queryFilter("Transfer", fromBlock, latestBlock)` を使用して過去の `Transfer` イベントを取得。
4. 取得したイベントの `from`, `to`, `value` をログ出力。

---

### 追加機能:
**リアルタイムで Transfer イベントをリッスンする場合**
```typescript
contract.on("Transfer", (from, to, value) => {
    console.log(`Real-time Transfer: From ${from} To ${to} Amount ${value.toString()}`);
});
```
このコードを追加すれば、`Transfer` イベントが発生するたびにリアルタイムでキャッチできます。
