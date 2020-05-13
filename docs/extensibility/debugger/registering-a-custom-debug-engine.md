---
title: 注册自定义调试引擎 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, registering
ms.assetid: 9984cd3d-d34f-4662-9ace-31766499abf5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fe6fb916810bc8a7e960a4723a6a7c7a6f0c1410
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713214"
---
# <a name="register-a-custom-debug-engine"></a>注册自定义调试引擎
调试引擎必须按照 COM 约定注册自己为类工厂，并通过 Visual Studio 注册表子键向 Visual Studio 注册。

> [!NOTE]
> 您可以在 TextInterpreter 示例中找到如何注册调试引擎的示例，该示例作为教程的一部分构建[：使用 ATL COM 构建调试引擎](https://msdn.microsoft.com/library/9097b71e-1fe7-48f7-bc00-009e25940c24)。

## <a name="dll-server-process"></a>DLL 服务器进程
 调试引擎通常在其自己的 DLL 中设置为 COM 服务器。 因此，调试引擎必须在 Visual Studio 访问之前将其类工厂的 CLSID 注册到 COM。 然后，调试引擎必须向 Visual Studio 注册自身，以建立调试引擎支持的任何属性（也称为指标）。 写入 Visual Studio 注册表子键的指标选择取决于调试引擎支持的功能。

 [用于调试的 SDK 帮助程序](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)不仅描述了注册调试引擎所需的注册表位置，还描述了调试引擎的注册表位置。它还描述了*dbgmetric.lib*库，该库包含许多有用的函数和声明，用于C++开发人员，使操作注册表更容易。

### <a name="example"></a>示例
 以下示例（从 TextInterpreter 示例）演示如何使用`SetMetric`函数（来自*dbgmetric.lib）* 向 Visual Studio 注册调试引擎。 正在通过的指标也在*dbgmetric.lib*中定义。

> [!NOTE]
> 文本解释器是一个基本的调试引擎;它不设置，因此不注册任何其他功能。 更完整的调试引擎将具有一个完整的`SetMetric`调用列表或其等效项，每个功能都针对调试引擎支持。

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
- [用于调试的 SDK 帮助器](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [教程：使用 ATL COM 构建调试引擎](https://msdn.microsoft.com/library/9097b71e-1fe7-48f7-bc00-009e25940c24)
