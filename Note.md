### 禁止同一台电脑同时启动同一个程序
```C++
CString   strMutexName;
strMutexName = "ZCCheck Tool";

m_hMutex = OpenMutex(MUTEX_ALL_ACCESS, FALSE, strMutexName);
if (m_hMutex == NULL)
{
	m_hMutex = ::CreateMutex(NULL, NULL, strMutexName);
}
else
{
	MessageBox(NULL, "已经有一个程序在运行....", "提示", MB_OK | MB_ICONINFORMATION);
	return FALSE;
}
```
---
### 创建线程
```C++
//线程函数
UINT CheckThread(LPVOID lpPara)
{

}

HANDLE      m_hThread;
DWORD       m_dwThread;
m_hThread = ::CreateThread(NULL, 0, (LPTHREAD_START_ROUTINE)CheckThread, (LPVOID)this, 0, &m_dwThread);
if (NULL == m_dwThread)
{
	AfxMessageBox("启动线程失败！");
}
```
---
### ini文件配置
```C++
获取配置文件路径
CString      g_strDLLDir;
CString      g_strWKDir;    //程序运行当前路径
::GetModuleFileName(NULL, g_strDLLDir.GetBuffer(_MAX_PATH), _MAX_PATH);
g_strDLLDir.ReleaseBuffer();
g_strDLLDir = g_strDLLDir.Left(g_strDLLDir.ReverseFind('\\'));
g_strWKDir = g_strDLLDir;

g_strDLLDir += "\\DLLConfig.ini";

//

```
