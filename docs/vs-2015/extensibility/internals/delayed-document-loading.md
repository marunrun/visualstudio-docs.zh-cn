---
title: 文档加载延迟 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: fb07b8e2-a4e3-4cb0-b04f-8eb11c491f35
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5565749a21614bb0b882beab8c83ed63bc839229
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196859"
---
# <a name="delayed-document-loading"></a>文档加载延迟
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

当用户重新打开 Visual Studio 解决方案时，不会立即加载的大多数相关联的文档。 在挂起的初始化状态下，创建文档窗口框架和占位符文档 （称为存根 （stub） 帧） 被放在正在运行文档表 (RDT)。  
  
 您的扩展插件可能会导致通过查询的文档中的元素，在加载前不必要地加载项目文档。 用于 Visual Studio，这可以增加总体内存占用量。  
  
## <a name="document-loading"></a>文档加载  
 在用户访问该文档，例如通过选择窗口框架的选项卡时，完全初始化的存根 （stub） 框架和文档。 也可通过请求该文档的数据时，通过访问 RDT 直接以获取文档数据，或通过进行以下调用之一间接访问 RDT 扩展初始化文档：  
  
- 窗口框架显示方法： <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A>。  
  
- 窗口框架的 GetProperty 方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>上的任何以下属性：  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  如果您的扩展插件使用托管的代码，不应调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.GetDocumentInfo%2A>除非确定文档未处于挂起的初始化状态，或者想要完全初始化后的文档... 这是因为此方法始终返回文档数据对象，如有必要创建它。 相反，应调用的方法之一 IVsRunningDocumentTable4 接口上。  
  
  如果您的扩展插件使用C++，可以将传递`null`不希望的参数。  
  
  可以通过要求提供相关的属性之前调用以下方法之一来避免不必要的文档加载： 寻求其他属性之前。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> 使用<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID6>。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentFlags%2A>。 此方法返回<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4>包括的值的对象<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4>如果文档尚未初始化。  
  
  当文档已加载订阅时已完全初始化文档引发 RDT 事件时，可以找出。 有两种可能：  
  
- 如果事件接收器会实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents2>，您可以订阅<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents2.OnAfterAttributeChangeEx%2A>，  
  
- 否则，您可以订阅<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnAfterAttributeChange%2A>。  
  
  下面是假设文档访问方案。 Visual Studio 扩展想要显示有关打开的文档的某些信息，例如编辑锁定计数和文档数据有关的内容。 枚举中 RDT 使用文档<xref:Microsoft.VisualStudio.Shell.Interop.IEnumRunningDocuments>，然后调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.GetDocumentInfo%2A>以便检索编辑锁计数和文档数据的每个文档。 如果文档处于挂起的初始化状态，则请求文档数据将会导致它不必要地初始化。  
  
  这是为了使用这样做的更有效地<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentEditLockCount%2A>可获取编辑锁计数，然后使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentFlags%2A>来确定文档是否已初始化。 如果不包括标志<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4>，该文档已初始化，并请求使用的文档数据<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentData%2A>不会导致任何不必要的初始化。 如果包括标志<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4>，该扩展应避免初始化文档后，才请求文档数据。 这可以 OnAfterAttributeChange(Ex) 事件处理程序中检测到。  
  
## <a name="testing-extensions-to-see-if-they-force-initialization"></a>测试以查看是否它们强制进行初始化的扩展  
 没有任何可见提示，以指示是否已初始化文档，因此它可能很难找到您的扩展插件强制初始化。 可以设置注册表项，简化验证，因为它会导致未完全初始化文本的每个文档的标题`[Stub]`标题中。  
  
 在中**HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\14.0\BackgroundSolutionLoad]** ，请设置**StubTabTitleFormatString**到 **{0} [存根]** 。
