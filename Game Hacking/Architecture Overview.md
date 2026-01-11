### **Bitness and Data Width**

- **x86 = 32-bit:**
    - Uses 32-bit registers and memory addresses.
    - Addressable memory space: **4 GB** (2³²).
    - Instructions use the `EAX`, `EBX`, etc., registers.
- **x64 = 64-bit:**
    - Uses 64-bit registers and memory addresses.
    - Addressable memory space: **16 exabytes** (theoretical limit of 2⁶⁴).
    - Backward compatible with x86 in most OSes.
    - Registers prefixed with `R` (e.g., `RAX`, `RBX`).

> Note: When reverse engineering or writing cheats, you must know whether the target binary is 32-bit or 64-bit — you can’t inject a 64-bit DLL into a 32-bit game, and vice versa.

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/21-x86x64-architecture-overview#user-content-register-comparison-table)**Register Comparison Table**

|Purpose|32-bit (x86)|64-bit (x64)|
|---|---|---|
|Accumulator|EAX|RAX|
|Base|EBX|RBX|
|Counter|ECX|RCX|
|Data|EDX|RDX|
|Stack Pointer|ESP|RSP|
|Base Pointer|EBP|RBP|
|Source Index|ESI|RSI|
|Destination Index|EDI|RDI|
|Instruction Pointer|EIP|RIP|

**x64 Additional Registers:**  
R8–R15 are additional general-purpose registers introduced in x64, offering more flexibility and faster calling conventions (as more parameters are passed in registers).

### **Practical Tip: Identifying Architecture of a Game**

To determine if a game is 32-bit or 64-bit:

- Open the executable in **PE-bear**, **CFF Explorer**, or **IDA Free**.
- Check the **machine type** field in the PE header:
    - `0x14C` = x86 (32-bit)
    - `0x8664` = x64 (64-bit)

In Windows Task Manager:

- 32-bit programs will show as `game.exe *32`