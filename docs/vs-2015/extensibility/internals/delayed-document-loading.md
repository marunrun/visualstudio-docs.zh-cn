---
title: 延迟的文档加载 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: fb07b8e2-a4e3-4cb0-b04f-8eb11c491f35
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5565749a21614bb0b882beab8c83ed63bc839229
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196859"
---
# <a name="delayed-document-loading"></a>文档加载延迟
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

当用户重新打开 Visual Studio 解决方案时，大多数关联的文档将不会立即加载。 文档窗口框架是在 "挂起初始化" 状态下创建的，占位符文档 (称为存根帧) 放置在正在运行的文档表中 (RDT) 。  
  
 在加载文档之前，通过在文档中查询元素，你的扩展可能会导致不必要地加载项目文档。 这会增加 Visual Studio 的总体内存占用量。  
  
## <a name="document-loading"></a>文档加载  
 当用户访问文档时（例如，通过选择窗口框架的选项卡），将完全初始化存根（stub）框架和文档。 该文档还可以通过以下方式初始化：请求文档数据的扩展：通过直接访问 RDT 来获取文档数据，或通过进行以下调用之一间接访问 RDT：  
  
- 窗口框架显示方法： <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A> 。  
  
- 以下任何属性的窗口框架 GetProperty 方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> ：  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  如果您的扩展插件使用托管代码，则不应调用， <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.GetDocumentInfo%2A> 除非您确定该文档未处于挂起初始化状态，或者您希望文档完全初始化。 这是因为，此方法始终返回 doc 数据对象（如有必要）。 应改为调用 IVsRunningDocumentTable4 接口上的方法之一。  
  
  如果扩展使用 c + +，则可以传递 `null` 不需要的参数。  
  
  在请求相关属性之前，可以通过调用以下方法之一来避免不必要的文档加载：在请求其他属性之前。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> 使用 <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID6> 。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentFlags%2A>. 如果文档尚未初始化，则此方法将返回一个 <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4> 对象，该对象包含的值 <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4> 。  
  
  您可以通过订阅 RDT 事件（在文档完全初始化时引发）来查看文档的加载时间。 有两种可能的原因：  
  
- 如果事件接收器实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents2> ，则可以订阅 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents2.OnAfterAttributeChangeEx%2A> 、  
  
- 否则，你可以订阅 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnAfterAttributeChange%2A> 。  
  
  下面是一个假设的文档访问方案。 Visual Studio 扩展希望显示有关打开的文档的一些信息，例如，编辑锁定计数和文档数据。 它使用枚举 RDT 中的文档 <xref:Microsoft.VisualStudio.Shell.Interop.IEnumRunningDocuments> ，然后对每个文档进行调用，以便 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.GetDocumentInfo%2A> 检索编辑锁定计数和文档数据。 如果文档处于挂起初始化状态，请求文档数据将导致其不必要地初始化。  
  
  执行此操作的一种更有效的方法是使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentEditLockCount%2A> 获取编辑锁计数，并使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentFlags%2A> 来确定文档是否已初始化。 如果标志不包括 <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4> ，则文档已初始化，请求的文档数据不 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentData%2A> 会导致不必要的初始化。 如果标志确实包括，则在 <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4> 初始化文档之前，扩展应避免请求文档数据。 这可以在 OnAfterAttributeChange (Ex) 事件处理程序中检测到。  
  
## <a name="testing-extensions-to-see-if-they-force-initialization"></a>测试扩展以了解它们是否强制初始化  
 没有可见的提示来指示文档是否已初始化，因此，如果扩展正在强制初始化，则很难发现。 你可以设置一个使验证更简单的注册表项，因为这会导致未完全初始化的每个文档的标题都包含 `[Stub]` 标题中的文本。  
  
 在**HKEY_CURRENT_USER \software\microsoft\visualstudio\14.0\backgroundsolutionload**"中，将**StubTabTitleFormatString**设置为** {0} [存根]**。
