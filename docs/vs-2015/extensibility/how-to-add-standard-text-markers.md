---
title: 如何：添加标准文本标记 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - standard text markers
ms.assetid: a39fca69-0014-474c-933f-51f0e9b9617e
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 912d5d7a225520fc825d832bf73f5cfc733a9486
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840345"
---
# <a name="how-to-add-standard-text-markers"></a>如何：添加标准文本标记
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用以下过程创建一个使用核心编辑器提供的默认文本标记类型 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。  
  
### <a name="to-create-a-text-marker"></a>创建文本标记  
  
1. 根据您使用的是一个还是二维坐标系统，请调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.CreateLineMarker%2A> 方法或 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream.CreateStreamMarker%2A> 方法来创建新的文本标记。  
  
     在此方法调用中，指定标记类型、用于创建标记的文本范围以及 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> 接口。 此方法随后返回指向新创建的文本标记的指针。 标记类型取自 <xref:Microsoft.VisualStudio.TextManager.Interop.MARKERTYPE> 枚举。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>如果希望收到标记事件的通知，请指定接口。  
  
    > [!NOTE]
    > 仅在主 UI 线程上创建文本标记。 核心编辑器依赖于文本缓冲区的内容来创建文本标记，文本缓冲区不是线程安全的。  
  
## <a name="adding-a-custom-command"></a>添加自定义命令  
 实现 `IVsTextMarkerClient` 接口并提供从标记指向它的指针可通过多种方式增强标记行为。 首先，你可以为标记提供提示并执行命令。 这还允许您接收各个标记的事件通知，并在标记上创建自定义上下文菜单。 使用以下过程将自定义命令添加到标记上下文菜单。  
  
#### <a name="to-add-a-custom-command-to-the-context-menu"></a>向上下文菜单添加自定义命令  
  
1. 在显示上下文菜单之前，环境将调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient.GetMarkerCommandInfo%2A> 方法，并向您传递指向受影响的文本标记的指针以及上下文菜单中的命令项的数目。  
  
     例如，上下文菜单上的断点特定命令包括通过**新断点****删除断点**，如以下屏幕截图所示。  
  
     ![标记上下文菜单](../extensibility/media/vsmarkercontextmenu.gif "vsMarkercontextmenu")  
  
2. 向后传递一些标识自定义命令的名称的文本。 例如，如果环境尚未提供，则 **删除断点** 可能是自定义命令。 还将返回命令是否受支持、是否可用和启用，以及/或是否处于禁用状态。 环境使用此信息以正确的方式在上下文菜单中显示自定义命令。  
  
3. 若要执行该命令，环境将调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient.ExecMarkerCommand%2A> 方法，并向您传递一个指向文本标记的指针以及从上下文菜单中选择的命令的数目。  
  
     从此调用中使用此信息来执行自定义命令所指示的文本标记的任何操作。  
  
## <a name="see-also"></a>另请参阅  
 [将文本标记与旧版 API 一起使用](../extensibility/using-text-markers-with-the-legacy-api.md)   
 [如何：实现错误标记](../extensibility/how-to-implement-error-markers.md)   
 [如何：创建自定义文本标记](../extensibility/how-to-create-custom-text-markers.md)   
 [如何：使用文本标记](../extensibility/how-to-use-text-markers.md)
