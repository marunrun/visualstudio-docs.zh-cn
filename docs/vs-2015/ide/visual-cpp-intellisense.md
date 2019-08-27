---
title: Visual C++ Intellisense | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 9d7c6414-4e6c-4889-a74c-a6033795eccc
caps.latest.revision: 11
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 2754a8ea663d888bb8ba2e2ff0276911976ff0af
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65696600"
---
# <a name="visual-c-intellisense"></a>Visual C++ Intellisense
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio 2015 中，IntelliSense 适用于单个代码文件以及项目中的文件。 在跨平台项目中，一些 IntelliSense 功能可用于共享代码项目中的 .cpp 和 .c 文件，甚至当你处于 Android 或 iOS 上下文中也可以。  
  
## <a name="intellisense-features-in-c"></a>C++ 中的 IntelliSense 功能  
 IntelliSense 是使编码更方便的一组功能的名称。 由于不同的人对方便的定义有着不同的看法，几乎所有的 IntelliSense 功能都可以在“文本编辑器、C/C++、高级”属性页中启用或禁用。  
  
 ![工具、选项、文本编辑器、C/C++、高级](../ide/media/sintellisensecpptoolsoptions.PNG "sIntelliSenseCppToolsOptions")  
  
 可以使用下图所示的菜单项和键盘快捷方来访问 IntelliSense。  
  
 ![“Visual C++ IntelliSense”菜单](../ide/media/vs2015-cpp-intellisense-menu.png "vs2015_cpp_intellisense_menu")  
  
### <a name="statement-completion-and-member-list"></a>语句完成和成员列表  
 当你开始键入关键字、类型、函数、变量名称或编译器可识别的其他程序元素时，编辑器会主动为你完成单词  
  
 有关图标及其含义的列表，请参阅[类视图和对象浏览器图标](../ide/class-view-and-object-browser-icons.md)。  
  
 ![“Visual C++ 完成单词”窗口](../ide/media/vs2015-cpp-complete-word.png "vs2015_cpp_complete_word")  
  
 首次调用成员列表时，它只显示当前上下文可访问的成员。 如果在此操作后使用 **Ctrl + J**，它将显示所有成员，而不考虑可访问性。 如果第三次调用它，则显示更宽的程序元素列表。 可在“C/C++ 常规选项”页中关闭语句完成。  
  
 ![Visual C++ 成员列表](../ide/media/vs2015-cpp-list-members.png "vs2015_cpp_list_members")  
  
### <a name="parameter-help"></a>参数帮助  
 当你在类模板变量声明上键入函数调用的左大括号或尖括号时，该编辑器将显示具有函数或构造函数的每个重载的参数类型的小窗口。 基于光标所在的位置的“current”参数以粗体显示。 可在“C/C++ 常规选项”页中关闭语句完成。  
  
 ![Visual C++ 参数帮助](../ide/media/vs-2015-cpp-param-help.png "vs_2015_cpp_param_help")  
  
### <a name="quick-info"></a>快速信息  
 将鼠标光标悬停在变量上时，将在内联出现一个小窗口，显示类型信息和在其中定义该类型的标头。 将鼠标悬停在函数调用上，以查看该函数的签名。 可在“文本编辑器、C/C++、高级”页上关闭快速信息。  
  
 ![Visual C++ 快速信息](../ide/media/vs2015-cpp-quickinfo.png "vs2015_cpp_quickInfo")  
  
## <a name="error-squiggles"></a>错误波形曲线  
 程序元素（变量、关键字、大括号、类型名称等）下的波形曲线提醒你注意代码中的错误或潜在错误。 当你编写前向声明时，会出现绿色波形曲线，提醒你仍然需要编写实现。 当未处于活动状态的代码中出现错误（例如，当你在 Windows 上下文中工作，但输入将在 Android 上下文中成为错误的内容时）时，紫色波形曲线将出现在共享项目中。 红色波形曲线指示处于活动状态的代码中存在需要处理的编译器错误或警告。  
  
 ![Visual C++ 错误波形曲线](../ide/media/vs2015-cpp-error-quiggles.png "vs2015_cpp_error_quiggles")  
  
