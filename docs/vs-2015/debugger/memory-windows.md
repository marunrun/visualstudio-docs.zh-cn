---
title: 内存窗口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.memory
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- Memory window
- strings [Visual Studio], viewing
- debugger [Visual Studio], Memory window
- memory [Visual Studio], debugging
- debugging [Visual Studio], Memory window
- buffers, viewing
ms.assetid: 7f7a0439-10e4-4966-bb2d-51f04cda4fe2
caps.latest.revision: 37
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e60f9b3c9acf1377139fee27486bb10251d8804a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68158468"
---
# <a name="memory-windows"></a>“内存”窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

" **内存** " 窗口提供对应用程序使用的内存空间的查看。 " **监视** " 窗口、" **快速监视** " 对话框、"自动 **" 窗口和 "** **局部变量** " 窗口显示变量的内容，这些变量存储在内存中的特定位置。 但 " **内存** " 窗口显示大规模图片。 这对于检查大片的数据（如缓冲区和大的字符串）很方便，在其他窗口中显示就不太好。 但是，" **内存** " 窗口并不局限于显示数据。 该窗口可以显示内存空间中的任何内容，不论这些内容是数据、代码还是未分配内存中的无用随机位。  
  
 只有在 "**选项**" 对话框的 "**调试**" 节点中启用了地址级调试后，"**内存**" 窗口才可用。 " **内存** " 窗口不适用于脚本或 SQL，这是不能识别内存概念的语言。  
  
## <a name="opening-a-memory-window"></a>打开“内存”窗口  
  
#### <a name="to-open-a-memory-window"></a>打开“内存”窗口  
  
1. 如果尚未进入调试模式，请开始调试。  
  
2. 在 " **调试** " 菜单中，指向 " **窗口**"。 然后，指向 " **内存** "，然后单击 " **内存 1**"、" **内存 2**"、" **内存 3**" 或 " **内存 4**"。  (低级别版本只有一个 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] **内存** 窗口。 如果正在使用这些版本之一，只需单击 " **内存**"。 )   
  
## <a name="paging-in-the-memory-window"></a>在“内存”窗口中分页  
 " **内存** " 窗口具有以非标准方式操作的垂直滚动条。 如今的计算机地址空间非常大，抓取滚动条滚动块并将其移动到任意位置，就容易找不到地址。 为此，滚动块就像“装了弹簧”，总是保持在滚动条的中心。 在本机代码应用程序中，可以向上或向下翻页，但不能随便滚动。  
  
 较高的内存地址显示在窗口的底部。 若要查看较高的地址，请向下滚动而不是向上滚动。  
  
#### <a name="to-page-up-or-down-in-memory"></a>在内存中向上或向下翻页  
  
1. 若要向下翻页（移动到较高的内存地址），请在垂直滚动条中单击滚动块以下的位置。  
  
2. 若要向上翻页（移动到较低的内存地址），请在垂直滚动条中单击滚动块以上的位置。  
  
## <a name="selecting-a-memory-location"></a>选择内存位置  
 如果要立即移动到内存中的选定位置，可以通过使用拖放操作或在 " **地址** " 框中编辑值来执行此操作。 " **地址** " 框不仅接受数字值，还接受计算结果为地址的表达式。 默认情况下，" **内存** " 窗口将 **地址** 表达式视为实时表达式，这会在程序执行时进行重新计算。 活动表达式可有极大用处。 例如，可以使用它们查看指针所指向的内存。  
  
#### <a name="to-select-a-memory-location-by-dragging-and-dropping"></a>通过拖放操作选择内存位置  
  
1. 在任一窗口中选择内存地址或选择包含内存地址的指针变量。  
  
2. 将地址或指针拖到 " **内存** " 窗口。  
  
#### <a name="to-select-a-memory-location-by-editing"></a>通过编辑选择内存位置  
  
1. 在 " **内存** " 窗口中，选择 " **地址** " 框。  
  
2. 键入或粘贴要查看的地址，然后按 **enter**。  
  
## <a name="changing-the-way-the-memory-window-displays-information"></a>更改“内存”窗口显示信息的方式  
 可以自定义“内存”窗口显示内存内容的方式。 默认情况下，内存内容以十六进制格式显示为一个字节的整数，列数由当前的窗口宽度自动确定。  
  
#### <a name="to-change-the-format-of-the-memory-contents"></a>更改内存内容的格式  
  
1. 右键单击 " **内存** " 窗口。  
  
2. 选择所需的格式。  
  
#### <a name="to-change-the-number-of-columns-in-the-memory-window"></a>更改“内存”窗口中的列数  
  
1. 在 " **内存** " 窗口顶部的工具栏中，找到 " **列** " 列表。  
  
2. 在 " **列** " 列表中，选择要显示的列数，或选择 " **自动** " 以自动调整以适应窗口的宽度。  
  
   如果你不希望在程序执行时更改 " **内存** " 窗口的内容，则可以关闭 "实时表达式计算"。  
  
#### <a name="to-toggle-live-evaluation"></a>打开或关闭活动计算  
  
1. 右键单击 " **内存** " 窗口。  
  
2. 在快捷菜单上，单击 " **自动重新计算**"。  
  
    如果打开活动计算，则该选项处于选中状态，单击该选项将关闭活动计算。 如果关闭活动计算，则该选项未处于选中状态，单击该选项将打开活动计算。  
  
   可以隐藏或显示“内存”窗口顶部的工具栏。 当工具栏隐藏时，无法访问“地址”框或其他工具。  
  
#### <a name="to-toggle-the-toolbar"></a>切换工具栏  
  
1. 右键单击 " **内存** " 窗口。  
  
2. 在快捷菜单上，单击 " **显示工具栏**"。  
  
     工具栏将出现或不出现，具体取决于它先前的状态。  
  
## <a name="following-a-pointer-through-memory"></a>跟踪内存中的指针  
 在本机代码应用程序中，可以将寄存器名称用作活动表达式。 例如，可以使用堆栈指针跟踪堆栈。  
  
#### <a name="to-follow-a-pointer-through-memory"></a>跟踪内存中的指针  
  
1. 在 " **内存** 窗口 **地址** " 框中，键入一个指针表达式。 指针变量必须在当前范围内。 根据所使用的语言，可能必须取消引用指针。  
  
2. 按 **Enter**。  
  
     现在，当你使用如 **Step**这样的执行命令时，显示的内存地址将在指针改变时自动更改。  
  
## <a name="see-also"></a>另请参阅  
 [查看调试器中的数据](../debugger/viewing-data-in-the-debugger.md)
