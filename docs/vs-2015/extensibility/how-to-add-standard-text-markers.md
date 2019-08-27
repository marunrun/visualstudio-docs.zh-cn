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
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63436022"
---
# <a name="how-to-add-standard-text-markers"></a>如何：添加标准文本标记
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用以下过程来创建一个与提供的默认文本标记类型[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]核心编辑器。  
  
### <a name="to-create-a-text-marker"></a>若要创建文本标记  
  
1. 根据您使用的一个或两个-维坐标系，请调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.CreateLineMarker%2A>方法或<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream.CreateStreamMarker%2A>方法来创建新的文本标记。  
  
     在此方法调用中，指定标记类型，范围内的文本，通过创建标记和<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>接口。 然后将此方法返回指向到新创建的文本标记。 标记类型取自<xref:Microsoft.VisualStudio.TextManager.Interop.MARKERTYPE>枚举。 指定<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>接口如果你想要通知的标记事件。  
  
    > [!NOTE]
    > 在主 UI 线程上创建文本标记。 核心编辑器依赖于要创建文本标记的文本缓冲区的内容，而文本缓冲区不是线程安全。  
  
## <a name="adding-a-custom-command"></a>添加自定义命令  
 实现`IVsTextMarkerClient`接口并向其提供一个指针，从标记增强了几种方式标记行为。 首先，这允许您在标记为提供提示，并执行命令。 这还允许您以接收各个标记的事件通知，并通过标记创建自定义上下文菜单。 使用以下过程将自定义命令添加到标记上下文菜单。  
  
#### <a name="to-add-a-custom-command-to-the-context-menu"></a>若要将自定义命令添加到上下文菜单  
  
1. 上下文菜单显示之前，环境在调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient.GetMarkerCommandInfo%2A>方法和通过您到文本标记的指针的影响和上下文菜单中的命令项的数目。  
  
     例如，上下文菜单上的特定于断点的命令包括**删除断点**通过**新断点**，如以下屏幕截图中显示。  
  
     ![标记上下文菜单](../extensibility/media/vsmarkercontextmenu.gif "vsMarkercontextmenu")  
  
2. 传递回标识的自定义命令名称的一些文本。 例如，**删除断点**如果环境未已提供它可能是自定义命令。 你还将传递回该命令是否受支持、 可用且已启用，和/或开启 / 关闭切换。 环境使用此信息来正确的方式的上下文菜单中显示自定义命令。  
  
3. 若要执行该命令，环境调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient.ExecMarkerCommand%2A>方法，您将指针传递到文本标记并从上下文菜单中选择的命令数。  
  
     使用来自此调用的此信息来执行任何操作的文本标记的自定义命令指示。  
  
## <a name="see-also"></a>请参阅  
 [旧版 API 中使用文本标记](../extensibility/using-text-markers-with-the-legacy-api.md)   
 [如何：实现错误标记](../extensibility/how-to-implement-error-markers.md)   
 [如何：创建自定义文本标记](../extensibility/how-to-create-custom-text-markers.md)   
 [如何：使用文本标记](../extensibility/how-to-use-text-markers.md)
