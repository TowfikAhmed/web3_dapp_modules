## Module 1 – Web3 Fundamentals

**Definition:** Decentralized internet where blockchain replaces centralized servers.

**Core Components:**
- • Blockchain
- • Smart Contracts
- • Wallets
- • Gas Fees
- • Tokens (ERC20, ERC721)
- • DApps

**Ethereum Virtual Machine (EVM):** Executes smart contracts.
**Mainnet vs Testnets:** Production vs development networks (Sepolia, Goerli).

**Documentation Links:**
- • [Ethereum Docs](https://ethereum.org/en/developers/docs/)
- • [EVM Overview](https://ethereum.org/en/developers/docs/evm/)

---

## Module 2 – Wagmi.sh (Nuxt 3 + Vue)

Wagmi provides React/Vue hooks for Ethereum. Works with viem for low-level blockchain calls.

**Installation:**
```bash
npm install @wagmi/core @wagmi/vue viem ethers
```

**Documentation Links:**
- • [Wagmi Docs](https://wagmi.sh/)
- • [viem Docs](https://viem.sh/)
- • [ethers.js Docs](https://docs.ethers.io/)

**Wallet Connection Example:**
```vue
<script setup>
import { useAccount, useConnect, useDisconnect } from '@wagmi/vue'
import { injected } from '@wagmi/connectors'

const { address, isConnected } = useAccount()
const { connect } = useConnect({ connector: injected() })
const { disconnect } = useDisconnect()
</script>
```

---

## Module 3 – Solidity Smart Contract Development

**Setup Hardhat:**
```bash
npm install --save-dev hardhat
npx hardhat
```

**Documentation Links:**
- • [Hardhat Docs](https://hardhat.org/getting-started/)
- • [Solidity Docs](https://docs.soliditylang.org/)
- • [OpenZeppelin Contracts](https://docs.openzeppelin.com/contracts/)

**ERC20 Token Example:**
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;
import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract MyToken is ERC20 {
    constructor() ERC20("MyToken", "MTK") {
        _mint(msg.sender, 1000 * 10 ** decimals());
    }
}
```

**Deploy Example:**
```bash
npx hardhat run scripts/deploy.js --network sepolia
```

---

## Module 4 – Solana Basics

**Solana vs Ethereum:** Rust vs Solidity, higher TPS.
**Tools:** Anchor (Rust framework), Solana-Web3.js (frontend integration)

**Documentation Links:**
- • [Solana Docs](https://docs.solana.com/)
- • [Anchor Docs](https://project-serum.github.io/anchor/)
- • [Solana Web3.js Docs](https://solana-labs.github.io/solana-web3.js/)

---

## Module 5 – Mempool

**What is Mempool?** Temporary storage of pending transactions.

**Watch Pending Transactions (viem):**
```javascript
import { watchPendingTransactions } from 'viem'
watchPendingTransactions({ onTransactions: console.log })
```

**Documentation Links:**
- • [Ethereum JSON-RPC](https://eth.wiki/json-rpc/API)
- • [viem watchPendingTransactions](https://viem.sh/)

---

## Module 6 – NFTs (ERC721)

**ERC721 Basics:** Unique tokens (art, collectibles).
**Standard Functions:** ownerOf, tokenURI, safeTransferFrom, approve

**Documentation Links:**
- • [ERC721 Standard](https://eips.ethereum.org/EIPS/eip-721)
- • [OpenZeppelin ERC721](https://docs.openzeppelin.com/contracts/4.x/erc721)

**Mint Example:**
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;
import "@openzeppelin/contracts/token/ERC721/extensions/ERC721URIStorage.sol";

contract MyNFT is ERC721URIStorage {
    uint public tokenCount;

    constructor() ERC721("MyNFT", "MNFT") {}

    function mint(string memory _tokenURI) public {
        tokenCount++;
        _mint(msg.sender, tokenCount);
        _setTokenURI(tokenCount, _tokenURI);
    }
}
```

**Interact via Wagmi:**
```javascript
const { data } = useReadContract({
address: '0xNFTAddress',
abi: erc721ABI,
functionName: 'ownerOf',
args: [tokenId],
})
```

---

## Module 7 – ERC20 Tokens

**Standard Functions:**
- • totalSupply()
- • balanceOf(address)
- • transfer(address, amount)

**Documentation Links:**
- • [ERC20 Standard](https://eips.ethereum.org/EIPS/eip-20)

**Interacting via Wagmi:**
```javascript
const { data } = useReadContract({
address: '0xTokenAddress',
abi: erc20ABI,
functionName: 'balanceOf',
args: [address],
})
```

---

## Module 8 – Security Best Practices

- • Test on testnets first
- • Audit contracts before mainnet deploy
- • Use OpenZeppelin libraries for standard compliance
- • Never expose private keys in frontend code

---

## Module 9 – Deployment & PM2

**Install Node.js and PM2:**
```bash
sudo apt install nodejs
sudo su
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo npm install pm2 -g
```

**Ecosystem Configuration Example (`ecosystem.config.cjs`):**
```javascript
module.exports = {
apps: [
{
name: 'NuxtApp1',
port: '3000',
exec_mode: 'cluster',
instances: 'max',
script: './path/to/app1/.output/server/index.mjs'
},
{
name: 'NuxtApp2',
port: '4000',
exec_mode: 'cluster',
instances: 'max',
script: './path/to/app2/.output/server/index.mjs'
}
]
}
```

**PM2 Commands:**
```bash
pm2 start ecosystem.config.cjs
pm2 list
pm2 stop NuxtAppName
pm2 restart NuxtAppName
pm2 logs NuxtAppName
```

**Start App with Specific Port:**
```bash
PORT=7777 pm2 start ipx-server.mjs
```

---

## Module 10 – Basic Linux Setup, Firewall & Certbot

**Update & Upgrade System:**
```bash
sudo apt update && sudo apt upgrade -y
```

**Firewall (UFW) Setup:**
```bash
sudo ufw allow OpenSSH
sudo ufw allow 'Nginx Full'
sudo ufw enable
sudo ufw status
```

**Check Logs:**
```bash
sudo journalctl -xe
sudo tail -f /var/log/syslog
```

**Install Certbot for SSL:**
```bash
sudo apt install certbot python3-certbot-nginx -y
sudo certbot --nginx -d your_domain.com -d www.your_domain.com
sudo systemctl status certbot.timer
```

**Renew SSL Automatically:**
```bash
sudo certbot renew --dry-run
```

**Documentation Links:**
- [UFW Docs](https://help.ubuntu.com/community/UFW)
- [Certbot Docs](https://certbot.eff.org/docs/)
- [Nginx Docs](https://nginx.org/en/docs/)

---

## Conclusion

Web3 combines blockchain, smart contracts, and decentralized architecture to give developers the ability to build secure, scalable, and censorship-resistant applications.\
Using Wagmi, viem, ethers, and Solidity, you can create ERC20 tokens, ERC721 NFTs, integrate with the mempool, and deploy your Nuxt apps with PM2 and Nginx.\
Master these technologies to be ready for the next wave of decentralized innovation.

— Written by towfik ahmed shimul
