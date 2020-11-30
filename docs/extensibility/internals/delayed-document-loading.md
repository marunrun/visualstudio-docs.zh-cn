---
title: 延迟的文档加载 |Microsoft Docs
description: 了解有关 Visual Studio 中延迟的文档加载的信息，以及如何编写扩展的代码，使其不在加载文档之前查询文档中的元素。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: fb07b8e2-a4e3-4cb0-b04f-8eb11c491f35
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c6489c819efe0fd29cd2d120c08414cf0532ad6f
ms.sourcegitcommit: 9ce13a961719afbb389fa033fbb1a93bea814aae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2020
ms.locfileid: "96328387"
---
# <a name="delayed-document-loading"></a>延迟的文档加载

当用户重新打开 Visual Studio 解决方案时，大多数关联的文档将不会立即加载。 文档窗口框架是在 "挂起初始化" 状态下创建的，占位符文档 (称为存根帧) 放置在正在运行的文档表中 (RDT) 。

扩展可能会导致不必要的情况下加载项目文档，方法是在加载文档之前查询文档中的元素，这会增加 Visual Studio 的总体内存占用量。

## <a name="document-loading"></a>文档加载

当用户访问文档时（例如，通过选择窗口框架的选项卡），将完全初始化存根（stub）框架和文档。 该文档还可以通过以下方式初始化：请求文档数据的扩展：通过直接访问 RDT 来获取文档数据，或通过进行以下调用之一间接访问 RDT：

- 窗口框架 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A> 方法。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>以下任何属性的窗口框架方法：

  - [__VSFPROPID。VSFPROPID_DocView](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_DocView>)

  - [__VSFPROPID。VSFPROPID_ViewHelper](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_ViewHelper>)

  - [__VSFPROPID。VSFPROPID_DocData](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_DocData>)

  - [__VSFPROPID。VSFPROPID_AltDocData](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_AltDocData>)

  - [__VSFPROPID。VSFPROPID_RDTDocData](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_RDTDocData>)

  - [__VSFPROPID。VSFPROPID_SPProjContext](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_SPProjContext>)

- 如果您的扩展插件使用托管代码，则不应调用， <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.GetDocumentInfo%2A> 除非您确定该文档未处于挂起初始化状态，或者您希望文档完全初始化。 原因是该方法始终返回 doc 数据对象，如有必要，创建它。 相反，应调用接口上的方法之一 `IVsRunningDocumentTable4` 。

- 如果扩展使用 c + +，则可以传递 `null` 不需要的参数。

- 在请求其他属性之前，您可以通过调用以下方法之一来避免不必要的文档加载：

  - <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> 使用 [__VSFPROPID6。VSFPROPID_PendingInitialization](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID6.VSFPROPID_PendingInitialization>)。

  - <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentFlags%2A>. 此方法返回一个 <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4> 对象，该对象包含一个 [_VSRDTFLAGS4 的值。](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4.RDT_PendingInitialization>) 如果文档尚未初始化，则 RDT_PendingInitialization。

您可以通过订阅 RDT 事件（在文档完全初始化时引发）来查看文档的加载时间。 有两种可能的原因：

- 如果事件接收器实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents2> ，则可以订阅 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents2.OnAfterAttributeChangeEx%2A> 、

- 否则，你可以订阅 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnAfterAttributeChange%2A> 。

下面的示例是一个假设的文档访问方案： Visual Studio 扩展需要显示有关打开的文档的一些信息，例如，编辑锁定计数和文档数据。 它使用枚举 RDT 中的文档 <xref:Microsoft.VisualStudio.Shell.Interop.IEnumRunningDocuments> ，然后对每个文档进行调用，以便 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.GetDocumentInfo%2A> 检索编辑锁定计数和文档数据。 如果文档处于挂起初始化状态，请求文档数据将导致其不必要地初始化。

访问文档的一种更有效的方法是使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentEditLockCount%2A> 来获取编辑锁计数，然后使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentFlags%2A> 来确定文档是否已初始化。 如果标志不包含 [_VSRDTFLAGS4。RDT_PendingInitialization](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4.RDT_PendingInitialization>)，文档已经初始化，请求的文档数据 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentData%2A> 不会导致不必要的初始化。 如果标志确实包括 [_VSRDTFLAGS4。RDT_PendingInitialization](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4.RDT_PendingInitialization>)，在初始化文档之前，扩展应避免请求文档数据。 可以在事件处理程序中检测到此初始化 `OnAfterAttributeChange(Ex)` 。

## <a name="test-extensions-to-see-if-they-force-initialization"></a>测试扩展以确定它们是否强制初始化

没有可见的提示来指示文档是否已初始化，因此，如果扩展正在强制初始化，则很难发现。 你可以设置一个使验证更简单的注册表项，因为这会导致未完全初始化的每个文档的标题在标题中具有文本 *[存根]* 。

在 **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\14.0\BackgroundSolutionLoad** 中，将 **StubTabTitleFormatString** 设置为 *{0} [存根]*。
