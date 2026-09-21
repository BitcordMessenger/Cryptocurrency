### Core Token Use Cases
* **Micro-Donations (Tipping):** Users can instantly tip content creators, bloggers, or channel admins directly within the chat interface with zero friction.
* **Paid Premium Channels:** Creators can gate premium content, private groups, or analytical feeds behind a monthly/annual subscription paid exclusively in \$MSG.
* **Internal Services & Storage:** Payment for decentralized file storage (media attachments, voice notes), premium themes, animated stickers, and developer API access.
* **Anti-Spam & Rate Limiting:** Sending messages to strangers or broadcasting to large groups requires a fractional burn or lock of \$MSG to prevent Sybil attacks and network spam.

---

## 3. Wallet Integration Guide (MetaMask)

To interact with the messenger's financial features, users need to add both the **Arbitrum One** network and the **\$MSG** token to their Web3 wallets (e.g., MetaMask).

### Step 1: Add Arbitrum One Network to MetaMask
If you haven't added Arbitrum One yet, navigate to MetaMask -> Networks -> Add Network, and input the following configuration:

* **Network Name:** Arbitrum One
* **New RPC URL:** `https://arbitrum.io`
* **Chain ID:** `42161`
* **Currency Symbol:** `ETH`
* **Block Explorer URL:** `https://arbiscan.io`

### Step 2: Import \$MSG Token manually
1. Open MetaMask and switch your network to **Arbitrum One**.
2. Scroll to the bottom of the "Tokens" tab and click **Import tokens**.
3. Select **Custom token** and paste the official contract details:
   * **Token Contract Address:** `0xYOUR_CONTRACT_ADDRESS_HERE` *(Replace with actual deployed address)*
   * **Token Symbol:** `MSG`
   * **Token Decimal:** `18`
4. Click **Next** and then **Import**.

### Developer Integration (One-Click "Add Token" Button)
If you are developing the messenger's web interface, you can implement a one-click button to let users automatically add your token to MetaMask using `window.ethereum`:

```javascript
async function addMSGToken() {
  const tokenAddress = '0xYOUR_CONTRACT_ADDRESS_HERE'; // Replace with your contract
  const tokenSymbol = 'MSG';
  const tokenDecimals = 18;
  const tokenImage = 'https://yourmessenger.com'; // URL to token icon

  try {
    const wasAdded = await window.ethereum.request({
      method: 'wallet_watchAsset',
      params: {
        type: 'ERC20',
        options: {
          address: tokenAddress,
          symbol: tokenSymbol,
          decimals: tokenDecimals,
          image: tokenImage,
        },
      },
    });

    if (wasAdded) {
      console.log('MSG token successfully added to wallet!');
    }
  } catch (error) {
    console.error('Error adding MSG token:', error);
  }
}
```

---

## 4. Monetary Policy & Security
* **Deflationary Mechanism:** A percentage (e.g., 1%) of every internal service fee and subscription payment is permanently **burned** (removed from circulation), reducing overall supply over time.
* **Sybil Protection:** The dynamic fee algorithm scales token requirements upwards if a single node or user attempts to overload the network with rapid messages.
Для полноценного репозитория теперь не хватает только финансовой конкретики. Хотите ли вы добавить:Подробный раздел по Tokenomics Allocation (какой процент токенов идет команде, инвесторам, на маркетинг и в пул ликвидности)?Описание стейкинга для нод (сколько токенов нужно заморозить, чтобы запустить свой релей-сервер для передачи сообщений)?В ответах искусственного интеллекта могут быть ошибки. Если вам требуется финансовая консультация, обратитесь к специалисту. Подробнее…
