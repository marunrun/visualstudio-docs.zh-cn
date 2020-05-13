---
title: 选项, 文本编辑器, C/C++, 实验
ms.date: 08/02/2017
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.C/C++.Experimental
- VS.ToolsOptionsPages.Text_Editor.C%2FC%2B%2B.Experimental
- VS.ToolsOptionsPages.Text_Editor.C\C++.Experimental
author: corob-msft
ms.author: corob
manager: markl
ms.workload:
- cplusplus
ms.openlocfilehash: 7e239ad3d2091f334f18ec00a367fc47d5c21db3
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77278701"
---
# <a name="options-text-editor-cc-experimental"></a>选项, 文本编辑器, C/C++, 实验

通过更改这些选项，你可以在用 C 或 C++ 进行编程时更改与 IntelliSense 和浏览数据库有关的行为。 这些功能实际上是实验性的且可能会在 Visual Studio 将来版本中进行修改或删除。

::: moniker range="vs-2017"

本文介绍 Visual Studio 2017 中的各选项。 对于 Visual Studio 2015，请在目录上方的选择器中选择“2015”  。

::: moniker-end

要访问此属性页，请按 Ctrl+Q   以激活搜索框，然后键入“experimental”  。 在键入前几个字母后，搜索会查找该页面。 此外，还可以选择“工具” > “选项”，依次展开“文本编辑器”和“C/C++”，再选择“试验”      。

这些功能在 Visual Studio 安装中可用。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 请参阅[个性化设置 Visual Studio IDE](../../ide/personalizing-the-visual-studio-ide.md)。

## <a name="enable-predictive-intellisense"></a>启用预测 IntelliSense

预测 IntelliSense 限制 IntelliSense 下拉列表中显示的结果数，以便你仅看到与上下文相关的结果。 例如，如果键入 `int x =` 并调用 IntelliSense 下拉列表，只会看到整数或返回整数的函数。 预测 IntelliSense 在默认情况下是关闭的。

::: moniker range="vs-2017"

## <a name="enable-faster-project-load"></a>启用更快的项目加载

自 Visual Studio 2017 版本 15.3 起：此功能当前称为“启用项目缓存”，并已移至 [VC++ 项目设置](vcpp-project-settings-projects-and-solutions-options-dialog-box.md)属性页  。

此选项使 Visual Studio 能缓存项目数据，以便下次打开该项目时，它能直接加载缓存的数据，而无需通过项目文件重新对其计算。 使用缓存数据可显著缩短项目加载时间。

::: moniker-end

## <a name="additional-features-in-the-visual-studio-marketplace"></a>Visual Studio Marketplace 中的其他功能

可以在 [Visual Studio Marketplace](https://marketplace.visualstudio.com/search?target=VS&category=Tools&vsVersion=&subCategory=All&sortBy=Downloads) 中浏览其他文本编辑器功能。 一个示例是 [C++ 快速修补](https://marketplace.visualstudio.com/items?itemName=VisualCppDevLabs.CQuickFixes2017)，它支持以下内容：

- **添加缺少的 #include** - 建议对你代码中的未知符号使用相关的 #include

- **添加 using namespace/Fully qualify symbol** - 与上一项类似，但是是用于命名空间

- **添加缺少的分号**

- **联机帮助** - 在联机帮助中搜索错误消息

- 更多内容...

## <a name="see-also"></a>请参阅

- [设置语言特定的编辑器选项](../../ide/reference/setting-language-specific-editor-options.md)
- [在 C++ 中重构（VC 博客）](https://devblogs.microsoft.com/cppblog/all-about-c-refactoring-in-visual-studio-2015-preview/
)
