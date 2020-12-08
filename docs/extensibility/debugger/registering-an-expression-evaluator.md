---
title: 注册表达式计算器 |Microsoft Docs
description: 了解表达式计算器如何使用 Windows COM 环境和 Visual Studio 将自身注册为类工厂。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 8f26eddf7191ee4393dd2ca986fe7a1d2c3af9e2
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2020
ms.locfileid: "96847138"
---
# <a name="register-an-expression-evaluator"></a>注册表达式计算器
> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 表达式计算器 (EE) 必须使用 Windows COM 环境和 Visual Studio 将自身注册为类工厂。 EE 设置为 DLL，以便将其插入调试引擎 (DE) 地址空间或 Visual Studio 地址空间，具体取决于实例化 EE 的实体。

## <a name="managed-code-expression-evaluator"></a>托管代码表达式计算器
 托管代码 EE 实现为类库，类库是一个 DLL，它将自身注册到 COM 环境，通常通过调用 VSIP 程序 *regpkg.exe* 启动。 系统会自动处理编写 COM 环境的注册表项的实际过程。

 主类的方法标记有 <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute> ，这表示当使用 COM 注册 DLL 时，将调用方法。 此注册方法（通常称为 `RegisterClass` ）执行向 Visual Studio 注册 DLL 的任务。 `UnregisterClass`标记有) 的相应 (<xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute> `RegisterClass` 会撤消卸载 DLL 时的影响。
与用非托管代码编写的 EE 相同的注册表项;唯一的区别在于，不存在任何帮助程序函数，例如 `SetEEMetric` 来完成工作。 下面是注册和注销过程的示例。

### <a name="example"></a>示例
 下面的函数演示托管代码 EE 如何向 Visual Studio 注册和取消注册。

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

## <a name="unmanaged-code-expression-evaluator"></a>非托管代码表达式计算器
 EE DLL 实现 `DllRegisterServer` 函数以便向 COM 环境和 Visual Studio 注册自身。

> [!NOTE]
> 你可以在文件 dllentry 中找到 MyCEE 代码示例注册表代码，该文件位于 EnVSDK\MyCPkgs\MyCEE. 中的 VSIP 安装下 *。*

### <a name="dll-server-process"></a>DLL 服务器进程
 注册 EE 时，DLL 服务器：

1. 按正常的 COM 约定注册其类工厂 `CLSID` 。

2. 调用 helper 函数 `SetEEMetric` 以便向 Visual Studio 注册下表中所示的 EE 指标。 `SetEEMetric`下面指定的函数和度量值是 *dbgmetric* 库的一部分。 有关详细信息，请参阅 [SDK 帮助程序](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) 。

    |指标|描述|
    |------------|-----------------|
    |`metricCLSID`|`CLSID` EE 类工厂的|
    |`metricName`|可显示字符串形式的 EE 名称|
    |`metricLanguage`|用于评估 EE 的语言名称|
    |`metricEngine`|`GUID` (DE) 使用此 EE 的调试引擎|

    > [!NOTE]
    > `metricLanguage``GUID`按名称标识语言，但它是 `guidLang` 用于选择语言的的参数 `SetEEMetric` 。 当编译器生成调试信息文件时，它应写入适当的， `guidLang` 以便 DE 知道要使用哪种 EE。 DE 通常会要求符号提供程序提供此语言，该提供程序 `GUID` 存储在调试信息文件中。

3. 通过在 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudioX. Y 下创建键来注册 Visual Studio \\ *X.Y*，其中， *x* 是要向其注册的 Visual studio 版本。

### <a name="example"></a>示例
 以下函数说明了非托管代码 (c + +) EE 如何使用 Visual Studio 进行注册和注销。

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
- [编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [SDK 调试帮助程序](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
