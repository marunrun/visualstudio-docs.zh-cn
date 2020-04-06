---
title: 注册表达式赋值器 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluators, registering
ms.assetid: 236be234-e05f-4ad8-9200-24ce51768ecf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 600f7c8a2e2957cddf23ccc82b0872617e491940
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713195"
---
# <a name="register-an-expression-evaluator"></a>注册表达式赋值器
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 表达式赋值器 （EE） 必须将自己注册为具有 Windows COM 环境和 Visual Studio 的类工厂。 EE 设置为 DLL，以便将其注入调试引擎 （DE） 地址空间或 Visual Studio 地址空间，具体取决于实例化 EE 的实体。

## <a name="managed-code-expression-evaluator"></a>托管代码表达式赋值器
 托管代码 EE 作为类库实现，它是一个 DLL，它向 COM 环境注册自身，通常由对 VSIP 程序*regpkg.exe*的调用启动。 自动处理为 COM 环境编写注册表项的实际过程。

 主类的方法用 标记，<xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute>指示在 DLL 向 COM 注册时将调用该方法。 此注册方法（通常称为`RegisterClass`）执行在 Visual Studio 注册 DLL 的任务。 相应的`UnregisterClass`（用 标记<xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute>），撤消卸载 DLL`RegisterClass`时的效果。
与使用非托管代码编写的 EE 相同的注册表项;唯一的区别是没有帮助器功能，例如`SetEEMetric`为你做工作。 下面是注册和取消注册过程的示例。

### <a name="example"></a>示例
 以下函数显示了托管代码 EE 如何在 Visual Studio 中注册和注销自身。

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

## <a name="unmanaged-code-expression-evaluator"></a>非托管代码表达式赋值器
 EE DLL 实现`DllRegisterServer`在 COM 环境和可视化工作室中注册自己的功能。

> [!NOTE]
> 您可以在文件*dllentry.cpp*中找到 MyCEE 代码示例注册表代码 ，该代码位于 EnVSDK_MyCPkgs_MyCEE 下的 VSIP 安装中。

### <a name="dll-server-process"></a>DLL 服务器进程
 注册 EE 时，DLL 服务器：

1. 根据正常的 COM`CLSID`约定注册其类工厂。

2. 调用帮助器函数`SetEEMetric`向 Visual Studio 注册下表中显示的 EE 指标。 函数`SetEEMetric`和指标如下所示是*dbgmetric.lib*库的一部分。 有关详细信息[，请参阅 SDK 帮助器进行调试](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)。

    |指标|描述|
    |------------|-----------------|
    |`metricCLSID`|`CLSID`EE 级工厂|
    |`metricName`|EE 的名称作为可显示字符串|
    |`metricLanguage`|EE 旨在评估的语言的名称|
    |`metricEngine`|`GUID`使用此 EE 的调试引擎 （DE） 的|

    > [!NOTE]
    > 按`metricLanguage``GUID`名称标识语言，但选择该语言的参数是`guidLang`该语言`SetEEMetric`的参数。 当编译器生成调试信息文件时，它应该编写适当的`guidLang`文件，以便 DE 知道要使用的 EE。 DE 通常会向符号提供程序询问此语言`GUID`，该语言存储在调试信息文件中。

3. 通过在HKEY_LOCAL_MACHINE_SOFTWARE_微软_VisualStudio\\*X.Y*下创建密钥来向 Visual Studio 注册，其中*X.Y*是要注册的 Visual Studio 版本。

### <a name="example"></a>示例
 以下函数显示了非托管代码 （C++） EE 如何在 Visual Studio 中注册和注销自身。

```cpp
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
- [编写 CLR 表达式赋值器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [用于调试的 SDK 帮助器](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
