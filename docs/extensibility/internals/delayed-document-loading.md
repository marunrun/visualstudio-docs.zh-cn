---
title: 文档加载延迟 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: fb07b8e2-a4e3-4cb0-b04f-8eb11c491f35
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 30a3b1ce88a3e6a8069053c6d9daa14230034b28
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67821827"
---
# <a name="delayed-document-loading"></a>文档加载延迟

当用户重新打开 Visual Studio 解决方案时，不会立即加载的大多数相关联的文档。 文档窗口框架创建处于挂起的初始化状态，并 （称为存根 （stub） 帧） 的占位符文档置于运行文档表 (RDT)。

您的扩展插件可能会导致项目文档不必要地加载的查询的文档中的元素之前加载，这可以用于 Visual Studio 增加总体内存占用量。

## <a name="document-loading"></a>文档加载

在用户访问该文档，例如通过选择窗口框架的选项卡时，完全初始化的存根 （stub） 框架和文档。 也可通过请求该文档的数据时，通过访问 RDT 直接以获取文档数据，或通过进行以下调用之一间接访问 RDT 扩展初始化文档：

- 窗口框架<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A>方法。

- 窗口框架<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>方法上的任何以下属性：

  - [__VSFPROPID.VSFPROPID_DocView](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_DocView>)

  - [__VSFPROPID.VSFPROPID_ViewHelper](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_ViewHelper>)

  - [__VSFPROPID.VSFPROPID_DocData](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_DocData>)

  - [__VSFPROPID.VSFPROPID_AltDocData](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_AltDocData>)

  - [__VSFPROPID.VSFPROPID_RDTDocData](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_RDTDocData>)

  - [__VSFPROPID.VSFPROPID_SPProjContext](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_SPProjContext>)

- 如果您的扩展插件使用托管的代码，不应调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.GetDocumentInfo%2A>除非确定文档未处于挂起的初始化状态，或者想要完全初始化后的文档。 此方法始终返回文档的原因是数据对象，如有必要创建它。 相反，应在调用的方法之一`IVsRunningDocumentTable4`接口。

- 如果您的扩展插件使用C++，可以将传递`null`不希望的参数。

- 你可以避免不必要的文档加载通过让其他属性之前让相关的属性之前调用以下方法之一：

  - <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> 使用[__VSFPROPID6。VSFPROPID_PendingInitialization](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID6.VSFPROPID_PendingInitialization>)。

  - <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentFlags%2A>。 此方法返回<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4>包括的值的对象[_VSRDTFLAGS4。RDT_PendingInitialization](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4.RDT_PendingInitialization>)如果文档尚未初始化。

当文档已加载订阅时已完全初始化文档引发 RDT 事件时，可以找出。 有两种可能：

- 如果事件接收器会实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents2>，您可以订阅<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents2.OnAfterAttributeChangeEx%2A>，

- 否则，您可以订阅<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnAfterAttributeChange%2A>。

下面的示例是假设文档访问方案：Visual Studio 扩展想要显示有关打开的文档的某些信息，例如编辑锁定计数和文档数据有关的内容。 枚举中 RDT 使用文档<xref:Microsoft.VisualStudio.Shell.Interop.IEnumRunningDocuments>，然后调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.GetDocumentInfo%2A>以便检索编辑锁计数和文档数据的每个文档。 如果文档处于挂起的初始化状态，则请求文档数据将会导致它不必要地初始化。

访问文档的更高效的方法是使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentEditLockCount%2A>可获取编辑锁计数，然后使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentFlags%2A>来确定文档是否已初始化。 如果不包括标志[_VSRDTFLAGS4。RDT_PendingInitialization](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4.RDT_PendingInitialization>)，该文档已初始化，并请求使用的文档数据<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentData%2A>不会导致任何不必要的初始化。 如果包括标志[_VSRDTFLAGS4。RDT_PendingInitialization](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4.RDT_PendingInitialization>)，该扩展应避免初始化文档后，才请求文档数据。 可以在中检测到此初始化`OnAfterAttributeChange(Ex)`事件处理程序。

## <a name="test-extensions-to-see-if-they-force-initialization"></a>测试以查看是否它们强制进行初始化的扩展

没有任何可见提示，以指示是否已初始化文档，因此它可能很难找到您的扩展插件强制初始化。 可以设置注册表项，简化验证，因为它会导致未完全初始化文本的每个文档的标题 *[存根]* 标题中。

在中**HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\14.0\BackgroundSolutionLoad**，请设置**StubTabTitleFormatString**到 *{0} [存根]* 。