## <a name="code-colorization-and-fonts"></a>代码着色和字体  
 通过使用“环境、字体和颜色”属性页可以更改默认颜色和字体。 你可以在此处更改多个 UI 窗口（而不仅仅是编辑器）的字体。 特定于 C++ 的设置以“C++”开头；其他设置适用于所有语言。  
  
## <a name="cross-platform-intellisense"></a>跨平台的 IntelliSense  
 在共享代码项目中，即使你正在 Android 上下文中工作，某些 IntelliSense 功能（如波形曲线）仍可用。 如果你编写一些可能在非活动状态的项目中导致错误的代码，IntelliSense 仍显示波形曲线，但它们显示的颜色与当前上下文中的错误的波形曲线相比不同。  
  
 以下是配置为针对 Android 和 iOS 进行构建的 OpenGLES 应用程序。 图中显示的是正在编辑的共享代码。 在第一张图中，Android 是活动项目：  
  
 ![Android 项目是活动项目。](../ide/media/intellisensecppcrossplatform.png "IntelliSenseCppCrossPlatform")  
  
 注意下列事项：  
  
- # 第 8 行的 else 分支呈灰色以指示非活动区域，因为`__ANDROID__`针对 Android 项目定义。  
  
- 第 11 行的问候语变量通过标识符 HELLO 进行初始化，该标识符具有紫色波形曲线。 这是因为当前处于非活动状态的 iOS 项目中没有定义任何标识符 HELLO。 第 11 行在 Android 项目中将进行编译，但在 iOS 项目中则不会进行编译。 这是共享代码，所以你应该做出一些更改，即使该代码是在当前处于活动状态的配置中进行编译也是如此。  
  
- 第 12 行的标识符 BYE 上具有红色波形曲线；当前选定的活动项目中未定义此标识符。  
  
  现在，将活动项目更改为 iOS.StaticLibrary，并注意波形曲线如何变化。  
  
  ![选择 iOS 作为活动项目。](../ide/media/intellisensecppcrossplatform2.png "IntelliSenseCppCrossPlatform2")  
  
  注意下列事项：  
  
- 第 6 行的 #ifdef 分支呈灰色，指示非活动的区域，因为 *_ANDROID\\*\_ 不是针对 iOS 项目定义的。  
  
- 第 11 行的问候语变量通过标识符 HELLO 进行初始化，该标识符现在具有红色波形曲线。 这是因为当前活动的 iOS 项目中没有定义任何标识符 HELLO。  
  
- 第 12 行的标识符 BYE 上具有紫色波形曲线；当前处于非活动状态的 Android.NativeActivity 项目中未定义此标识符。  
  
## <a name="single-file-intellisense"></a>单个文件 IntelliSense  
 当你在任何项目外部打开单个文件时，你仍然会得到 IntelliSense。 转到“文本编辑器、C/C++、高级”打开或关闭 IntelliSense 功能，即可启用或禁用特定功能。 若要为不属于项目的单个文件配置 IntelliSense，请在“高级”部分中查找“IntelliSense 和浏览非项目文件”。 请参阅 [Visual C++ 指导教程](https://msdn.microsoft.com/499cb66f-7df1-45d6-8b6b-33d94fd1f17c)。  
  
 ![Visual C++ 单个文件 intellisense](../ide/media/vs2015-cpp-single-file-intellisense.png "vs2015_cpp_single_file_intellisense")  
  
 默认情况下，单个文件 IntelliSense 仅使用标准包含目录来查找头文件。 若要添加其他目录，请打开解决方案节点上的快捷菜单，然后将你的目录添加到“调试源代码”列表中，如下图所示：  
  
 ![将路径添加到标头文件。](../ide/media/intellisensedebugyourcode.jpg "IntelliSenseDebugYourCode")  
  
## <a name="see-also"></a>请参阅  
 [使用 IntelliSense](../ide/using-intellisense.md)
