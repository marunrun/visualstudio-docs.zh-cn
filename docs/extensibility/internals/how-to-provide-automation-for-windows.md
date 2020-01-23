---
title: 如何：为 Windows 提供自动化 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], tool windows
- tool windows, automation
ms.assetid: 512ab2a4-7987-4912-8f40-8804bf66f829
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f02860b76c80a05808d4e46f315fc3616a19f94f
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75848855"
---
# <a name="how-to-provide-automation-for-windows"></a>如何：为 windows 提供自动化

您可以为文档和工具窗口提供自动化功能。 无论何时需要使自动化对象在窗口中可用，并且环境尚未提供现成的自动化对象（与任务列表相同），都建议提供自动化。

## <a name="automation-for-tool-windows"></a>工具窗口自动化

环境通过返回标准 <xref:EnvDTE.Window> 对象（如以下过程中所述），在工具窗口上提供自动化：

1. 通过 __VSFPROPID 的环境调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> 方法[。VSFPROPID_ExtWindowObject](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_ExtWindowObject>)为获取 `Window` 对象 `VSFPROPID` 参数。

2. 当调用方通过 <xref:EnvDTE.Window.Object%2A>为工具窗口请求 VSPackage 特定的自动化对象时，环境将调用 `IExtensibleObject`、<xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>或 `IDispatch` 接口的 `QueryInterface`。 `IExtensibleObject` 和 `IVsExtensibleObject` 均提供 <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject.GetAutomationObject%2A> 方法。

3. 然后，环境调用传递 `NULL`的 `GetAutomationObject` 方法，通过传递回 VSPackage 特定的对象来做出响应。

4. 如果调用 `QueryInterface` 用于 `IExtensibleObject` 并且 `IVsExtensibleObject` 失败，则环境将为 `IDispatch`调用 `QueryInterface`。

## <a name="automation-for-document-windows"></a>文档窗口自动化

尽管编辑器可以通过实现 `IExtensibleObject` 接口并响应 `GetAutomationObject`来拥有自己的 <xref:EnvDTE.Document> 对象实现，但也可以从环境中获取标准 <xref:EnvDTE.Document> 对象。

此外，编辑器还可以通过实现 `IVsExtensibleObject` 或 `IExtensibleObject` 接口，提供通过 <xref:EnvDTE.Document.Object%2A> 方法检索到的 VSPackage 特定的自动化对象。 [VSSDK 示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)提供了 RTF 文档特定的自动化对象。

## <a name="see-also"></a>另请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>
