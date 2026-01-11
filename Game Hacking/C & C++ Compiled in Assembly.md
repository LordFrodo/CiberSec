### **Why This Matters in Game Hacking**

When hacking games:

- You won’t see high-level code — only raw instructions.
- But understanding the **correlation** between C/C++ and assembly allows you to reverse engineer:
    - Health checks
    - Ammo logic
    - Position updates
    - Cooldowns
    - AI states

This knowledge enables you to patch logic, create cheats, or write memory scanners and trainers.

---

### [](https://courses.redteamleaders.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/24-understanding-compiled-cc-in-assembly#user-content-from-c-to-assembly-a-simple-example)**From C to Assembly: A Simple Example**

#### [](https://courses.redteamleaders.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/24-understanding-compiled-cc-in-assembly#user-content-c-code)**C Code**

```c
int health = 100;
if (health > 0) {
    take_damage(10);
}
```

#### [](https://courses.redteamleaders.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/24-understanding-compiled-cc-in-assembly#user-content-compiled-assembly-x86)**Compiled Assembly (x86)**

```asm
mov dword ptr [ebp-4], 64   ; health = 100 (0x64)
cmp dword ptr [ebp-4], 0    ; compare health > 0
jle skip_damage             ; jump if less/equal
push 0A                     ; push 10 as param
call take_damage            ; call function
skip_damage:
```

> You can recognize variables stored at `[ebp-4]` (local stack variable) and how conditional logic is compiled (`cmp`, `jle`, `call`).

---

### [](https://courses.redteamleaders.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/24-understanding-compiled-cc-in-assembly#user-content-understanding-function-calls)**Understanding Function Calls**

#### [](https://courses.redteamleaders.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/24-understanding-compiled-cc-in-assembly#user-content-c-code-1)**C Code**

```c
int result = add(5, 3);
```

#### [](https://courses.redteamleaders.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/24-understanding-compiled-cc-in-assembly#user-content-assembly-cdecl-x86)**Assembly (cdecl, x86)**

```asm
push 3
push 5
call add
mov [ebp-4], eax  ; store return value
```

#### [](https://courses.redteamleaders.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/24-understanding-compiled-cc-in-assembly#user-content-assembly-x64-calling-convention)**Assembly (x64 calling convention)**

```asm
mov ecx, 5        ; 1st param
mov edx, 3        ; 2nd param
call add
mov [rbp-4], eax
```

> Recognizing parameter passing helps identify functions like damage, movement, or input handlers.

---

### [](https://courses.redteamleaders.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/24-understanding-compiled-cc-in-assembly#user-content-loops-and-branching)**Loops and Branching**

#### [](https://courses.redteamleaders.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/24-understanding-compiled-cc-in-assembly#user-content-c-code-2)**C Code**

```c
for (int i = 0; i < 5; i++) {
    print(i);
}
```

#### [](https://courses.redteamleaders.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/24-understanding-compiled-cc-in-assembly#user-content-assembly)**Assembly**

```asm
mov dword ptr [ebp-4], 0   ; i = 0
loop_start:
cmp dword ptr [ebp-4], 5
jge loop_end
mov eax, [ebp-4]
push eax
call print
add dword ptr [ebp-4], 1   ; i++
jmp loop_start
loop_end:
```

> Loops become jumps and conditionals — you can patch them or find iteration-based logic (e.g., enemy spawning).

---

### [](https://courses.redteamleaders.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/24-understanding-compiled-cc-in-assembly#user-content-structures-and-object-layout)**Structures and Object Layout**

C++ classes and structs are flattened in memory:

```c
struct Player {
    int health;       // 0x00
    int ammo;         // 0x04
    float posX;       // 0x08
    float posY;       // 0x0C
};
```

#### [](https://courses.redteamleaders.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/24-understanding-compiled-cc-in-assembly#user-content-pointer-access)**Pointer Access**

```asm
mov eax, [ecx+0x04] ; access Player->ammo
```

> `ecx` usually holds the `this` pointer. Game objects like `Player`, `Vehicle`, `NPC` often follow this layout.

---

### [](https://courses.redteamleaders.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/24-understanding-compiled-cc-in-assembly#user-content-virtual-functions-and-vtables)**Virtual Functions and VTables**

In C++, virtual functions are implemented via **vtables** (virtual function tables). These are arrays of function pointers.

You’ll often see:

```asm
mov eax, [ecx]       ; get vtable pointer
mov eax, [eax+0x10]  ; get function from vtable
call eax             ; call virtual method
```

> You can hook or patch these calls for behavior like teleport, aim assist, etc.

---

### [](https://courses.redteamleaders.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/24-understanding-compiled-cc-in-assembly#user-content-recognizing-game-logic-patterns)**Recognizing Game Logic Patterns**

|Pattern|C/C++ Equivalent|Use in Game Hacking|
|---|---|---|
|cmp, jle|if/else conditions|Infinite health, god mode|
|mov, add, sub|arithmetic|Ammo, score, velocity hacks|
|call, push|function calls|Hooking/patching behavior|
|jmp, je, jne|control flow, logic branches|Skipping cooldowns or checks|

---

### [](https://courses.redteamleaders.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/24-understanding-compiled-cc-in-assembly#user-content-disassemblers-help-you-see-this)**Disassemblers Help You See This**

- **IDA Free** and **Ghidra** decompile to pseudo-C — helping you understand quickly.
- **OllyDbg** and **Cheat Engine Debugger** show exact instruction flow in memory.
- By recognizing these patterns, you’ll know **where** to patch and **what** to change.

---

### [](https://courses.redteamleaders.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/24-understanding-compiled-cc-in-assembly#user-content-real-case-finding-damage-function)**Real Case: Finding Damage Function**

You see this in disassembly:

```asm
mov eax, [esi+0xF8]   ; health
sub eax, ecx          ; take damage
mov [esi+0xF8], eax
```

Now you know:

- `esi` is player base
- `0xF8` = health offset
- `ecx` is damage amount

Patch `sub` to `nop nop` or set `eax = 999` for infinite health.

---

### [](https://courses.redteamleaders.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/24-understanding-compiled-cc-in-assembly#user-content-takeaways)**Takeaways**

- Assembly is the compiled truth of C/C++.
- Mastering patterns between C and disassembly helps you locate and alter game logic.
- You do not need to reverse _everything_ — just enough to find what to patch or read.