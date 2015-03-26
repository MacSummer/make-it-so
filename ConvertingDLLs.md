### Overview ###
The code for shared-objects libraries in gcc is simpler than the code for Windows DLLs. For example, Windows has a DllMain() function and DLL\_EXPORT declaration on functions. The code needed for a Windows DLL will not directly compile under gcc. So you have to do some conditional compilation to remove some of the extra stuff that Windows needs but gcc does not.

**DLL\_EXPORT**

You need to undefine DLL\_EXPORT for gcc builds. Include these lines before DLL\_EXPORT is used. For example in header files that declare exported functions:
```
#ifdef WIN32
    #undef DLL_EXPORT
    #define DLL_EXPORT __declspec(dllexport)
#else
    #undef DLL_EXPORT
    #define DLL_EXPORT 
#endif
```

**stdafx.h**

You do not need many (if any) of the things in stdafx.h, so you can conditionally only compile them under Windows. For example:
```
#ifdef WIN32

    // stdafx.h : include file for standard system include files,
    // or project specific include files that are used frequently, but
    // are changed infrequently
    //
    #include "targetver.h"

    #define WIN32_LEAN_AND_MEAN             // Exclude rarely-used stuff from Windows headers
    // Windows Header Files:
    #include <windows.h>

#endif
```

**dllmain.cpp**

You do not need the DllMain() function in gcc, so you can conditionally compile it only under Windows. For example:
```
#ifdef WIN32

BOOL APIENTRY DllMain( HMODULE hModule, DWORD ul_reason_for_call, LPVOID lpReserved)
{
    switch (ul_reason_for_call)
    {
    case DLL_PROCESS_ATTACH:
    case DLL_THREAD_ATTACH:
    case DLL_THREAD_DETACH:
    case DLL_PROCESS_DETACH:
        break;
    }
    return TRUE;
}

#endif
```