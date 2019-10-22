---
title: 工作流设计器 Shell 功能 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- WFDShellFeatures.UI
ms.assetid: 14bfe312-9592-408e-92ce-e98585ad16e7
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2c59dc8232713d4126b2c37693a1e241735eb163
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72606602"
---
# <a name="workflow-designer-shell-features"></a>工作流设计器 Shell 功能
[!INCLUDE[wfd1](../includes/wfd1-md.md)] 由三个主要的 UI 区域组成：设计器图面、设计器图面上面的痕迹栏和下面的 shell。 痕迹栏位于屏幕的顶部，用于显示当前根活动的祖先列表。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][如何：使用痕迹导航](../workflow-designer/how-to-use-breadcrumb-navigation.md)。 设计器图面位于屏幕的中央，用于撰写工作流。 Shell 位于屏幕的底部，包含用于管理当前视图的若干按钮。

## <a name="shell-features"></a>Shell 功能
 Shell 栏的右侧有几个按钮，可用于缩放工作流，使工作流的内容适合屏幕的大小，还可以显示或隐藏摘要图。 使用键盘快捷键 Ctrl++ 和 Ctrl+- 也可以放大和缩小工作流。

## <a name="overview-map"></a>摘要图
 摘要图显示当前痕迹根处的整个活动的缩小版本，包括该根的所有子级和这些子级的所有已展开子级。 视区（即带有橙色边框的矩形）中突出显示编辑器内当前显示的活动部分。 在摘要图中四处拖动该矩形将会滚动工作流设计器并更改编辑器的视图。

> [!NOTE]
> [!INCLUDE[wfd2](../includes/wfd2-md.md)] 用户界面是虚拟化的。 只在需要时才呈现活动设计器。 如果从未将工作流的某一部分拖到设计器图面，该部分在摘要图上将显示为空白。 在摘要图中四处滚动将绘制出完整的工作流。

## <a name="copying-or-saving-workflows-as-images"></a>将工作流复制或另存为图像
 可以用位图格式复制工作流，或者用位图或向量格式保存工作流。 复制或保存图像提供了一种将当前痕迹根处的整个活动的视图（包括该根的所有子级和这些子级的所有已展开子级）导出到其他程序的方法。

 若要复制为图像，请在设计器中右键单击任意位置，然后选择 "**复制为图像**"。 若要另存为图像，请在设计器中右键单击任意位置，然后选择 "**另存为图像**"。 可以采用 JPG、PNG、GIF 或 XPS 格式保存工作流。 该格式在窗口底部的 "**另存为类型：** " 下拉列表框中的 "**另存为**" 对话框中选择。

## <a name="fonts-and-colors"></a>字体和颜色
 在 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 内的 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 中使用的字体由环境字体控制。 如果您使用的是高对比度的操作系统主题配色方案，[!INCLUDE[wfd2](../includes/wfd2-md.md)] 中显示的颜色将发生更改。 在对字体或颜色设置进行更改后，必须重新启动 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 才能使更改在 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 中生效。