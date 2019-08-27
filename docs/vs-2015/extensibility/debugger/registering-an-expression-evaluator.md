---
title: 注册表达式计算器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluators, registering
ms.assetid: 236be234-e05f-4ad8-9200-24ce51768ecf
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3595daa51fddf5c9c027d5643382918d85f83cc1
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63435679"
---
# <a name="registering-an-expression-evaluator"></a>注册表达式计算器
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 表达式计算器 (EE) 必须将自身注册为使用 Windows COM 环境和 Visual Studio 的类工厂。 EE 作为 DLL 实现，以便它可以注入到调试引擎 (DE) 地址空间或 Visual Studio 的地址空间，具体取决于实体实例化 EE。  
  
## <a name="managed-code-expression-evaluator"></a>托管的代码表达式计算器  
 托管的代码类库，这是一个 DLL，它向 COM 环境，通常通过 VSIP 计划，对的调用来启动注册自身作为实现 EE **regpkg.exe**。 自动处理实际编写 COM 环境的注册表项的过程。  
  
 主类的方法标记为<xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute>，指示正在 com 注册 DLL 时要调用方法 此注册方法中，通常称为`RegisterClass`，执行向 Visual Studio 注册该 DLL 的任务。 相应`UnregisterClass`(标有<xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute>)，撤消的影响`RegisterClass`卸载 DLL 时。  
  
 与非托管代码; 编写 EE 进行相同的注册表条目唯一的区别是，没有任何帮助器函数如`SetEEMetric`来完成工作。 此注册/取消注册过程的示例如下所示：  
  
### <a name="example"></a>示例  
 此函数显示托管的代码 EE 如何注册和注销本身与 Visual Studio。  
  
```csharp  
namespace EEMC  
{  
    [GuidAttribute("462D4A3D-B257-4AEE-97CD-5918C7531757")]  
    public class EEMCClass : IDebugExpressionEvaluator  
    {  
        #region Register and unregister.  
        private static Guid guidMycLang = new Guid("462D4A3E-B257-4AEE-97CD-5918C7531757");  
        private static string languageName = "MyC";  
        private static string eeName = "MyC Expression Evaluator";  
  
        private static Guid guidMicrosoftVendor = new Guid("994B45C4-E6E9-11D2-903F-00C04FA302A1");  
        private static Guid guidCOMPlusOnlyEng = new Guid("449EC4CC-30D2-4032-9256-EE18EB41B62B");  
        private static Guid guidCOMPlusNativeEng = new Guid("92EF0900-2251-11D2-B72E-0000F87572EF");  
  
        /// <summary>  
        /// Register the expression evaluator.  
        /// Set "project properties/configuration properties/build/register for COM interop" to true.  
        /// </summary>  
         [ComRegisterFunctionAttribute]  
        public static void RegisterClass(Type t)  
        {  
            // Get Visual Studio version (set by regpkg.exe)  
            string hive = Environment.GetEnvironmentVariable("EnvSdk_RegKey");  
            string s = @"SOFTWARE\Microsoft\VisualStudio\"  
                        + hive  
                        + @"\AD7Metrics\ExpressionEvaluator";  
  
            RegistryKey rk = Registry.LocalMachine.CreateSubKey(s);  
            if (rk == null)  return;  
  
            rk = rk.CreateSubKey(guidMycLang.ToString("B"));  
            rk = rk.CreateSubKey(guidMicrosoftVendor.ToString("B"));  
            rk.SetValue("CLSID", t.GUID.ToString("B"));  
            rk.SetValue("Language", languageName);  
            rk.SetValue("Name", eeName);  
  
            rk = rk.CreateSubKey("Engine");  
            rk.SetValue("0", guidCOMPlusOnlyEng.ToString("B"));  
            rk.SetValue("1", guidCOMPlusNativeEng.ToString("B"));  
        }  
        /// <summary>  
        /// Unregister the expression evaluator.  
        /// </summary>  
         [ComUnregisterFunctionAttribute]  
        public static void UnregisterClass(Type t)  
        {  
            // Get Visual Studio version (set by regpkg.exe)  
            string hive = Environment.GetEnvironmentVariable("EnvSdk_RegKey");  
            string s = @"SOFTWARE\Microsoft\VisualStudio\"  
                        + hive  
                        + @"\AD7Metrics\ExpressionEvaluator\"  
                        + guidMycLang.ToString("B");  
            RegistryKey key = Registry.LocalMachine.OpenSubKey(s);  
            if (key != null)  
            {  
                key.Close();  
                Registry.LocalMachine.DeleteSubKeyTree(s);  
            }  
        }  
    }  
}  
```  
  
## <a name="unmanaged-code-expression-evaluator"></a>非托管的代码表达式计算器  
 EE DLL 实现`DllRegisterServer`函数以将自身注册 COM 环境以及 Visual Studio。  
  
> [!NOTE]
> 可在文件 dllentry.cpp，它位于下 EnVSDK\MyCPkgs\MyCEE VSIP 安装 MyCEE 注册表的代码示例。  
  
