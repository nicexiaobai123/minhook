# minhook
minhook的lib和头文件以及使用方法

# 引入头文件和lib库
#include "MinHook.h"
#pragma comment(lib, "libMinHook.x64.lib")
#pragma comment(lib, "libMinHook.x86.lib")

# 初始化与开启hook
BOOL Stat;
LPVOID pfn = GetProcAddress(LoadLibraryA("Ole32.dll"), "CoCreateInstance");
if (MH_Initialize() == MB_OK)
{
	MH_CreateHook(pfn, &CoCreateInstanceHook, reinterpret_cast<void**>(&g_pOldCoCreateInstance));
	MH_EnableHook(pfn);
}

# 停止hook与卸载
MH_DisableHook(pfn);
MH_Uninitialize();
