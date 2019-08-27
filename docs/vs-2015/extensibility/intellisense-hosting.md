---
title: IntelliSense 承载 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203898"
---
# <a name="intellisense-hosting"></a>IntelliSense 托管
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 使 IntelliSense 托管。 IntellSense 承载可让你提供不 Visual Studio 文本编辑器由托管代码的 IntelliSense。  
  
## <a name="intellisense-hosting-usage"></a>IntelliSense 承载使用情况  
 在 Visual Studio 中，有权访问一完成，以及文本缓冲区的所有代码可以都获取 IntelliSense windows 从任何位置中的用户界面 (UI)。 此的一些示例方案是中的自动补全**监视**窗口或断点属性窗口的条件字段中。  
  
### <a name="implementation-interfaces"></a>实现接口  
  
#### <a name="ivsintellisensehost"></a>IVsIntellisenseHost  
 承载 IntelliSense 弹出窗口的任何 UI 组件必须支持<xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost>接口。 默认核心编辑器文本视图包括股票<xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost>接口实现以保留当前的 IntelliSense 功能。 大多数情况下的方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost>接口实现的功能子集的表示<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>接口。 该子集包括 IntelliSense UI 处理、 插入符号和选择操作和简单的文本的替代功能。 此外，<xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost>接口使单独智能感知"subject"和"上下文"，以便可以为不直接存在于正在使用的上下文的文本缓冲区的使用者提供 IntelliSense。  
  
#### <a name="ivsintellisensehostgethostflags"></a>IVsIntellisenseHost.GetHostFlags  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost>接口提供程序必须实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetHostFlags%2A>方法，以使客户端以确定哪种类型的 IntelliSense 功能在主机支持。  
  
 中定义的主机标志[IntelliSenseHostFlags](../extensibility/intellisensehostflags.md)，总结如下。  
  
|IntelliSense 主机标志|描述|  
|----------------------------|-----------------|  
|IHF_READONLYCONTEXT|设置此标志表示，上下文缓冲区是只读的文件和编辑仅发生在主题文本。|  
|IHF_NOSEPERATESUBJECT|设置此标志表示的存在是没有单独的 IntelliSense 使用者。 主题中的上下文缓冲区，例如中存在的传统<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>智能感知系统。|  
|IHF_SINGLELINESUBJECT|设置此标志表示，将使用者不是多行支持，如单个行中编辑**监视**窗口。|  
|IHF_FORCECOMMITTOCONTEXT|如果设置此标志，必须更新上下文缓冲区，主机将启用要忽略的上下文缓冲区上的只读标志和编辑以继续。|  
|IHF_OVERTYPE|应在改写模式下编辑 （在使用者或上下文）。|  
  
#### <a name="ivsintellisensehostbeforecompletorcommit-and-ivsintellisensehostaftercompletorcommit"></a>IVsIntellisenseHost.BeforeCompletorCommit 和 IVsIntellisenseHost.AfterCompletorCommit  
 之前和之后的文本是已提交，以便预处理和后处理完成窗口通过调用这些回调方法。  
  
#### <a name="ivsintellisensecompletor"></a>IVsIntellisenseCompletor  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseCompletor>接口是在集成的开发环境 (IDE) 使用标准完成窗口的共同创建版本。 任何<xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost>接口快速可以通过使用此 completor 接口来实现智能感知。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.TextManager.Interop>