### <a name="dll-server-process"></a>DLL 服务器进程  
 当注册 EE，DLL 服务器：  
  
1. 注册类工厂`CLSID`根据正常 COM 约定。  
  
2. 调用帮助器函数`SetEEMetric`若要通过 Visual Studio 注册以下表中所示的 EE 度量值。 该函数`SetEEMetric`和下面指定的指标是 dbgmetric.lib 库的一部分。 请参阅[以便进行调试的 SDK 帮助程序](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)有关详细信息。  
  
    |指标|描述|  
    |------------|-----------------|  
    |`metricCLSID`|`CLSID` EE 类工厂的|  
    |`metricName`|作为可显示字符串 EE 的名称|  
    |`metricLanguage`|EE 的语言名称旨在评估|  
    |`metricEngine`|`GUID`秒的处理此 EE 的调试引擎 (DE)|  
  
    > [!NOTE]
    > `metricLanguage``GUID`标识的名称，但它的语言是`guidLang`参数`SetEEMetric`选择语言。 当编译器生成调试信息文件时，它应编写相应`guidLang`以便 DE 知道要使用哪个 EE。 DE 通常会符号提供程序要求此语言`GUID`，它存储在调试信息文件。  
  
3. 注册 Visual Studio，通过创建密钥下 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\*X.Y*，其中*X.Y*是 Visual Studio 将注册到的版本。  
  
### <a name="example"></a>示例  
 此函数演示如何将非托管代码 (C++) EE 注册并使用 Visual Studio 中取消注册自身。  
  
```cpp#  
/*---------------------------------------------------------  
  Registration  
-----------------------------------------------------------*/  
#ifndef LREGKEY_VISUALSTUDIOROOT  
    #define LREGKEY_VISUALSTUDIOROOT L"Software\\Microsoft\\VisualStudio\\8.0"  
#endif  
  
static HRESULT RegisterMetric( bool registerIt )  
{  
    // check where we should register  
    const ULONG cchBuffer = _MAX_PATH;  
    WCHAR wszRegistrationRoot[cchBuffer];  
    DWORD cchFreeBuffer = cchBuffer - 1;  
    wcscpy(wszRegistrationRoot, LREGKEY_VISUALSTUDIOROOT_NOVERSION);  
    wcscat(wszRegistrationRoot, L"\\");  
  
    // this is Environment SDK specific  
    // we check for  EnvSdk_RegKey environment variable to  
    // determine where to register  
    DWORD cchDefRegRoot = lstrlenW(LREGKEY_VISUALSTUDIOROOT_NOVERSION) + 1;  
    cchFreeBuffer = cchFreeBuffer - cchDefRegRoot;  
    DWORD cchEnvVarRead = GetEnvironmentVariableW(  
        /* LPCTSTR */ L"EnvSdk_RegKey", // environment variable name  
        /* LPTSTR  */ &wszRegistrationRoot[cchDefRegRoot],// buffer for variable value  
        /* DWORD   */ cchFreeBuffer);// size of buffer  
    if (cchEnvVarRead >= cchFreeBuffer)  
        return E_UNEXPECTED;  
    // If the environment variable does not exist then we must use   
    // LREGKEY_VISUALSTUDIOROOT which has the version number.  
    if (0 == cchEnvVarRead)  
        wcscpy(wszRegistrationRoot, LREGKEY_VISUALSTUDIOROOT);  
  
    if (registerIt)  
    {  
        SetEEMetric(guidMycLang,  
                    guidMicrosoftVendor,  
                    metricCLSID,  
                    CLSID_MycEE,  
                    wszRegistrationRoot );  
        SetEEMetric(guidMycLang,  
                    guidMicrosoftVendor,  
                    metricName,  
                    GetString(IDS_INFO_MYCDESCRIPTION),  
                    wszRegistrationRoot );  
        SetEEMetric(guidMycLang,  
                    guidMicrosoftVendor,  
                    metricLanguage, L"MyC",  
                    wszRegistrationRoot);  
  
        GUID engineGuids[2];  
        engineGuids[0] = guidCOMPlusOnlyEng;  
        engineGuids[1] = guidCOMPlusNativeEng;  
        SetEEMetric(guidMycLang,  
                    guidMicrosoftVendor,  
                    metricEngine,  
                    engineGuids,  
                    2,  
                    wszRegistrationRoot);  
    }  
    else  
    {  
        RemoveEEMetric( guidMycLang,  
                        guidMicrosoftVendor,  
                        metricCLSID,  
                        wszRegistrationRoot);  
        RemoveEEMetric( guidMycLang,  
                        guidMicrosoftVendor,  
                        metricName,  
                        wszRegistrationRoot );  
        RemoveEEMetric( guidMycLang,  
                        guidMicrosoftVendor,  
                        metricLanguage,  
                        wszRegistrationRoot );  
        RemoveEEMetric( guidMycLang,  
                        guidMicrosoftVendor,  
                        metricEngine,  
                        wszRegistrationRoot );  
    }  
  
    return S_OK;  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)   
 [用于调试的 SDK 帮助程序](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
