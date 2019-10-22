---
title: Blend 中的“笔”工具修改键 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: c3ab14c6-a320-46db-a6b3-7fd1ca261587
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5f69969ac60e7476e2d9430266acca41c0745f3a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72664181"
---
# <a name="pen-tool-modifier-keys-in-blend"></a>Blend 中的“笔”工具修改键
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

下表列出了在使用 "**笔**" 工具![](../designers/media/d514358f-185a-412f-a55d-36633b25dc8a.png "d514358f-185a-412f-a55d-36633b25dc8a")创建路径时可用于修改路径的快捷方式。 “笔”工具还可用于在现有路径上添加或删除点，或联接两个现有路径。

|任务|请执行此操作|指针|
|-----------------------|-------------|-------------|
|创建一个点来开始绘制直线线段|单击以创建新点|![](../designers/media/0bfb1b71-80ac-4ad4-aed8-40e09f8b7ab8.png "0bfb1b71-80ac-4ad4-aed8-40e09f8b7ab8")<br /><br /> “钢笔”指针|
|创建一个点来开始绘制曲线线段|单击以创建新点，然后在松开鼠标按钮前拖动以调整切线图柄|![](../designers/media/0bfb1b71-80ac-4ad4-aed8-40e09f8b7ab8.png "0bfb1b71-80ac-4ad4-aed8-40e09f8b7ab8")<br /><br /> “钢笔”指针|
|在没有平滑限制的情况下调整最后的切线，使您生成尖锐的角|单击以创建新点，然后在松开鼠标按钮前按 Alt 键|![](../designers/media/317e5475-b70c-489f-9477-110a98639ade.png "317e5475-b70c-489f-9477-110a98639ade")<br /><br /> “钢笔”调整指针|
|拆分最后一个切线，以便切线终结点独立操作，使您生成尖锐的角|单击以创建新点，然后在松开鼠标按钮前按住 Alt 键并拖动|![](../designers/media/317e5475-b70c-489f-9477-110a98639ade.png "317e5475-b70c-489f-9477-110a98639ade")<br /><br /> “钢笔”调整指针|
|以 15 度的增量将切线终结点绕新点移动|单击以创建新点，然后在松开鼠标按钮前按住 Shift+Alt 并拖动|![](../designers/media/317e5475-b70c-489f-9477-110a98639ade.png "317e5475-b70c-489f-9477-110a98639ade")<br /><br /> “钢笔”调整指针|
|将一个终结点处的切线减小为零长度|单击该终结点|![](../designers/media/317e5475-b70c-489f-9477-110a98639ade.png "317e5475-b70c-489f-9477-110a98639ade")<br /><br /> “钢笔”调整指针|
|向现有路径添加新点|单击您需要新点的位置处的路径|![](../designers/media/b004ad5a-33a4-46ae-81c0-20be0d819332.png "b004ad5a-33a4-46ae-81c0-20be0d819332")<br /><br /> “钢笔”插入指针|
|从路径删除一个点|悬浮在现有点上并单击|![](../designers/media/08a64b78-f3df-4730-8169-c56b5631b071.png "08a64b78-f3df-4730-8169-c56b5631b071")<br /><br /> “钢笔”删除指针|
|结束具有尖锐角的路径|单击起始点|![](../designers/media/a12fd3b4-a553-4762-b01c-c35efa594362.png "a12fd3b4-a553-4762-b01c-c35efa594362")<br /><br /> “钢笔”结束指针|
|结束边角处具有平滑曲线的路径|单击起始点并在松开鼠标按钮前拖动以修改切线图柄|![](../designers/media/a12fd3b4-a553-4762-b01c-c35efa594362.png "a12fd3b4-a553-4762-b01c-c35efa594362")<br /><br /> “钢笔”结束指针|
|在联接两个路径时创建尖锐的角|选择两个路径，单击“笔”工具，并单击其中一个路径的终结点，然后单击另一路径的终结点|![](../designers/media/bd12dfa4-112e-4f37-9765-3479e6b69894.png "bd12dfa4-112e-4f37-9765-3479e6b69894")<br /><br /> “钢笔”联接指针|
|在联接两个路径时创建平滑的角|选择两个路径，单击“笔”工具，并单击其中一个路径的终结点，然后拖动另一路径的终结点|![](../designers/media/bd12dfa4-112e-4f37-9765-3479e6b69894.png "bd12dfa4-112e-4f37-9765-3479e6b69894")<br /><br /> “钢笔”联接指针|
|创建一个新路径|按住 Ctrl 键并在前一路径外单击以停止向前一路径添加点，然后单击或拖动新路径开始的位置|![](../designers/media/69758176-5f53-465b-808c-f13fd1a0b3f2.png "69758176-5f53-465b-808c-f13fd1a0b3f2")<br /><br /> “钢笔”开始指针|

## <a name="see-also"></a>请参阅
 [键盘快捷方式和修改键](../designers/keyboard-shortcuts-and-modifier-keys-in-blend.md)[美工板修改键](../designers/artboard-modifier-keys-in-blend.md)[路径选择工具修改键](../designers/direct-selection-tool-modifier-keys-in-blend.md)[绘制形状和路径](../designers/draw-shapes-and-paths.md)
