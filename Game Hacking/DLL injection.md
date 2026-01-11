### **1.6.4 Writing Your First DLL Hack**

```cpp
// DLLMain.cpp
#include <Windows.h>

DWORD WINAPI HackThread(HMODULE hModule)
{
    MessageBox(NULL, "DLL Injected Successfully!", "GameHack", MB_OK);

    // Your hack code goes here

    FreeLibraryAndExitThread(hModule, 0);
    return 0;
}

BOOL APIENTRY DllMain(HMODULE hModule, DWORD ul_reason_for_call, LPVOID lpReserved)
{
    if (ul_reason_for_call == DLL_PROCESS_ATTACH)
        CreateThread(nullptr, 0, (LPTHREAD_START_ROUTINE)HackThread, hModule, 0, nullptr);
    return TRUE;
}
```

**Compile as DLL (.dll)** using Visual Studio or MinGW.

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/16-introduction-to-process-injection-and-dll-hack-design#user-content-165-injecting-the-dll)**1.6.5 Injecting the DLL**

You can inject the DLL into a game like **AssaultCube** using tools such as:

#### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/16-introduction-to-process-injection-and-dll-hack-design#user-content-extreme-injector)**Extreme Injector**

- GitHub: [Extreme Injector](https://github.com/master131/ExtremeInjector)
- Simple GUI to select process and DLL
- Supports:
    - Standard, manual map injection
    - Delayed and stealth injection

**Steps:**

1. Launch the target game (AssaultCube).
2. Open Extreme Injector.
3. Select the game process.
4. Add your compiled DLL.
5. Click "Inject".

You should see your `MessageBox` pop up if successful.

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/16-introduction-to-process-injection-and-dll-hack-design#user-content-166-common-issues-during-injection)**1.6.6 Common Issues During Injection**

|Issue|Possible Cause|
|---|---|
|Injection fails silently|DLL not compiled as 32-bit/64-bit match|
|Game crashes after injection|Wrong calling convention, memory issues|
|MessageBox not shown|Thread not running, DLLMain failed|
|DLL rejected by game|Anti-cheat protection|

---

### [](https://redteamleaders.coursestack.com/courses/c0f369dc-356d-4362-8942-b5446e02164b/take/16-introduction-to-process-injection-and-dll-hack-design#user-content-167-safe-practice-environment)**1.6.7 Safe Practice Environment**

For learning and testing:

- Always inject into offline, open-source games like **AssaultCube**.
- Do not use injections in online, anti-cheat protected environments.
- Keep backups of original game executables.