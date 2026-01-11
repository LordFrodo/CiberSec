**Cheat Engine (CE)** is a powerful open-source tool used to scan, modify, and analyze the memory of running processes. It is the standard entry point for beginners and professionals learning about memory hacking.

In this topic, you'll:

- Learn how to install and configure Cheat Engine.
- Use CE to scan and modify memory.
- Understand scanning types (exact, fuzzy, pointer).
- Learn how to attach to a game like **AssaultCube**.
- Explore trainers, breakpoints, and basic debugging.

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/14-introduction-to-cheat-engine-and-memory-scanning#user-content-141-installing-cheat-engine)**1.4.1 Installing Cheat Engine**

Download from the official source:  
👉 [https://cheatengine.org](https://cheatengine.org/)
Tutorial: [https://wiki.cheatengine.org/index.php?title=Tutorials:Cheat%5FEngine%5FTutorial%5FGuide%5Fx64](https://wiki.cheatengine.org/index.php?title=Tutorials:Cheat%5FEngine%5FTutorial%5FGuide%5Fx64)

> **Important:** Decline any bundled software during installation.

**Configuration:**

- Run CE as administrator.
- Enable “Read/Write Process Memory” options.
- Disable signature scanning if testing undetected cheats later.

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/14-introduction-to-cheat-engine-and-memory-scanning#user-content-142-basic-terminology)**1.4.2 Basic Terminology**

|Term|Definition|
|---|---|
|Scan|Searching game memory for a value (e.g. health = 100)|
|Pointer|An address that holds the location of another value|
|Trainer|A small tool (often EXE) that modifies memory automatically|
|Freeze|Locking a value in memory to prevent it from changing|
|Debugger|A tool to step through instructions and watch memory access|

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/14-introduction-to-cheat-engine-and-memory-scanning#user-content-143-connecting-to-a-process)**1.4.3 Connecting to a Process**

**Steps to attach to a game:**

1. Launch the game (e.g., **AssaultCube**).
2. Launch Cheat Engine.
3. Click the **Process Icon** (top-left).
4. Select `ac_client.exe`.
5. Click "Open" to attach.

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/14-introduction-to-cheat-engine-and-memory-scanning#user-content-144-performing-an-exact-value-scan)**1.4.4 Performing an Exact Value Scan**

Use this when you know the in-game value (e.g., Health = 100).

**Example (Health):**

1. Type `100` in the "Value" field.
2. Click "First Scan".
3. Take damage in game.
4. Enter new health value (e.g., `87`) and click "Next Scan".
5. Repeat until 1–3 addresses remain.
6. Double-click address to move to bottom.
7. Edit or freeze value.

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/14-introduction-to-cheat-engine-and-memory-scanning#user-content-145-unknown-value-scan-fuzzy-search)**1.4.5 Unknown Value Scan (Fuzzy Search)**

Used when you **don’t know the exact value**, but know that it changed.

**Example (Speed or State Flag):**

1. Set scan type to “Unknown initial value”.
2. Click "First Scan".
3. Move character or trigger action.
4. Choose "Increased/Decreased/Changed/Unchanged".
5. Repeat scanning to narrow down.

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/14-introduction-to-cheat-engine-and-memory-scanning#user-content-146-pointer-scanning)**1.4.6 Pointer Scanning**

Many game variables (e.g., player health) are stored in **dynamic memory**. The address changes on each restart. To make a **trainer** or reliable cheat, you need the **base pointer**.

**Steps:**

1. Find the correct dynamic address.
2. Right-click > “Pointer Scan for this address”.
3. Save results and reboot game.
4. Reattach to process and **rescan for pointer**.

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/14-introduction-to-cheat-engine-and-memory-scanning#user-content-147-multi-level-pointers)**1.4.7 Multi-Level Pointers**

Games often use pointer chains like:

```
[GameModule.dll+0x0032A4B0] → +0x0 → +0x14 → Health
```

Use CE to:

- Find static base pointer (`green` address).
- Add offsets manually in CE.

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/14-introduction-to-cheat-engine-and-memory-scanning#user-content-148-code-injection-and-debugger-basics)**1.4.8 Code Injection and Debugger Basics**

You can use CE to:

- Inject custom assembly instructions.
- Set breakpoints on memory writes.
- Modify function behavior (e.g., infinite ammo).

**Steps (Auto-Assembler):**

1. Right-click an instruction → “Find out what writes to this address”.
2. CE breaks on code that modifies value.
3. Use **"Replace with NOP"** (No Operation) to disable function.

```asm
// Original
mov [eax+04],edx

// Cheat (disable write)
nop
nop
```

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/14-introduction-to-cheat-engine-and-memory-scanning#user-content-149-creating-a-simple-trainer)**1.4.9 Creating a Simple Trainer**

CE allows you to generate standalone trainers:

- Right-click your found value.
- Choose “Add to Cheat Table”.
- Right-click again → “Generate Trainer”.
- You can export as `.EXE`.

> Trainers can be customized with scripts, hotkeys, and even GUIs.

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/14-introduction-to-cheat-engine-and-memory-scanning#user-content-1410-anti-cheat-detection)**1.4.10 Anti-Cheat Detection**

Be aware:

- VAC, EAC, BattlEye and others may detect CE.
- Running CE on online games can lead to bans.
- **Use CE in offline or lab environments only.**

### **1.7.8 Real Cheat Example: Infinite Ammo**

1. Start game, fire weapon, note ammo (e.g., 20).
2. First Scan `20`, shoot again, Next Scan `19`.
3. Narrow results and freeze value.

To make a better cheat:

- Use debugger to find instruction that decreases ammo
- Replace the instruction with NOP (`No Operation`)

**Assembly Example:**

```asm
sub [eax+18], 1   ; subtract 1 from ammo
↓
nop
nop
```

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/17-working-with-cheat-engine-for-real-time-hacking#user-content-179-saving-your-cheat-table)**1.7.9 Saving Your Cheat Table**

After finding reliable addresses or pointers:

1. Click **File → Save As** in CE
2. Save as `.CT` (Cheat Table)
3. Next time, load it directly with the game

You can also write **scripts** in CE using **Auto Assembler** to automate your patches.