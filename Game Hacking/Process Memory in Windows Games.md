### **1.3.1 What Is Process Memory?**

When you launch a game (or any program), the operating system (Windows) assigns it a **process** and allocates **virtual memory**. This memory space contains:

- **Executable code**
- **Variables (health, ammo, score)**
- **Buffers and objects**
- **Loaded modules (DLLs, textures, assets)**

Each process has its own **virtual address space**, meaning:

- It cannot directly access memory from another process.
- Hackers must use system-level tools or permissions to inspect or alter that memory.

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/13-process-memory-in-windows-games#user-content-132-memory-layout-overview)**1.3.2 Memory Layout Overview**

A process typically contains these segments:

|Section|Description|
|---|---|
|.text|Executable code (functions, instructions)|
|.data|Static initialized data (e.g., global variables)|
|.bss|Static uninitialized data|
|**Heap**|Dynamically allocated memory (new, malloc)|
|**Stack**|Local variables, function call frames|
|**PE Headers**|Metadata about the binary format|
|**Modules**|DLLs and imported libraries (e.g., kernel32.dll)|

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/13-process-memory-in-windows-games#user-content-133-how-games-use-memory)**1.3.3 How Games Use Memory**

Games are dynamic. Their memory constantly changes as the game runs:

- Health increases/decreases
- Ammo depletes
- Positions are recalculated
- AI state changes

Games store these values in predictable structures:

- Player class or struct
- Enemy list
- Weapon data
- Position vectors

These are stored in memory addresses that you can scan for using tools like **Cheat Engine**.

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/13-process-memory-in-windows-games#user-content-134-accessing-another-processs-memory-windows-api)**1.3.4 Accessing Another Process’s Memory (Windows API)**

To manipulate a game's memory from an external process, you use the Windows API:

#### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/13-process-memory-in-windows-games#user-content-step-1-find-the-process-id)**Step 1: Find the Process ID**

```cpp
DWORD pid = GetProcessIdFromName("Game.exe");
```

#### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/13-process-memory-in-windows-games#user-content-step-2-open-the-process)**Step 2: Open the Process**

```cpp
HANDLE hProc = OpenProcess(PROCESS_ALL_ACCESS, FALSE, pid);
```

#### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/13-process-memory-in-windows-games#user-content-step-3-read-or-write-memory)**Step 3: Read or Write Memory**

```cpp
int value;
ReadProcessMemory(hProc, (LPCVOID)address, &value, sizeof(value), 0);

int newValue = 999;
WriteProcessMemory(hProc, (LPVOID)address, &newValue, sizeof(newValue), 0);
```

> Note: You must run your cheat or tool **as Administrator** or with **elevated permissions** to access protected memory.

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/13-process-memory-in-windows-games#user-content-135-cheat-engine-and-manual-memory-scanning)**1.3.5 Cheat Engine and Manual Memory Scanning**

**Cheat Engine (CE)** allows you to:

- Scan memory regions for specific values.
- Apply filters to narrow down.
- Modify values in-place.
- Inspect memory regions (e.g., heap vs stack).
- Attach to a process and freeze or change values.

**Example CE usage:**

1. Open Cheat Engine.
2. Attach it to `ac_client.exe` (AssaultCube).
3. Search for health value (e.g., 100).
4. Take damage, scan again.
5. Narrow until correct address is found.
6. Modify value or freeze it.

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/13-process-memory-in-windows-games#user-content-136-address-types)**1.3.6 Address Types**

Understanding types of addresses is vital.

|Type|Description|
|---|---|
|Static Address|Fixed in the binary (e.g., global variable)|
|Dynamic Address|Changes each run (e.g., player object pointer)|
|Pointer Address|An address that **points to another address**|
|Multi-Level Pointer|Chains of pointers used in dynamic memory allocation (common in modern games)|

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/13-process-memory-in-windows-games#user-content-137-pointer-and-multi-level-pointer-example)**1.3.7 Pointer and Multi-Level Pointer Example**

**Example**:  
Game allocates the player object dynamically:

```
0x01234F00 → points to → 0x0456A320 → points to → Player.health = 0x0456A324
```

This requires **pointer path traversal**, which Cheat Engine can resolve with **Pointer Scans**.

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/13-process-memory-in-windows-games#user-content-138-common-pitfalls)**1.3.8 Common Pitfalls**

- Memory changes constantly (use breakpoints or freezing if needed).
- Values may be **encrypted** or **obfuscated**.
- Anti-cheats may detect memory scanning or editing.
- 64-bit games use 64-bit addressing – handle sizes properly in C++.

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/13-process-memory-in-windows-games#user-content-139-memory-protection-flags)**1.3.9 Memory Protection Flags**

When accessing memory manually, it may be **read-protected**, **write-protected**, or **execute-only**.

```cpp
VirtualProtectEx(hProc, address, size, PAGE_READWRITE, &oldProtect);
```

This temporarily allows changes to protected memory.

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/13-process-memory-in-windows-games#user-content-key-takeaways)**Key Takeaways**

- Every game is a running process with memory regions you can scan, inspect, and manipulate.
- Use tools like Cheat Engine to identify values.
- Learn the Windows APIs for reading/writing memory safely.
- Understand how games dynamically allocate memory, especially in object-oriented engines.