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
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63435971"
---
# <a name="how-to-implement-error-markers"></a>如何：实现错误标记
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

错误标记 （或红色的波浪形下划线） 是最困难的文本编辑器自定义实现。 但是，它们提供给你的 VSPackage 的用户的好处可以远远超过，让他们的成本。 错误标记略有标记语言分析器认为不正确并波浪或波浪红线的文本。 此指标帮助程序员通过直观地显示不正确的代码。  
  
 使用文本标记来实现红色的波浪形下划线。 一般来说，语言服务红色的波浪形下划线的文本缓冲区将作为添加到背景通过在空闲时或在后台线程中。  
  
### <a name="to-implement-the-red-wavy-underline-feature"></a>若要实现红色波浪下划线功能  
  
1. 选择要在其下放置的红色的波浪下划线的文本。  
  
2. 创建类型的标记`MARKER_CODESENSE_ERROR`。 有关详细信息，请参阅[如何：添加标准文本标记](../extensibility/how-to-add-standard-text-markers.md)。  
  
3. 此后，传入<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>接口指针。  
  
   此过程还允许您通过给定标记创建的提示文本或特殊的上下文菜单。 有关详细信息，请参阅[如何：添加标准文本标记](../extensibility/how-to-add-standard-text-markers.md)。  
  
   错误标记才能显示以下对象是必需的。  
  
- 分析器。  
  
- 任务提供程序 (即，实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskProvider2>)，以便确定要重新分析中的行保留行信息中的更改的记录。  
  
- 捕获插入符号的文本视图筛选器从视图中使用的更改事件<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEvents.OnChangeCaretLine%2A>) 方法。  
  
  分析器、 任务提供程序和筛选器提供必要尽量将错误标记的基础结构。 以下步骤提供进程显示错误标记。  
  
1. 正在筛选的视图，在筛选器获取指向与该视图的数据关联的任务提供程序的指针。  
  
    > [!NOTE]
    > 有关方法的提示、 语句完成、 错误标记等，可以使用的相同命令筛选器。  
  
2. 当筛选器收到一个事件，指示已移动到另一个行时，创建任务，检查有错误。  
  
3. 任务处理程序会检查是否已更新行。 如果是这样，它将解析错误的行。  
  
4. 如果发现错误，任务提供程序创建的任务项实例。 此实例创建文本视图中将错误标记为在环境中使用的文本标记。  
  
## <a name="see-also"></a>请参阅  
 [旧版 API 中使用文本标记](../extensibility/using-text-markers-with-the-legacy-api.md)   
 [如何：添加标准文本标记](../extensibility/how-to-add-standard-text-markers.md)   
 [如何：创建自定义文本标记](../extensibility/how-to-create-custom-text-markers.md)   
 [如何：使用文本标记](../extensibility/how-to-use-text-markers.md)
