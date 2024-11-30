# Kill or Pass: Game Design and Layout

## 1. Dealer System

### Role of the Dealer
- The **dealer** acts as the host of the game and is the primary authority for:
  - Setting up the table.
  - Ensuring anti-cheat measures.
  - Managing payouts to players.
  - Synchronizing player data (money and actions).

### Dealer Incentive
- Dealers receive **1-10% of winnings**, configurable via server settings.
- Dealers are **Trusted Dealers** and undergo a vetting process.
- Dealers maintain fairness and accountability:
  - Ensure no player cheats.
  - Confirm accurate payouts.
  - Prevent fraudulent actions.

### Dealer Application
- Only distributed to **trusted individuals**.
- Applications have **strict limits** on availability.
- Dealers are identified by a unique **dealer ID** and public key.

---

## 2. Server/Network Structure

### Node.js Server
- The dealer runs a lightweight **Node.js server** that:
  - Handles game state synchronization.
  - Implements anti-cheat mechanisms (e.g., action validation, hashed data).
  - Tracks player bets, actions, and eliminations.
  - Manages payouts and game results.

### Player Access
- Players join the game via a **unique website link**.
  - No installation required—just a browser.
  - The link directly connects to the dealer's Node.js server.
  - Example: `http://dealer123.killorpass.com/gameID`

---

### No Central Server
- To avoid costs and complexity:
  - The game uses a **decentralized mesh network of dealers**.
  - Each dealer maintains a local ledger of player data (money and status).
  - Dealers communicate with one another to synchronize player data:
    - Player money is hashed with their name for secure identification.
    - Updates propagate through active dealers in the network.

---

## 3. Data Persistence

### Mesh Network of Dealers
- Dealers act as a **distributed database**, ensuring persistent player data.
- Data includes:
  - Player name.
  - Current balance.
  - Betting history (if required for audits).

### Hashing for Security
- Player balances are hashed with their usernames:
  - Example: `hash(player_name + balance)` ensures:
    - Integrity of data.
    - Easy verification between dealers.

### Backup System
- Dealers periodically push hashed data to a **GitHub repository** as a nightly backup.
- GitHub repository serves as:
  - A backup for recovery.
  - A public ledger for transparency.

---

## 4. Anti-Cheat System

### Dealer Responsibilities
- Dealers verify all player actions:
  - Validate bets.
  - Check the legitimacy of shots (e.g., no illegal targeting).
  - Ensure payouts match game outcomes.
- Anti-cheat scripts are part of the dealer's Node.js server:
  - Detect anomalies in gameplay or betting behavior.
  - Log suspicious activity for auditing.

### Trust Model
- Dealers are bound by a **code of conduct**.
- Misconduct (e.g., cheating or failing to pay winnings) leads to revocation of dealer privileges:
  - Public blacklist of offending dealer IDs.

---

## 5. Gameplay Flow Update

### Joining a Game
1. Player visits the dealer's game link (e.g., `http://dealer123.killorpass.com/gameID`).
2. The browser connects to the dealer’s Node.js server.
3. Player enters their name (hashed for tracking) and balance.

### Gameplay
- Game follows the existing flow:
  - Players place bets.
  - Players take turns (shoot someone or the air).
  - Dealer resolves actions and updates the game state.

### Payout and Data Sync
1. At the end of the game:
   - Dealer calculates payouts and distributes winnings.
   - Updates the player's balance in the dealer's ledger.
2. Player data is hashed and synchronized across the mesh network.
3. Data is backed up to GitHub nightly.

---

## 6. Flow Chart

```plaintext
Start Game
  ↓
Dealer Sets Up Table
   ↓
Player Joins via Link
   ↓
Game Starts
   ↓
Players Place Bets
   ↓
Players Take Turns
   ├── Shoot Someone
   └── Shoot the Air
   ↓
Dealer Resolves Actions
   ├── Updates Game State
   └── Eliminates Players
   ↓
Final Player Wins
   └── Dealer Distributes Winnings
   ↓
Player Data Updated
   ├── Dealer Syncs Data with Mesh Network
   └── Backup to GitHub
```

---

## 7. Challenges and Solutions

### Challenge 1: Decentralized Mesh Network
- **Problem:**  
  Dealers may not always be online, disrupting synchronization.

- **Solution:**  
  1. Active dealers periodically broadcast the latest ledger updates to other online dealers.  
  2. Nightly backups to GitHub ensure data integrity even if a dealer goes offline.

---

### Challenge 2: Anti-Cheat Enforcement
- **Problem:**  
  Ensuring all dealers adhere to rules.

- **Solution:**  
  1. Trusted Dealer vetting process ensures only reliable individuals get access.  
  2. Public audits and reports of misconduct deter abuse.

---

## 8. Advantages of This System

1. **Cost-Effective:** No central server, leveraging dealers as distributed hosts.  
2. **Scalable:** New dealers can join the network, increasing capacity.  
3. **Secure:** Player data is hashed and validated across multiple dealers.  
4. **Transparent:** Public GitHub ledger ensures fairness and accountability.
