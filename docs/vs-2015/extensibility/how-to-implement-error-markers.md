---
title: 如何：实现错误标记 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - error markers
ms.assetid: e8e78514-5720-4fc2-aa43-00b6af482e38
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2af9e0765fb5bc73a35bebfc2f50f5d2a41122d3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840515"
---
# <a name="how-to-implement-error-markers"></a>如何：实现错误标记
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

错误标记 (或红色波浪下划线) 是最难以实现的文本编辑器自定义项。 不过，他们为你的 VSPackage 用户提供的好处远远超过提供这些用户的成本。 错误标记的细微标记文本，语言分析器使用波浪线或红色波浪线认为不正确。 此指标通过直观显示错误代码来帮助编程人员。  
  
 使用文本标记实现红色的波浪形下划线。 作为一种规则，语言服务在空闲时或后台线程中，将红色的波浪形下划线添加到文本缓冲区。  
  
### <a name="to-implement-the-red-wavy-underline-feature"></a>实现红色波浪下划线功能  
  
1. 选择要在其下放置红色波浪下划线的文本。  
  
2. 创建类型的标记 `MARKER_CODESENSE_ERROR` 。 有关详细信息，请参阅 [如何：添加标准文本标记](../extensibility/how-to-add-standard-text-markers.md)。  
  
3. 之后，传递 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> 接口指针。  
  
   此过程还允许您在给定的标记上创建提示文本或特殊的上下文菜单。 有关详细信息，请参阅 [如何：添加标准文本标记](../extensibility/how-to-add-standard-text-markers.md)。  
  
   需要以下对象，才能显示错误标记。  
  
- 分析器。  
  
- 任务提供程序 (即，用于 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskProvider2> 维护行信息更改记录的) 的实现，以便确定要重新分析的行。  
  
- 使用) 方法从视图中捕获插入符号更改事件的文本视图筛选器 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEvents.OnChangeCaretLine%2A> 。  
  
  分析器、任务提供程序和筛选器提供必要的基础结构来使错误标记成为可能。 以下步骤提供了显示错误标记的过程。  
  
1. 在正在筛选的视图中，筛选器将获取指向与视图的数据关联的任务提供程序的指针。  
  
    > [!NOTE]
    > 您可以对方法提示、语句完成、错误标记等使用相同的命令筛选器。  
  
2. 当筛选器收到指示您已移到另一行的事件时，将创建一个任务来检查是否有错误。  
  
3. 任务处理程序检查行是否已更新。 如果是，它将分析行中是否有错误。  
  
4. 如果发现错误，任务提供程序会创建任务项实例。 此实例创建环境用作文本视图中的错误标记的文本标记。  
  
## <a name="see-also"></a>另请参阅  
 [将文本标记与旧版 API 一起使用](../extensibility/using-text-markers-with-the-legacy-api.md)   
 [如何：添加标准文本标记](../extensibility/how-to-add-standard-text-markers.md)   
 [如何：创建自定义文本标记](../extensibility/how-to-create-custom-text-markers.md)   
 [如何：使用文本标记](../extensibility/how-to-use-text-markers.md)
