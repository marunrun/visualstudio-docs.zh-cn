---
title: 如何：为 Windows 提供自动化 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- automation [Visual Studio SDK], tool windows
- tool windows, automation
ms.assetid: 512ab2a4-7987-4912-8f40-8804bf66f829
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fec2b9ef6612a294dc70d129cf4bdd3dde843262
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905253"
---
# <a name="how-to-provide-automation-for-windows"></a>如何：为 windows 提供自动化

您可以为文档和工具窗口提供自动化功能。 无论何时需要使自动化对象在窗口中可用，并且环境尚未提供现成的自动化对象（与任务列表相同），都建议提供自动化。

## <a name="automation-for-tool-windows"></a>工具窗口自动化

环境通过返回标准 <xref:EnvDTE.Window> 对象（如以下过程中所述），对工具窗口提供自动化：

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>通过 __VSFPROPID 的环境调用方法[。VSFPROPID_ExtWindowObject](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_ExtWindowObject>)作为 `VSFPROPID` 参数以获取 `Window` 对象。

2. 当调用方为工具窗口请求 VSPackage 特定的自动化对象时 <xref:EnvDTE.Window.Object%2A> ，环境将调用 `QueryInterface` `IExtensibleObject` 、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject> 或 `IDispatch` 接口。 `IExtensibleObject`和都 `IVsExtensibleObject` 提供 <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject.GetAutomationObject%2A> 方法。

3. 然后，在环境调用通过的 `GetAutomationObject` 方法时 `NULL` ，通过传递回 VSPackage 特定的对象来做出响应。

4. 如果调用 `QueryInterface` `IExtensibleObject` 并 `IVsExtensibleObject` 失败，则环境将调用 `QueryInterface` `IDispatch` 。

## <a name="automation-for-document-windows"></a>文档窗口自动化

<xref:EnvDTE.Document>尽管编辑器可以 <xref:EnvDTE.Document> 通过实现 `IExtensibleObject` 接口并响应来拥有自己的对象实现，但也可以从环境中使用标准对象 `GetAutomationObject` 。

此外，编辑器还可以 <xref:EnvDTE.Document.Object%2A> 通过实现或接口，提供通过方法检索到的 VSPackage 特定的自动化对象 `IVsExtensibleObject` `IExtensibleObject` 。 [VSSDK 示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)提供了 RTF 文档特定的自动化对象。

## <a name="see-also"></a>另请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>
