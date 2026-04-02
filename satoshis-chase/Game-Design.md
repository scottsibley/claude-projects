# Game Design Document: Satoshi Chase
Project Code: SHAmory-MC-01
Lead Designer: Scott Sibley
Date: March 2026
Target Platform: Web (HTML5/Phaser 3) and Mobile Responsive

## 1. Executive Summary
Satoshi Chase is a high-speed branded arcade game featuring SHAmory
characters. Uses Pac-Man logic to create a competitive Mining environment.
Goal: collect all Satoshis (Bitcoin coins) while outmaneuvering Malware
enemies using strategic movement and power-ups.

## 2. Visual Assets and Branding
All assets are in the assets/ folder. Strictly adhere to SHAmory brand palette.

### 2.1 Protagonist: Glimmer (Purple Monster)
- File: assets/Satoshi.png
- Behavior: The Miner. Uses 4-way movement logic.
- Animations:
  - Walking: cycle Front, Back, Side profiles based on input direction
  - Mining: 2-frame mouth chomp animation when overlapping Satoshis
  - Boosted State: file assets/Satoshi-Boosted.png
    Apply pulsing golden aura (#FFBF00) and lens flare sparkle on sunglasses

### 2.2 Enemies: Malware (Red Monster Variants)
- File: assets/Enemy.png
- Behavior: The Threat. 4 variants, same base sprite, different color hexes.
- Colors: Teal, Blue, Orange, Red
- States:
  - Standard: moving with pickaxe held
  - Frightened: swap to Blue (#0E79B2) with Panic facial expression,
    pickaxe turns grey
  - Eaten: sprite becomes Eyes Only, moves at 200% speed to Center Pen

### 2.3 Environment and Collectibles
- Maze: Classic 1980 arcade layout. Walls: #0A2463
- Satoshi coins: file assets/Coins.png
  Gold coin (#FFBF00) with angled Bitcoin symbol
  Must include 2-frame shimmer loop (Standard vs Shimmer)
- Mining Boost (Power Pellet): large pulsing Golden Pickaxe icon in corners

## 3. Technical Specifications

### 3.1 Enemy AI Personality Logic
Each Malware character has a unique targeting script to prevent clumping:
1. Red (#FF6666): Direct Chase — targets player current X,Y
2. Teal (#00FDDC): Ambush — targets tile 4 units ahead of player direction
3. Blue (#0E79B2): Pincer — targets vector (playerpos + 2*heading) - RedMalwarepos
4. Orange (#FF9900): Chaos — chases if distance >8 tiles,
   retreats to bottom-left corner if distance <8 tiles

### 3.2 Controls
- Desktop: Arrow Keys (Up, Down, Left, Right)
- Mobile: Full-screen swipe listener
  - A swipe queues that turn direction
  - Miner executes turn at next available intersection
  - Minimum 30px displacement to register a swipe

## 4. Gameplay Loop and UI

### 4.1 Life and Death
- Lives: 3 total. Lost on contact with Malware.
- Reset: entities return to start, cleared Satoshis do NOT respawn
- Eaten Malware: must stay in Center Pen 3 seconds before re-entering

### 4.2 Levels and Difficulty
- Max Levels: 5
- Level 1: 100% speed
- Level 2: 105% speed
- Level 3: 110% speed
- Level 4: 115% speed
- Level 5: 120% speed

### 4.3 End States and UI
- Victory (Level 5 clear): "Genesis Block Mined!" screen with coin shower animation
- Game Over (0 lives): display final Hashrate (score)
- Leaderboard: Local Storage Top 10, prompt for 3-character alias entry

## 5. Audio
- Coin collection: Cha-Ching sound
- Power-up active: continuous low-frequency electronic hum
- Death: downward-pitch 8-bit slide

## Developer Checklist
- [ ] Implement Phaser 3 arcade physics
- [ ] Integrate 4-way orthographic sprite switching
- [ ] Code individual AI targeting scripts
- [ ] Verify Cha-Ching audio on every Satoshi overlap
- [ ] Test swipe gesture on iOS and Android browsers