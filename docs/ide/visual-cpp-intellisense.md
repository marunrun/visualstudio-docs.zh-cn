---
title: C++ IntelliSense
ms.date: 10/08/2018
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: markl
ms.workload:
- cplusplus
ms.openlocfilehash: c0d1be12f733a858bf223fb1dce6a091c0dc6c50
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75594209"
---
# <a name="visual-c-intellisense-features"></a>Visual C++ IntelliSense 功能

IntelliSense 是使编码更方便的一组功能的名称。 用于 C++ 的 IntelliSense 可用于独立文件及作为 C++ 项目一部分的文件。 在跨平台项目中，一些 IntelliSense 功能可用于共享代码项目中的 .cpp  和 .c  文件，甚至在处于 Android 或 iOS 上下文中也可以。

本文概述了 C++ IntelliSense 功能。 若要详细了解如何为项目配置 IntelliSense，以及如何排查问题，请参阅[为 C++ 项目配置 IntelliSense](visual-cpp-intellisense-configuration.md)。

## <a name="intellisense-features-in-c"></a>C++ 中的 IntelliSense 功能

IntelliSense 是使编码更方便的一组功能的名称。 由于不同的人对方便的定义有着不同的看法，几乎所有的 IntelliSense 功能都可以在“选项”  对话框中的“文本编辑器”   > “C/C++”   > “高级”  下启用或禁用。 可从菜单栏上的“工具”  菜单中访问“选项”  对话框。

![“工具选项”对话框](../ide/media/sintellisensecpptoolsoptions.PNG)

可以使用下图所示的菜单项和键盘快捷方来访问 IntelliSense。

![IntelliSense 菜单](../ide/media/vs2015_cpp_intellisense_menu.png)

## <a name="statement-completion-and-member-list"></a>语句完成和成员列表

当你开始键入关键字、类型、函数、变量名称或编译器可识别的其他程序元素时，编辑器会主动为你完成单词。

有关图标及其含义的列表，请参阅[类视图和对象浏览器图标](../ide/class-view-and-object-browser-icons.md)。

![Visual C++ 完成单词窗口](../ide/media/vs2015_cpp_complete_word.png)

首次调用成员列表时，它只显示当前上下文可访问的成员。 如果在此操作后按 Ctrl  +J  ，它将显示所有成员，而不考虑可访问性。 如果第三次调用它，则显示更宽的程序元素列表。 可在“选项”  对话框中的“文本编辑器”   > “C/C++”   > “常规”   > “自动列出成员”  下关闭“成员列表”。

![Visual C++ 成员列表](../ide/media/vs2015_cpp_list_members.png)

## <a name="parameter-help"></a>参数帮助

当你在类模板变量声明上键入函数调用的左大括号或尖括号时，该编辑器将显示具有函数或构造函数的每个重载的参数类型的小窗口。 基于光标所在的位置的“current”参数以粗体显示。 可在“选项”  对话框中的“文本编辑器”   > “C/C++”   > “常规”   > “参数信息”  下关闭“参数信息”。

![Visual C++ 参数帮助](../ide/media/vs_2015_cpp_param_help.png)

## <a name="quick-info"></a>快速信息

将鼠标光标悬停在变量上时，将在内联出现一个小窗口，显示类型信息和在其中定义该类型的标头。 将鼠标悬停在函数调用上，以查看该函数的签名。 可在“选项”  对话框中的“文本编辑器”   > “C/C++”   > “高级”   > “自动快速信息”  下关闭“快速信息”。

![Visual C++ QuickInfo](../ide/media/vs2015_cpp_quickinfo.png)

## <a name="error-squiggles"></a>错误波形曲线

程序元素（变量、关键字、大括号、类型名称等）下的波形曲线提醒你注意代码中的错误或潜在错误。 当你编写前向声明时，会出现绿色波形曲线，提醒你仍然需要编写实现。 当未处于活动状态的代码中出现错误（例如，当你在 Windows 上下文中工作，但输入将在 Android 上下文中成为错误的内容时）时，紫色波形曲线将出现在共享项目中。 红色波形曲线指示处于活动状态的代码中存在需要处理的编译器错误或警告。

