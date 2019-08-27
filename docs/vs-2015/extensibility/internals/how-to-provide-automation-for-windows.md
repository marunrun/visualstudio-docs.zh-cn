---
title: 如何：提供适用于 Windows 的自动化 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68191842"
---
# <a name="how-to-provide-automation-for-windows"></a>如何：提供适用于 Windows 的自动化
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

你可以提供文档和工具窗口的自动化。 提供自动化是建议您无论何时你想要使自动化对象在一个窗口，并在环境已不提供现成的自动化对象，方式与在任务列表。  
  
## <a name="automation-for-tool-windows"></a>自动化工具 Windows  
 通过返回一个标准工具窗口上环境提供自动化<xref:EnvDTE.Window>对象下面的过程中所述：  
  
#### <a name="to-provide-automation-for-tool-windows"></a>若要提供自动化的工具窗口  
  
1. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>方法通过使用环境<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>作为`VSFPROPID`参数，以获取`Window`对象。  
  
2. 当调用方请求特定于 VSPackage 的自动化对象通过工具窗口<xref:EnvDTE.Window.Object%2A>，环境调用`QueryInterface`有关`IExtensibleObject`， <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>，或`IDispatch`接口。 这两`IExtensibleObject`并`IVsExtensibleObject`提供<xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject.GetAutomationObject%2A>方法。  
  
3. 当环境然后调用`GetAutomationObject`方法并传递`NULL`，表示通过响应返回特定于 VSPackage 的对象。  
  
4. 如果调用`QueryInterface`有关`IExtensibleObject`并`IVsExtensibleObject`失败，则环境在调用`QueryInterface`为`IDispatch`。  
  
## <a name="automation-for-document-windows"></a>自动化文档 Windows  
 一种标准<xref:EnvDTE.Document>对象也是可从环境中，虽然编辑器可以有自己的实现`T:EnvDTE.Document`通过实现对象`IExtensibleObject`接口和响应的`GetAutomationObject`。  
  
 此外，编辑器可以提供特定于 VSPackage 的自动化对象，通过检索<xref:EnvDTE.Document.Object%2A>方法，通过实现`IVsExtensibleObject`或`IExtensibleObject`接口。 [VSSDK 示例](../../misc/vssdk-samples.md)有助于 RTF 特定于文档的自动化对象。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>
