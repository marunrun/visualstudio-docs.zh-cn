---
title: 注册自定义调试引擎 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debug engines, registering
ms.assetid: 9984cd3d-d34f-4662-9ace-31766499abf5
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9cf06e881034b980b8e40e095779007b3c7fa6f6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65703605"
---
# <a name="registering-a-custom-debug-engine"></a>注册自定义调试引擎
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

调试引擎必须在 COM 约定后将自身注册为类工厂，并通过 Visual Studio 注册表子项注册到 Visual Studio。  
  
> [!NOTE]
> 有关如何注册调试引擎的示例，请参阅 TextInterpreter 示例，该示例作为教程的一部分生成 [：使用 ATL COM 构建调试引擎](https://msdn.microsoft.com/9097b71e-1fe7-48f7-bc00-009e25940c24)。  
  
## <a name="dll-server-process"></a>DLL 服务器进程  
 通常，调试引擎在其自己的 DLL 中作为 COM 服务器实现。 这意味着，在 Visual Studio 可以访问之前，调试引擎必须向 COM 注册其类工厂的 CLSID。 然后，调试引擎必须自行向 Visual Studio 进行注册，以便建立任何属性 (也称为调试引擎支持) 指标。 为调试引擎写入 Visual Studio 注册表子项的度量值的选择取决于调试引擎支持的功能。  
  
 [用于调试的 SDK 帮助](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) 器不仅描述注册调试引擎所需的注册表位置;它还介绍了 dbgmetric 库，其中包含许多适用于 c + + 开发人员的有用函数和声明，使操作更容易。  
  
### <a name="example"></a>示例  
 下面是 TextInterpreter 示例中的一个典型示例 () 演示如何使用 `SetMetric` dbgmetric) 中的函数 (向 Visual Studio 注册调试引擎。 还会在 dbgmetric 中定义要传递的指标。  
  
> [!NOTE]
> TextInterpreter 是一个基本的调试引擎;它不实现，因此不会注册任何其他功能。 一个更完整的调试引擎可能有一个 `SetMetric` 或其等效的调用的完整列表，一个用于调试引擎支持的每个功能。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)   
 [SDK 调试帮助程序](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)   
 [教程：使用 ATL COM 构建调试引擎](https://msdn.microsoft.com/9097b71e-1fe7-48f7-bc00-009e25940c24)
