---
title: 注册的自定义调试引擎 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, registering
ms.assetid: 9984cd3d-d34f-4662-9ace-31766499abf5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 90400a9bf750eb80e40d6558fed382e18e7824ef
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66316045"
---
# <a name="register-a-custom-debug-engine"></a>注册自定义调试引擎
调试引擎必须将自身注册为一个类工厂，以下 COM 约定，以及通过 Visual Studio 注册通过 Visual Studio 注册表子项。

> [!NOTE]
> 您可以找到举例说明如何注册在 TextInterpreter 示例中，作为一部分生成的调试引擎[教程：生成调试引擎使用 ATL COM](https://msdn.microsoft.com/library/9097b71e-1fe7-48f7-bc00-009e25940c24)。

## <a name="dll-server-process"></a>DLL 服务器进程
 调试引擎是通常设置在其自己的 DLL 中作为 COM 服务器。 在这种情况下，调试引擎必须注册类工厂的 CLSID COM Visual Studio 才能访问它。 然后，调试引擎必须注册自身建立任何属性 （也称为度量值） 的 Visual Studio 调试引擎支持。 度量值写入到 Visual Studio 注册表子项的选择取决于调试引擎支持的功能。

 [用于调试的 SDK 帮助程序](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)介绍了不唯一的注册表位置必须注册的调试引擎; 它还介绍了*dbgmetric.lib*库，其中包含许多有用的功能和声明有关C++开发人员，使操作更容易注册表。

### <a name="example"></a>示例
 下面的示例 （摘自 TextInterpreter 示例） 演示如何使用`SetMetric`函数 (从*dbgmetric.lib*)，以注册 Visual Studio 调试引擎。 中也定义了所传递的指标*dbgmetric.lib*。

> [!NOTE]
> TextInterpreter 是一种基本的调试引擎;它未设置，并因此不会注册 — 任何其他功能。 更完整的调试引擎必须一整个系列`SetMetric`调用或其等效项，一个用于调试引擎的每个功能支持。

```
// Define base registry subkey to Visual Studio.
static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0";

HRESULT CTextInterpreterModule::RegisterServer(BOOL bRegTypeLib, const CLSID * pCLSID)
{
    SetMetric(metrictypeEngine, __uuidof(Engine), metricName, L"Text File", false, strRegistrationRoot);
    SetMetric(metrictypeEngine, __uuidof(Engine), metricCLSID, CLSID_Engine, false, strRegistrationRoot);
    SetMetric(metrictypeEngine, __uuidof(Engine), metricProgramProvider, CLSID_MsProgramProvider, false, strRegistrationRoot);

    return base::RegisterServer(bRegTypeLib, pCLSID);
}
```

## <a name="see-also"></a>请参阅
- [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)
- [用于调试的 SDK 帮助程序](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [教程：生成调试引擎使用 ATL COM](https://msdn.microsoft.com/library/9097b71e-1fe7-48f7-bc00-009e25940c24)