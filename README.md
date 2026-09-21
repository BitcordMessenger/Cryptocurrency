### Core Token Use Cases
* **Micro-Donations (Tipping):** Users can instantly tip content creators, bloggers, or channel admins directly within the chat interface with zero friction.
* **Paid Premium Channels:** Creators can gate premium content, private groups, or analytical feeds behind a monthly/annual subscription paid exclusively in \$MSG.
* **Internal Services & Storage:** Payment for decentralized file storage (media attachments, voice notes), premium themes, animated stickers, and developer API access.
* **Anti-Spam & Rate Limiting:** Sending messages to strangers or broadcasting to large groups requires a fractional burn or lock of \$MSG to prevent Sybil attacks and network spam.

---

## Wallet Integration Guide (MetaMask)

Since the messenger features a built-in exchange system to swap Ethereum (ETH) for our internal utility token, you need to import the token contract into your MetaMask wallet to monitor your balance and manage your assets on the Layer 2 network.

### Network Configuration (Arbitrum One)
Before importing the token, ensure your MetaMask is connected to the **Arbitrum One** network. If it is not configured yet, use the following settings:

* **Network Name:** Arbitrum One
* **New RPC URL:** `[https://arbitrum.io](https://arb1.arbitrum.io/rpc)`
* **Chain ID:** `42161`
* **Currency Symbol:** `ETH`
* **Block Explorer URL:** `https://arbiscan.io`

---

### Method 1: Manual Import via Contract Address

1. Open **MetaMask** and switch your network to **Arbitrum One**.
2. Scroll to the bottom of the **Tokens** tab and click **"Import tokens"**.
3. Select the **"Custom token"** tab.
4. Paste the following official contract details:
   * **Token Contract Address:** `0xYOUR_CONTRACT_ADDRESS_HERE` *(Replace with your actual deployed contract address)*
   * **Token Symbol:** `MSG`
   * **Token Decimal:** `18`
5. Click **"Next"** and then confirm by clicking **"Import"**.

---

### Method 2: One-Click Web Integration (For Developers)

To provide the best user experience within the messenger's web interface or dashboard, you can implement a seamless **"Add Token to MetaMask"** button. This leverages the `wallet_watchAsset` RPC method to automate the manual steps above.

Add the following JavaScript function to your frontend code:

```javascript
async function addTokenToMetaMask() {
  const tokenAddress = '0xYOUR_CONTRACT_ADDRESS_HERE'; // Replace with your actual contract address
  const tokenSymbol = 'MSG';
  const tokenDecimals = 18;
  const tokenImage = 'https://yourmessenger.com'; // URL to your token icon (PNG/SVG)

  if (!window.ethereum) {
    alert('MetaMask is not installed. Please install the extension to interact with the messenger assets.');
    return;
  }

  try {
    // Request MetaMask to add the custom ERC-20 token
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
      console.log('Token successfully added to MetaMask!');
    } else {
      console.log('User declined to add the token.');
    }
  } catch (error) {
    console.error('Error adding token to MetaMask:', error);
  }
}
```

### UI Integration Example
You can trigger the function above using a standard HTML button in your app's wallet settings or post-swap success screen:

```html
<button onclick="addTokenToMetaMask()">Add \$MSG to MetaMask</button>
```
