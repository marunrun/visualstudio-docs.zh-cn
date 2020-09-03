---
title: IntelliSense 宿主 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - IntelliSense hosting
ms.assetid: 20c61f8a-d32d-47e2-9c67-bf721e2cbead
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a5c378aec6822a436de0d8fc2656fcac7be4149f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203898"
---
# <a name="intellisense-hosting"></a>IntelliSense 托管
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 启用 IntelliSense 宿主。 通过 IntellSense 宿主，你可以为不是由 Visual Studio 文本编辑器承载的代码提供 IntelliSense。  
  
## <a name="intellisense-hosting-usage"></a>IntelliSense 托管使用情况  
 在 Visual Studio 中，有权访问完成集和文本缓冲区的任何代码都可以从用户界面中的任何位置)  (UI 获取智能感知窗口。 在 " **监视** " 窗口或 "断点属性" 窗口的 "条件" 字段中完成此任务的一些示例方案。  
  
### <a name="implementation-interfaces"></a>实现接口  
  
#### <a name="ivsintellisensehost"></a>IVsIntellisenseHost  
 承载 IntelliSense 弹出窗口的任何 UI 组件都必须支持 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost> 接口。 默认的核心编辑器文本视图包含 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost> 用于保留当前 IntelliSense 功能的常用接口实现。 大多数情况下，接口的方法表示在 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost> 接口上实现的部分的子集 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 。 子集包括 IntelliSense UI 处理、插入符号和选择操作以及简单的文本替换功能。 此外，接口还 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost> 启用了单独的 IntelliSense "subject" 和 "context"，以便为不会直接存在于上下文中的文本缓冲区中的主题提供 intellisense。  
  
#### <a name="ivsintellisensehostgethostflags"></a>IVsIntellisenseHost.GetHostFlags  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost>接口提供程序必须实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetHostFlags%2A> 方法，使客户端能够确定宿主支持的 IntelliSense 功能类型。  
  
 下面汇总了 [IntelliSenseHostFlags](../extensibility/intellisensehostflags.md)中定义的主机标志。  
  
|IntelliSense 主机标志|说明|  
|----------------------------|-----------------|  
|IHF_READONLYCONTEXT|如果设置此标志，则意味着上下文缓冲区是只读的，并且只在主题文本中进行编辑。|  
|IHF_NOSEPERATESUBJECT|如果设置此标志，则意味着没有单独的 IntelliSense 主题。 主题存在于上下文缓冲区中，如传统 IntelliSense 系统中的 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 。|  
|IHF_SINGLELINESUBJECT|如果设置此标志，则意味着使用者不支持多行功能，如 " **监视** " 窗口中的单个行编辑。|  
|IHF_FORCECOMMITTOCONTEXT|如果设置了此标志并且必须更新上下文缓冲区，则宿主允许忽略上下文缓冲区的只读标志，并继续编辑。|  
|IHF_OVERTYPE|在主题或上下文) 中编辑 (应在改写模式下完成。|  
  
#### <a name="ivsintellisensehostbeforecompletorcommit-and-ivsintellisensehostaftercompletorcommit"></a>IVsIntellisenseHost. BeforeCompletorCommit 和 IVsIntellisenseHost AfterCompletorCommit  
 这些回调方法由完成窗口在提交文本之前和之后调用，以启用预处理和后期处理。  
  
#### <a name="ivsintellisensecompletor"></a>IVsIntellisenseCompletor  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseCompletor>接口是标准完成窗口的共同创建版本，由集成开发环境 (IDE) 使用。 任何 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost> 接口都可以使用此 completor 接口快速实现 IntelliSense。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.TextManager.Interop>