![Visual C++ 错误波形曲线](../ide/media/vs2015_cpp_error_quiggles.png)

### <a name="code-colorization-and-fonts"></a>代码着色和字体

可在“选项”  对话框中的“环境”   > “字体和颜色”  下更改默认颜色和字体。 你可以在此处更改多个 UI 窗口（而不仅仅是编辑器）的字体。 特定于 C++ 的设置以“C++”开头；其他设置适用于所有语言。

## <a name="cross-platform-intellisense"></a>跨平台的 IntelliSense

在共享代码项目中，即使你正在 Android 上下文中工作，某些 IntelliSense 功能（如波形曲线）仍可用。 如果你编写一些可能在非活动状态的项目中导致错误的代码，IntelliSense 仍显示波形曲线，但它们显示的颜色与当前上下文中的错误的波形曲线相比不同。

请考虑配置为针对 Android 和 iOS 进行生成的 OpenGLES 应用程序。 图中显示的是正在编辑的共享代码。 在此图中，活动项目是 iOS.StaticLibrary  ：

![iOS 被选作活动项目。](../ide/media/intellisensecppcrossplatform2.png)

注意下列事项：

- 第 6 行的 `#ifdef` 分支呈灰色，指示非活动状态的区域，因为 `__ANDROID__` 不是针对 iOS 项目定义的。

- 第 11 行的问候语变量通过标识符 `HELLO` 进行初始化，该标识符现在具有红色波形曲线。 这是因为当前处于活动状态的 iOS 项目中没有定义任何标识符 `HELLO`。

- 第 12 行的标识符 `BYE` 上具有紫色波形曲线，因为（当前）处于非活动状态的 Android.NativeActivity 项目中未定义此标识符  。 即使此行在 iOS 为活动项目时编译，它也不会在 Android 为活动项目时编译。 因为这是共享代码，所以应更改代码，即使该代码是在当前处于活动状态的配置中进行编译也是如此。

如果将活动项目更改为 Android，则波形曲线会发生变化：

- 第 8 行的 `#else` 分支呈灰色，指示非活动状态的区域，因为 `__ANDROID__` 是针对 Android 项目定义的。

- 第 11 行的问候语变量通过标识符 `HELLO` 进行初始化，该标识符具有紫色波形曲线。 这是因为当前处于非活动状态的 iOS 项目中没有定义任何标识符 `HELLO`。

- 第 12 行的标识符 `BYE` 上具有红色波形曲线，因为活动项目中未定义此标识符。

## <a name="intellisense-for-stand-alone-files"></a>用于独立文件的 IntelliSense

当你在任何项目外部打开单个文件时，你仍然会得到 IntelliSense。 可在“选项”  对话框中的“文本编辑器”   > “C/C++”   > “高级”  下，启用或禁用特定 IntelliSense 功能。 若要为不属于项目的单个文件配置 IntelliSense，请参见“IntelliSense 和浏览非项目文件”  部分。

![Visual C++ 单个文件 Intellisense](../ide/media/vs2015_cpp_single_file_intellisense.png)

默认情况下，单个文件 IntelliSense 仅使用标准包含目录来查找头文件。 若要添加其他目录，请打开“解决方案”  节点上的快捷菜单，然后将目录添加到“调试源代码”  列表中，如下图所示：

![添加指向头文件的路径。](../ide/media/intellisensedebugyourcode.jpg)

## <a name="enable-or-disable-features"></a>启用或禁用功能

由于不同的人对方便的定义有着不同的看法，几乎所有的 IntelliSense 功能都可以在“选项”  对话框中的“文本编辑器”   > “C/C++”   > “高级”  下启用或禁用。 可从菜单栏上的“工具”  菜单中访问“选项”  对话框。

![“工具选项”对话框](../ide/media/sintellisensecpptoolsoptions.PNG)

## <a name="see-also"></a>请参阅

- [使用 IntelliSense](../ide/using-intellisense.md)
- [为 C++ 项目配置 IntelliSense](visual-cpp-intellisense-configuration.md)
