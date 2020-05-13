---
title: 延迟文档加载 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: fb07b8e2-a4e3-4cb0-b04f-8eb11c491f35
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2f78d49013c1f0bd359d4439b73620a159a9ccc0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708816"
---
# <a name="delayed-document-loading"></a>延迟的文档加载

当用户重新打开 Visual Studio 解决方案时，大多数关联的文档不会立即加载。 文档窗口框架以挂起初始化状态创建，占位符文档（称为存根框架）放置在正在运行的文档表 （RDT） 中。

通过加载文档中的元素，扩展可能会导致项目文档不必要地加载，这会增加 Visual Studio 的总体内存占用空间。

## <a name="document-loading"></a>文档加载

当用户访问文档时，通过选择窗口框架的选项卡，将完全初始化存根框架和文档。 文档还可以通过请求文档数据的扩展进行初始化，该扩展通过直接访问 RDT 获取文档数据，或者通过进行以下调用之一间接访问 RDT：

- 窗口框架<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A>方法。

- 以下任一<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>属性上的窗口框架方法：

  - [__VSFPROPIDVSFPROPID_DocView](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_DocView>)

  - [__VSFPROPIDVSFPROPID_ViewHelper](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_ViewHelper>)

  - [__VSFPROPIDVSFPROPID_DocData](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_DocData>)

  - [__VSFPROPIDVSFPROPID_AltDocData](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_AltDocData>)

  - [__VSFPROPIDVSFPROPID_RDTDocData](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_RDTDocData>)

  - [__VSFPROPIDVSFPROPID_SPProjContext](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_SPProjContext>)

- 如果扩展使用托管代码，则不应调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.GetDocumentInfo%2A>，除非您确定文档未处于挂起初始化状态，或者您希望文档完全初始化。 原因是该方法始终返回 doc 数据对象，并在必要时创建它。 相反，您应该调用`IVsRunningDocumentTable4`接口上的一种方法。

- 如果扩展使用C++，则可以传递`null`不需要的参数。

- 在请求其他属性之前，可以通过调用以下方法之一来避免不必要的文档加载：

  - <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>使用[__VSFPROPID6。VSFPROPID_PendingInitialization](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID6.VSFPROPID_PendingInitialization>). .

  - <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentFlags%2A>. 此方法返回包含<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4>_VSRDTFLAGS4值的对象[。如果](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4.RDT_PendingInitialization>)文档尚未初始化，RDT_PendingInitialization。

通过订阅文档完全初始化时引发的 RDT 事件，可以找出文档加载时间。 有两种可能性：

- 如果事件接收器实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents2>，则可以订阅<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents2.OnAfterAttributeChangeEx%2A>。

- 否则，您可以订阅<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnAfterAttributeChange%2A>。

下面的示例是假设的文档访问方案：Visual Studio 扩展希望显示有关打开文档的一些信息，例如编辑锁计数和文档数据。 它使用<xref:Microsoft.VisualStudio.Shell.Interop.IEnumRunningDocuments>枚举 RDT 中的文档，然后<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.GetDocumentInfo%2A>调用每个文档以检索编辑锁计数和文档数据。 如果文档处于挂起的初始化状态，则请求文档数据会导致它不必要地初始化。

访问文档的更有效方法是使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentEditLockCount%2A>来获取编辑锁计数，然后用于<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentFlags%2A>确定文档是否已初始化。 如果标志不包含[_VSRDTFLAGS4。RDT_PendingInitialization](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4.RDT_PendingInitialization>)，文档已初始化，请求文档<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentData%2A>数据不会导致任何不必要的初始化。 如果标志包含[_VSRDTFLAGS4。RDT_PendingInitialization](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4.RDT_PendingInitialization>)，扩展应避免请求文档数据，直到文档初始化。 可以在事件处理程序中`OnAfterAttributeChange(Ex)`检测到此初始化。

## <a name="test-extensions-to-see-if-they-force-initialization"></a>测试扩展以查看它们是否强制初始化

没有指示文档是否已初始化的可见提示，因此很难确定扩展是否强制初始化。 您可以设置一个注册表项，使验证更容易，因为它会导致未完全初始化的每个文档的标题在标题中包含文本 *[Stub]。*

在**HKEY_CURRENT_USER_软件\微软_VisualStudio_14.0\背景解决方案加载中**，将**StubTabTitle格式字符串**设置为*{0}[Stub]。*
