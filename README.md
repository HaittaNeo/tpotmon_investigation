# TPOTMON Investigation Report

### Maintained by: @HaittaNeo (aka Neo@VTuber~$ 😈🛜 Exploit Hunter)

---

## 🕵️ Overview
This investigation was conducted to validate or refute community concerns regarding the website [tpotmon.com](https://tpotmon.com) and its possible association with cryptocurrency or blockchain activity, unauthorized data harvesting, and AI-generated content.

I examined the **entire source code**, both **frontend and backend**, performed **network traffic interception**, and analyzed **social proof** of potential affiliations. This repository documents each method and all findings with clarity and neutrality.

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

**Confirmed via multiple sources and backend review:**

- The **card descriptions** (`abilityDescription`, `attackDescription`, `description`) all exhibit language structure, humor, and coherence consistent with LLMs like ChatGPT
- **Backend logic in `/src/routes/create.ts`** processes incoming usernames and builds these fields dynamically

### 🧠 How We Know It's Using ChatGPT

Although the backend doesn’t show an *explicit* API key or endpoint like `api.openai.com/v1/completions`, here’s how we know it's LLM-generated:

1. **Backend File Observations**  
   In the `create.ts` logic, text strings are composed dynamically and structured in ways that suggest use of a language model:
   - Highly contextual personality descriptions
   - Consistent syntax and tone
   - No canned template usage — it's too dynamic to be hardcoded

2. **Dev Livestream Confirmation**  
   In public livestream footage, the developer:
   - Shows code referencing **prompt planning**
   - Discusses **ChatGPT outputs**
   - Indicates testing of prompts for generating card text

3. **No OpenAI Reference in Network Logs**  
   Our deep MITM traffic inspection (using `mitmproxy`, `curl`, and header logging) found:
   - No request to OpenAI’s servers
   - No external AI proxy URLs
   - Meaning all LLM use is **done server-side**, unseen by the browser

4. **Frontend `create()` call returns AI-style content**  
   Here’s a sample returned from the `/create` POST request:

   ```json
   {
     "attackName": "Cookie Dough Confession",
     "attackDescription": "Neo@VTuber~$ admits to liking it raw, but we're all just here for the crumbs of humor.",
     "abilityName": "Ego Shield",
     "abilityDescription": "Boosts self-esteem by 20% every time someone acknowledges your existence."
   }
   ```

---

## 💰 Cryptocurrency Link

### 🎯 Public Token Listing
- **Token:** [$TPOTMON on Solana](https://pump.fun/coin/GngkvJ21n9AJwYPRB7GPwEhs9nxqfExZVwQn4ppYpump)
- **Platform:** [pump.fun](https://pump.fun)
- **Token Address:** `GngkvJ21n9AJwYPRB7GPwEhs9nxqfExZVwQn4ppYpump`
- **Decimals:** 6
- **First Mint:** April 12, 2025 @ 22:52 UTC
- **Current Stats (at time of writing):**
  - Market Cap: ~$39,960.43
  - Holders: 371
  - Volume: Active daily
- Token classified as a **meme coin**, typical of pump.fun trends

![Pump.fun Token](https://github.com/HaittaNeo/tpotmon_investigation/blob/main/images/pumpfun.png)

---

### 🧠 Developer Ties & Live Stream Evidence

Multiple **cross-referenced elements** show that the creator of tpotmon.com is very likely the **creator of the $TPOTMON token**:

| Evidence | Description |
|---------|-------------|
| 🖥️ Terminal Screenshot | Live stream footage shows the dev terminal as `kion@McWeebies` |
| 🧠 ChatGPT past conversations | During a coding stream you can see in the sidebar of ChatGPT it includes phrases like “Making meme token on Solana” |
| 🔁 Timing | Token creation occurred **in parallel** with the public launch of the website |

---

### 🧩 Is the Token Required for the Site?

No. The site works **independently** of the token:

- There is **no wallet login**
- No minting, staking, or blockchain connection
- No `web3.js`, `ethers.js`, or RPC traffic detected

However — the **viral card generation** drives **brand awareness**, which **increases interest in the token**. The pattern matches other meme token launches:

- Viral "game" → social buzz → token speculation
- Token exists **outside the site** but is clearly **influenced by its popularity**

This indirect relationship is **strategic**, even if not embedded in code.

---

### 🛑 Key Contradiction

Despite this clear connection, the site prominently states:

> “This project IS NOT ASSOCIATED with any crypto projects.”

That claim is misleading. While technically the card generator doesn’t use crypto — the **developer does**, and the **token name and timing are no coincidence**.


---

## 📢 Community Concerns

**Most cited issues from VTubers & artists:**

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

I conclude:

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

## 🛡️ Recommendations
- 🚫 Don’t connect wallets or send crypto
- ✅ Cards are safe if you’re comfortable with public data and LLM use

## 🧾 Credits
Investigation by **@HaittaNeo**

Tools used:
- `mitmproxy`, `curl`, `openssl`, `dig`
- `grep`, `zsh`, full `.zip` decompilation
- Social analysis from Twitter/X VTuber community

Contact: [@HaittaNeo](https://x.com/HaittaNeo)

📂 Repo: [tpotmon_investigation](https://github.com/HaittaNeo/tpotmon_investigation)

