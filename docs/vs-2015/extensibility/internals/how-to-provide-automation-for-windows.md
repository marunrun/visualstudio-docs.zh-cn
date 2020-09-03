---
title: 如何：为 Windows 提供自动化 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], tool windows
- tool windows, automation
ms.assetid: 512ab2a4-7987-4912-8f40-8804bf66f829
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7ea7b79df4e7f3748ec2bc7f5e57c6ecb7dfca5b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68191842"
---
# <a name="how-to-provide-automation-for-windows"></a>如何：提供适用于 Windows 的自动化
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

您可以为文档和工具窗口提供自动化功能。 无论何时需要使自动化对象在窗口中可用，并且环境尚未提供现成的自动化对象（与任务列表相同），都建议提供自动化。  
  
## <a name="automation-for-tool-windows"></a>工具窗口自动化  
 环境通过返回标准 <xref:EnvDTE.Window> 对象（如以下过程中所述），对工具窗口提供自动化：  
  
#### <a name="to-provide-automation-for-tool-windows"></a>为工具窗口提供自动化  
  
1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>通过环境调用方法 <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID> `VSFPROPID` 以获取 `Window` 对象。  
  
2. 当调用方为工具窗口请求 VSPackage 特定的自动化对象时 <xref:EnvDTE.Window.Object%2A> ，环境将调用 `QueryInterface` `IExtensibleObject` 、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject> 或 `IDispatch` 接口。 `IExtensibleObject`和都 `IVsExtensibleObject` 提供 <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject.GetAutomationObject%2A> 方法。  
  
3. 然后，在环境调用通过的 `GetAutomationObject` 方法时 `NULL` ，通过传递回 VSPackage 特定的对象来做出响应。  
  
4. 如果调用 `QueryInterface` `IExtensibleObject` 并 `IVsExtensibleObject` 失败，则环境将调用 `QueryInterface` `IDispatch` 。  
  
## <a name="automation-for-document-windows"></a>文档窗口自动化  
 <xref:EnvDTE.Document>尽管编辑器可以 `T:EnvDTE.Document` 通过实现 `IExtensibleObject` 接口并响应来拥有自己的对象实现，但也可以从环境中使用标准对象 `GetAutomationObject` 。  
  
 此外，编辑器还可以 <xref:EnvDTE.Document.Object%2A> 通过实现或接口，提供通过方法检索到的 VSPackage 特定的自动化对象 `IVsExtensibleObject` `IExtensibleObject` 。 [VSSDK 示例](../../misc/vssdk-samples.md)提供了 RTF 文档特定的自动化对象。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>
