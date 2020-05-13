---
title: 如何：为 Windows 提供自动化 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], tool windows
- tool windows, automation
ms.assetid: 512ab2a4-7987-4912-8f40-8804bf66f829
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c8716fbaa56cdb77063597fd5e07f6e469cc86a0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707954"
---
# <a name="how-to-provide-automation-for-windows"></a>如何：为窗口提供自动化

您可以为文档和工具窗口提供自动化。 每当您想要使自动化对象在窗口中可用时，建议提供自动化，并且环境尚未提供现成的自动化对象，就像使用任务列表一样。

## <a name="automation-for-tool-windows"></a>工具窗口的自动化

环境通过返回标准<xref:EnvDTE.Window>对象（如以下过程所述）在工具窗口中提供自动化：

1. 使用__VSFPROPID<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>通过环境调用该方法[。VSFPROPID_ExtWindowObject](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_ExtWindowObject>)作为`VSFPROPID`参数获取`Window`对象。

2. 当调用方请求特定于 VSPackage 的自动化对象以访问工具窗口<xref:EnvDTE.Window.Object%2A>时，环境将`QueryInterface`调用`IExtensibleObject` <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>。 `IDispatch` 和`IExtensibleObject``IVsExtensibleObject`都提供了<xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject.GetAutomationObject%2A>一种方法。

3. 当环境调用传递`GetAutomationObject``NULL`方法时，通过传递特定于 VSPackage 的对象来响应。

4. 如果调用`QueryInterface``IExtensibleObject`并`IVsExtensibleObject`失败，则环境将调用`QueryInterface``IDispatch`。

## <a name="automation-for-document-windows"></a>文档窗口的自动化

标准<xref:EnvDTE.Document>对象也可以从环境中提供，尽管编辑器可以通过实现<xref:EnvDTE.Document>`IExtensibleObject`接口和响应`GetAutomationObject`来实现该对象。

此外，编辑器可以通过实现<xref:EnvDTE.Document.Object%2A>`IVsExtensibleObject`或`IExtensibleObject`接口提供通过方法检索的特定于 VSPackage 的自动化对象。 [VSSDK 示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)提供特定于 RTF 文档的自动化对象。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>
