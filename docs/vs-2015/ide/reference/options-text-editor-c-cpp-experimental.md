---
title: “选项”->“文本编辑器”->“C/C++”->“实验”| Microsoft Docs
ms.date: 11/15/2016
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.C/C++.Experimental
- VS.ToolsOptionsPages.Text_Editor.C%2FC%2B%2B.Experimental
- VS.ToolsOptionsPages.Text_Editor.C\C++.Experimental
ms.assetid: b9e9dda2-350c-460d-b368-37d6c5342eee
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5979363f16f2e9d78a2f50ffbb6511d03146caaa
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297852"
---
# <a name="options-text-editor-cc-experimental"></a>选项, 文本编辑器, C/C++, 实验
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

通过更改这些选项，你可以在用 C 或 C++ 进行编程时更改与 IntelliSense 和浏览数据库有关的行为。

 若要访问此页，请在“选项” 对话框的左窗格中，展开“文本编辑器”，再展开“C/C++”，然后选择“实验”。

 这些功能在 Visual Studio 2015 Update 1 RC 安装中可用。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 请参阅[在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。

## <a name="browsingnavigation"></a>浏览/导航
 **启用新数据库引擎**这应该会自动提高数据库填充速度，并使所有数据库操作更快（不损失准确性）执行操作（例如，"**转向定义**" 和 "**查找所有引用**"）的速度。 （只需关闭并重新打开你的解决方案即可应用所做的更改；不需要重新启动 Visual Studio。）

## <a name="intellisense"></a>IntelliSense
 **成员列表点到箭头**当适用于成员列表时，将 "." 替换为 "->"。

## <a name="refactoring"></a>Refactoring
 **启用提取函数**将所选代码提取到它自己的函数，并将代码替换为对新函数的调用。 若要访问此功能，请右键单击所选代码并选择“快速操作”，或只需按默认快捷键 Ctrl + 点 [Ctrl+.]。

 **启用更改签名**添加、重新排列和删除函数的参数并将更改传播到所有调用站点。 若要访问此功能，请右键单击任何函数使用情况并选择“快速操作”，或只需按默认快捷键 Ctrl + 点 [Ctrl+.]。

## <a name="text-editor"></a>文本编辑器
 **启用展开作用域**如果启用，则可以通过在文本编辑器中键入 "{"，将选定的文本括在大括号内。

 **启用展开优先级**如果启用，则可以通过在文本编辑器中键入 ' （' 来包围选定文本和括号。

 有关 Visual Studio 库上的其他文本编辑器功能，请参阅 [此处](https://go.microsoft.com/fwlink/?LinkId=692016)列表。 一个示例是 [C++ 快速修补](https://visualstudiogallery.msdn.microsoft.com/be91feef-8dc3-4f7a-ac9f-f34e7ca5918f)，它支持以下内容：

- **添加缺少的 #include** - 建议对你代码中的未知符号使用相关的 #include

- **添加 using namespace/Fully qualify symbol** - 与上一项类似，但是是用于命名空间

- **添加缺少的分号**

- **MSDN 帮助** - 搜索用于你的错误消息的 MSDN

  你可以将鼠标悬停在波浪线上以获取灯泡，或者使用默认键盘快捷键 Ctrl+点 (Ctrl+.)。 注意，对于键盘快捷方式，你的插入点无需定位在特定的错误或令牌上；你只需将其与错误置于同一行，以调用该行上任何内容的建议。

## <a name="see-also"></a>请参阅
 [在C++中](https://devblogs.microsoft.com/cppblog/all-about-c-refactoring-in-visual-studio-2015-preview/)[设置特定于语言的编辑器选项](../../ide/reference/setting-language-specific-editor-options.md)重构（VC 博客）
