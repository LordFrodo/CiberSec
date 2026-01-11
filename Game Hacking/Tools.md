| Tool         | Type    | Use Case                                     |
| ------------ | ------- | -------------------------------------------- |
| **IDA Free** | Static  | Precise function graph, automatic analysis   |
| **Ghidra**   | Static  | Decompiler and disassembler with annotations |
| **OllyDbg**  | Dynamic | Real-time analysis and instruction patching  |

> **Note:** Static = analyzing code without executing it; Dynamic = analysis during execution.

### **Loading a Game Binary**

#### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/23-analyzing-functions-in-ida-free-ghidra-or-ollydbg#user-content-ida-free--ghidra)**IDA Free / Ghidra**

1. Open the game’s `.exe` file.
2. Choose the correct architecture:
    - `x86` (32-bit) or `x86_64` (64-bit)
3. Let the tool auto-analyze functions.
4. Navigate to `start()` or `main()` or known entry point.
5. Use function graph to visualize control flow.

#### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/23-analyzing-functions-in-ida-free-ghidra-or-ollydbg#user-content-ollydbg)**OllyDbg**

1. Launch OllyDbg.
2. Attach or open the game process.
3. Press `F9` to run until code hits an entry point.
4. Use `Ctrl+G` to go to specific addresses.