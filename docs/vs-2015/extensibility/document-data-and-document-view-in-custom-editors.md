---
title: 文档数据和文档视图中自定义编辑器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - document data and document view
ms.assetid: 71eea623-f566-4feb-84cd-ca1ba71bc493
caps.latest.revision: 24
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2f73ffde43f2ef3608ae492a9643f7920243d818
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68204680"
---
# <a name="document-data-and-document-view-in-custom-editors"></a>自定义编辑器中的文档数据和文档视图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

自定义编辑器由两部分组成： 文档数据对象和文档视图对象。 顾名思义，文档数据对象表示要显示的文本数据和文档视图对象 （或"视图"） 表示要在其中显示文档数据对象的一个或多个窗口。  
  
## <a name="document-data-object"></a>文档数据对象  
 文档数据对象是文本的表示形式中的文本缓冲区的数据。 它是存储文档文本和其他信息、 处理文档的持久性，并使其数据的多个视图的 COM 对象。 有关详细信息，请参见  
  
 <xref:EnvDTE80.Window2.DocumentData%2A> 并[记录 Windows](../extensibility/internals/document-windows.md)。  
  
 自定义编辑器和设计器可以选择使用<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>对象或其自己的自定义缓冲区。 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> 对标准编辑器采用简化的嵌入模型，支持多个视图，并提供用于管理多个视图的事件接口。  
  
## <a name="document-view-object"></a>文档视图对象  
 一个窗口，显示代码和其他文本被称为文档视图。 当您创建一个编辑器时，可以选择单个视图中，单个窗口中显示文本或多个视图中，多个窗口中显示文本。 选择取决于你的应用程序。 例如，如果您需要编辑的同时，可以选择多个视图。 每个视图都在集成的开发环境中的 (IDE) 运行文档表 (RDT) 的条目相关联。 查看 windows 属于项目或<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>对象。  
  
 如果编辑器支持文档数据对象的多个视图，你的文档数据和文档视图对象必须单独。 否则，可以将它们分组在一起。 有关详细信息，请参阅[Supporting Multiple Document Views](../extensibility/supporting-multiple-document-views.md)。  
  
 IDE 会通过运行文档表中每个条目匹配的项标识符 (ItemID) 通知视图获取有关事件 （例如，关闭一个包含文档的解决方案时）。 有关这方面的详细信息，请参阅[运行文档表](../extensibility/internals/running-document-table.md)。  
  
 有两个选项用于自定义编辑器创建视图。 一个是就地激活模型，该视图托管在窗口中使用的 ActiveX 控件或文档数据对象。 第二个是简化的嵌入模型，通过托管视图的位置[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]和<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>实现以处理窗口命令。 有关就地激活模型的信息，请参阅[就地激活](../misc/in-place-activation.md)。 简化的嵌入模型有关的信息，请参阅[简化嵌入](../extensibility/simplified-embedding.md)。  
  
## <a name="see-also"></a>请参阅  
 [支持多个文档视图](../extensibility/supporting-multiple-document-views.md)   
 [简化的嵌入](../extensibility/simplified-embedding.md)   
 [如何：附加文档数据的视图](../extensibility/how-to-attach-views-to-document-data.md)   
 [文档锁持有者管理](../extensibility/document-lock-holder-management.md)   
 [单个和多选项卡视图](../extensibility/single-and-multi-tab-views.md)   
 [正在保存标准文档](../extensibility/internals/saving-a-standard-document.md)   
 [持久性和正在运行文档表](../extensibility/internals/persistence-and-the-running-document-table.md)   
 [确定哪个编辑器打开一个项目中的文件](../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)   
 [编辑器工厂](../extensibility/editor-factories.md)
