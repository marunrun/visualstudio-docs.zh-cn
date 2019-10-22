---
title: 代码片段选择器 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vs.expansionpicker
helpviewer_keywords:
- Code Snippet Picker
- IntelliSense code snippets, Code Snippet Picker
- code snippets, Code Snippet Picker
ms.assetid: f0862d48-fbbc-4cfe-b228-24492d5c89c4
caps.latest.revision: 29
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2918826d6923efa3db42f4f572c416b9668513a9
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660890"
---
# <a name="code-snippet-picker"></a>代码段选择器
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 代码编辑器提供了“代码片段选择器”，使用它，单击几下鼠标就可将现成的代码块插入到活动文档中。

 显示“代码片段选择器”的过程根据用户所使用的语言会有所不同。

- [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]：在代码编辑器中所需的位置处右击，以显示快捷菜单，然后选择“插入片段”。

- [!INCLUDE[csprcs](../../includes/csprcs-md.md)]：在代码编辑器中所需的位置处右击，以显示快捷菜单，然后单击“插入片段”或“外侧代码”。

- [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)]：“代码片段选择器”不可用。

- Visual F#：“代码片段选择器”不可用。

- [!INCLUDE[jsprjscript](../../includes/jsprjscript-md.md)]：在代码编辑器中所需的位置处右击，以显示快捷菜单，然后单击“插入片段”或“外侧代码”。

- XML：在代码编辑器中所需的位置处右击，以显示快捷菜单，然后单击“插入片段”或“外侧代码”。

- HTML：在代码编辑器中所需的位置处右击，以显示快捷菜单，然后单击“插入片段”或“外侧代码”。

- SQL：在代码编辑器中所需的位置处右击，以显示快捷菜单，然后单击“插入片段”。

  在大多数 Visual Studio 开发语言中，可以使用“代码片段管理器”将文件夹添加到“文件夹列表”，“代码片段选择器”会在该列表中扫描 XML 片段文件。 也可以创建自己的片段添加到该列表。 有关详细信息，请参阅[演练：创建代码片段](../../ide/walkthrough-creating-a-code-snippet.md)。

## <a name="uielement-list"></a>UIElement 列表
 项名称一个可编辑的文本字段，它显示在 "**项" 列表**中选定的项的名称。 若要执行渐进式搜索以查找所需的项，请首先在此字段中键入其名称。 继续添加字母，直到在“项列表”中选定所需的项。

 项列出可插入的代码片段列表，或包含代码段的文件夹的列表。 若要插入片段或展开文件夹，请选择所需的项，然后按 Enter。

## <a name="see-also"></a>请参阅
 [使用代码片段的最佳做法](../../ide/best-practices-for-using-code-snippets.md) [Visual Basic IntelliSense 代码段](https://msdn.microsoft.com/library/ffdde4c9-8141-4906-b09b-15181357a643)[设置代码中的书签](../../ide/setting-bookmarks-in-code.md)[如何：使用外侧代码片段](../../ide/how-to-use-surround-with-code-snippets.md)
