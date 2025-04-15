# TPOTMON Investigation Report

### Maintained by: @HaittaNeo (aka Neo@VTuber~$ 😈🛜 Exploit Hunter)

---

## 🕵️ Overview
This investigation was conducted to validate or refute community concerns regarding the website [tpotmon.com](https://tpotmon.com) and its possible association with cryptocurrency or blockchain activity, unauthorized data harvesting, and AI-generated content.

We examined the **entire source code**, both **frontend and backend**, performed **network traffic interception**, and analyzed **social proof** of potential affiliations. This repository documents each method and all findings with clarity and neutrality.

---

## 🔍 Key Questions Investigated

| Concern | Description |
|--------|-------------|
| **Crypto** | Is the site linked to a token, NFT, or blockchain project? |
| **Wallet Access** | Does the site attempt to connect to user wallets? |
| **Data Harvesting** | Is personal data sent to 3rd-party collectors? |
| **OpenAI API** | Does the site send requests to LLMs like ChatGPT? |
| **Generative AI** | Are card descriptions generated via AI? |
| **Obfuscation** | Is anything hidden, encrypted, or dynamic? |
| **Token Ownership** | Is the developer tied to $TPOTMON or pump.fun? |

---

## 📁 File System + Source Review

**Source Code Reviewed:**
- `tpotmon-cards-main.zip` (complete local project)
- Backend, frontend, static content, config files — **everything** included

**Frontend Technologies:**
- Static HTML + Vanilla JS (custom web component)
- No Web3 libraries (ethers.js, web3.js, walletconnect, etc.)
- Card rendering logic handled in `card-view.js` using `<tpotmon-card>`

**Backend Observations:**
- `src/` contains worker logic for `/check` and `/create`
- No usage of crypto APIs, token logic, or wallet hooks
- No calls to blockchain providers like Quicknode, Solana RPC, or Metaplex

**Code Snippet (Create Endpoint Schema):**
```json
{
  "id": 173960,
  "displayName": "Neo@VTuber~$ 😈🛜 Exploit Hunter",
  "userName": "haittaneo",
  "attackType": "roast",
  "resistType": "drama",
  "weaknessType": "thirst"
}
```

**AI Evidence:**
- Descriptive strings like `abilityDescription`, `attackDescription`, and `description` resemble LLM outputs
- Confirmed via dev stream using ChatGPT to craft card data
- No frontend `fetch()` to OpenAI, but AI generation is implied from:

**Visual Gags (not NFTs):**
- Images like `drama.png`, `thirst.png`, `roast.png` found in `/public/types`
- Used purely for card styling — no minting, contracts, or tokens involved

✅ **No evidence of Web3, crypto wallet hooks, NFT minting, or data exfiltration found in full source.**

---

## 🔬 Manual Network Inspection

### Tools Used:
- `curl` with MITM proxy
- `mitmproxy`, `mitmweb`
- `openssl s_client`, `dig` for DNS/TLS analysis

### Traffic Observed:
- `/check` and `/create` POST routes
- Static assets only (CSS, PNGs, JS)
- No calls to:
  - `solana.com`
  - `pump.fun`
  - `*.rpc.*`
  - wallet providers (Metamask, Phantom)

**Captured Result Sample:**
```bash
curl -x http://127.0.0.1:8084 https://tpotmon.com --insecure -v
# All traffic internal, no blockchain calls
```

✅ No Web3 calls, token transactions, wallet lookups, or fingerprinting observed.

---

## 💬 AI Generation and OpenAI Use

**Confirmed via multiple sources:**
- Card text clearly AI-generated
- No direct OpenAI API call visible in source
- Strong inference backend uses ChatGPT

![OpenAI Token Planning](https://user-images.githubusercontent.com/your-image-id/ai-token-chat.png)

⚠️ We can't detect OpenAI requests directly without backend logs — but context, naming, and dev behavior all confirm it.

---

## 💰 Cryptocurrency Link

### Public Token Listing:
- Token: [$TPOTMON on Solana](https://pump.fun/coin/GngkvJ21n9AJwYPRB7GPwEhs9nxqfExZVwQn4ppYpump)
- Minted via [pump.fun](https://pump.fun)
- Currently listed with holders and volume

### Developer Ties:
- Terminal shown on stream: `kion@McWeebies`
- ChatGPT topics include “Making Meme Token Solana”

![Dev ID Match](https://user-images.githubusercontent.com/your-image-id/kion-terminal.png)

⚠️ Developer’s own environment + project timeline show strong correlation to token origin.

---

## 📢 Community Concerns

**Most cited issues from VTubers & artists:**

![Concern Example](https://user-images.githubusercontent.com/your-image-id/concern1.png)
![Concern Example](https://user-images.githubusercontent.com/your-image-id/concern2.png)

| Concern | Status | Explanation |
|--------|--------|-------------|
| **Uses AI** | ✅ True | Confirmed via dev activity and file content |
| **Linked to Crypto** | ✅ Likely | Token exists and dev appears involved |
| **Wallet Harvesting** | ❌ False | No wallet logic, no crypto SDKs present |
| **NFT Minting** | ❌ False | Images used are humorous assets only |
| **Data Farming** | ❌ No Evidence | Only public Twitter usernames queried |
| **Deceptive Branding** | ⚠️ Yes | Site says “no crypto” yet token exists |

---

## 📘 Final Conclusion

After reviewing:
- ✅ Full source code (including backend, workers, and migration files)
- ✅ Local network traffic and DNS/TLS certs
- ✅ Live dev behavior and ChatGPT logs
- ✅ Public token metadata and chain state

We conclude:

### ✅ Technically Safe
- No wallet access, no Web3 injection
- No token mints or NFT integrations

### ⚠️ Ethically Misleading
- Strong evidence dev is the token creator
- Branding intentionally omits crypto ties
- Viral site likely fueling token indirectly

> If you're concerned about AI ethics or crypto integration — skip it.
> If you’re okay with parody content powered by AI, it’s likely safe.

---

## 📸 Notable Screenshots

| Context | Image |
|--------|-------|
| ChatGPT session | ![ChatGPT Sidebar](https://user-images.githubusercontent.com/your-image-id/chatgpt-sidebar.png) |
| Dev terminal ("kion@McWeebies") | ![Dev Terminal](https://user-images.githubusercontent.com/your-image-id/kion-terminal.png) |
| Token planning chat | ![AI Token Planning](https://user-images.githubusercontent.com/your-image-id/ai-token-chat.png) |

---

## 🛡️ Recommendations
- 🚫 Don’t connect wallets or send crypto
- ✅ Cards are safe if you’re comfortable with public data and LLM use
- 🧠 Share the truth and let people decide

## 🧾 Credits
Investigation by **@HaittaNeo**

Tools used:
- `mitmproxy`, `curl`, `openssl`, `dig`
- `grep`, `zsh`, full `.zip` decompilation
- Social analysis from Twitter/X VTuber community

Contact: [@HaittaNeo](https://x.com/HaittaNeo)

📂 Repo: [tpotmon_investigation](https://github.com/HaittaNeo/tpotmon_investigation)

