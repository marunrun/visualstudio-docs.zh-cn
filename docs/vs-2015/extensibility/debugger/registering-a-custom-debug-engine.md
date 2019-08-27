---
title: 注册的自定义调试引擎 |Microsoft Docs
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
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65703605"
---
# <a name="registering-a-custom-debug-engine"></a>注册自定义调试引擎
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

调试引擎必须将自身注册为 COM 约定的类工厂，以及通过 Visual Studio 注册通过 Visual Studio 注册表子项。  
  
> [!NOTE]
> 如何注册调试引擎的示例可以找到在 TextInterpreter 示例中，作为一部分生成[教程：生成调试引擎使用 ATL COM](https://msdn.microsoft.com/9097b71e-1fe7-48f7-bc00-009e25940c24)。  
  
## <a name="dll-server-process"></a>DLL 服务器进程  
 通常情况下，调试引擎 DLL 中实现其自身作为 COM 服务器。 这意味着，调试引擎必须类工厂的 CLSID 向 COM 注册 Visual Studio 才能访问它。 然后调试引擎必须自身注册 Visual Studio 自身建立任何属性 （也称为度量值） 调试引擎支持。 写入调试引擎的 Visual Studio 注册表子项的度量值的选择取决于调试引擎支持的功能。  
  
 [以便进行调试的 SDK 帮助程序](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)描述不仅注册表位置必须注册的调试引擎; 它还介绍了 dbgmetric.lib 库，其中包含大量有用的函数并声明C++，使开发人员操作更容易注册表。  
  
### <a name="example"></a>示例  
 以下是典型示例 （从 TextInterpreter 示例） 演示如何使用`SetMetric`函数 （从 dbgmetric.lib)，以注册 Visual Studio 调试引擎。 Dbgmetric.lib 中也定义了所传递的度量值。  
  
> [!NOTE]
> TextInterpreter 是一种基本的调试引擎;它不实现，并因此不会注册 — 任何其他功能。 更完整的调试引擎必须一整个系列`SetMetric`调用或其等效项，一个用于调试引擎的每个功能支持。  
  
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
 [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)   
 [用于调试的 SDK 帮助程序](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)   
 [教程：生成调试引擎使用 ATL COM](https://msdn.microsoft.com/9097b71e-1fe7-48f7-bc00-009e25940c24)
