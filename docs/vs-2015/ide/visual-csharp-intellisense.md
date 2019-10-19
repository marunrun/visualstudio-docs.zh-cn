---
title: Visual C# IntelliSense | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense [J#]
- Visual C#, IntelliSense
- IntelliSense [C#]
ms.assetid: 79ca304d-dc1e-4dc9-a2a6-7808df2e588e
caps.latest.revision: 26
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 36803dfbba7ea6d6d2a869fb94c05105ed4af15d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72643339"
---
# <a name="visual-c-intellisense"></a>Visual C# IntelliSense
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在编辑器中进行编码以及在[即时模式](../ide/reference/immediate-window.md)命令窗口中进行调试时，可以使用 Visual C# IntelliSense。

## <a name="completion-lists"></a>完成列表
 Visual C# 中的 IntelliSense 完成列表包含来自列表成员、完成单词等的标记。 它提供到以下内容的快速访问：

- 类型或命名空间的成员，

- 变量、命令和函数名称，

- [代码片段](#CodeSnippets)，

- [语言关键字](#Keywords)，

- [扩展方法](#ExtensionMethods)

  C# 中的完成列表也足够智能，可筛选出不相关的标记，并可基于上下文预先选择标记。 有关详细信息，请参阅 [C# 中经过筛选的完成列表](../misc/filtered-completion-lists-in-csharp.md)和 [C# 中预选择的完成列表项](../misc/pre-selected-completion-list-items-in-csharp.md)。

### <a name="CodeSnippets"></a> 完成列表中的代码片段
 在 Visual C# 中，完成列表包含代码片段，可助你将预定义的代码体轻松插入程序。 代码片段作为片段的 [Shortcut 元素（Intellisense 代码片段）](https://msdn.microsoft.com/052cc97a-5c70-42f8-b398-4c3adf670cfa)出现在完成列表中。  若要了解 Visual C# 中默认情况下可用的代码片段，请参阅 [Visual C# 代码片段](../ide/visual-csharp-code-snippets.md)。

### <a name="Keywords"></a> 完成列表中的语言关键字
 在 Visual C# 中，完成列表还包括语言关键字。 若要了解 C# 语言关键字，请参阅 [C# 关键字](https://msdn.microsoft.com/library/e929b0f2-4b92-4d37-8060-23d323b098ad)。

### <a name="ExtensionMethods"></a> 完成列表中的扩展方法
 在 Visual C# 中，完成列表包含位于作用域的扩展方法。

> [!NOTE]
> 完成列表不显示 <xref:System.String> 对象的所有扩展方法。

 扩展方法使用不同于实例方法的图标。 若要了解列表图标的列表，请参阅[类视图和对象浏览器图标](../ide/class-view-and-object-browser-icons.md)。 当具有相同名称的实例方法和扩展方法都处于作用域时，完成列表将显示扩展方法图标。

### <a name="filtered-completion-lists"></a>经过筛选的完成列表
 IntelliSense 使用筛选器从完成列表中删除不必要的成员。

 Visual C# 对针对这些项出现的完成列表进行筛选：

- **接口和基类** IntelliSense 自动从接口和基类完成列表、类声明基类和接口列表和约束列表中移除项。 例如，枚举不会出现在基类的完成列表中，因为枚举无法用于基类。 基类的完成列表仅包含接口和命名空间。 如果在列表中选择一个项，再键入逗号，则 IntelliSense 从完成列表移除基类，因为 Visual C# 不支持多重继承。 相同的行为也发生在约束子句中。

- **特性**：将特性应用于类型时，对完成列表进行筛选，从而使列表仅包含源自包含那些类型的命名空间的类型，如 <xref:System.Attribute>。

- `as` 和 `is` 运算符。

- **Catch 子句**。

- **对象初始值设定项**：完成列表中将仅列出可进行初始化的成员。

- **新关键字**：键入 `new` 并按空格键后，将显示完成列表。 基于代码的上下文将在列表中自动选择项。 例如，自动为声明和方法中的 return 语句在完成列表中选择项。

- **as 和 is 运算符**：键入 `as` 或 `is` 关键字后按空格键，将自动显示经过筛选的完成列表。

- 事件：当键入关键字`event` 时，完成列表仅包含委托类型。

- 当输入参数时，参数将帮助自动根据匹配参数的首个方法重载进行排序。 如果有多个可用的方法重载，则可使用向上和向下箭头导航到列表中下一个可能的重载。

## <a name="most-recently-used-members"></a>最近使用的成员
 IntelliSense 会记住最近在自动完成对象名称的[列表成员](../ide/using-intellisense.md)弹出框中选择的成员。 下次使用成员列表时，将在顶部显示最近使用过的成员。 在 IDE 中的每个会话之间，最近使用过的成员的历史记录将被清除。

## <a name="override"></a>override
 键入 [override](https://msdn.microsoft.com/library/dd1907a8-acf8-46d3-80b9-c2ca4febada8)，然后按空格键后，IntelliSense 将在弹出的列表框中显示可以重写的全部有效基类成员。 在 `override` 之后键入方法的返回类型将提示 IntelliSense 仅显示返回相同类型的方法。 如果 IntelliSense 找不到任何匹配项，它将显示全部基类成员。

## <a name="automatic-code-generation"></a>自动代码生成

### <a name="add-using"></a>添加 using
 “添加 using IntelliSense”操作能够使你专注于编写的代码上，而无需将注意力转换到代码的另一部分。

 若要启动“添加 using”操作，请将光标放在无法解析的类型引用上。 例如，创建控制台应用程序并将 `XmlTextReader` 添加到 `Main` 方法主体时，`XmlTextReader` 最右边的字符下方将出现智能标记，因其显示为无法解析的类型引用。

 ![使用智能标记图像添加](../ide/media/addusesmart.gif "AddUseSmart")

 然后可以通过从“IntelliSense”菜单或上下文菜单的“解析”子菜单中选择“添加 using”来对其进行调用，或通过智能标记调用“添加 using”。 只有当光标位于未绑定的类型上或靠近它时，才可见智能标记。

 ![使用智能标记扩展图像添加](../ide/media/addusesmartexp.gif "AddUseSmartExp")

### <a name="organize-usings"></a>组织 using
 “组织 Using”选项对 `using` 和 `extern` 声明进行排序和删除，而无需更改源代码的行为。 一段时间后，由于不必要和未经组织的`using`指令，源文件可能会变得臃肿且难以读取。 “组织 Using”选项通过删除未使用的 `using` 指令来压缩源代码，并通过对其进行排序提高可读性。

 若要查看 Visual Studio IDE 中的可用选项，请在“编辑”菜单上，指向“IntelliSense”，然后指向“组织 Using”。 IDE 提供了以下选项来组织和删除`usings`指令：

### <a name="implement-interface"></a>实现接口
 IntelliSense 提供了一个选项，可帮助你在使用代码编辑器时实现[接口](https://msdn.microsoft.com/library/7da38e81-4f99-4bc5-b07d-c986b687eeba)。 通常情况下，若要正确实现接口，必须为类中接口的每个成员创建一个方法声明。 通过使用 IntelliSense，在类声明中键入接口名称后，将显示一个智能标记。 智能标记为你提供通过使用显式或隐式命名自动实现接口的选项。 在显式命名下，方法声明具有接口名称；在隐式命名下，方法声明不表示其所属的接口。 只有通过接口实例（而不是类实例）才能访问显式命名的接口方法。 有关详细信息，请参阅[显式接口实现](https://msdn.microsoft.com/library/181c901f-0d4c-4f29-97fc-895079617bf2)。

 实现接口将生成满足接口所需的最小数量的方法存根。 如果基类实现部分接口，则不会重新生成这些存根。

### <a name="implement-abstract-base-class"></a>实现抽象基类
 IntelliSense 提供了一个选项，可帮助你在使用代码编辑器时自动实现抽象基类的成员。 通常情况下，实现抽象基类的成员需要在你的派生类中为抽象基类的每个方法创建新的方法定义。 使用 IntelliSense，在类声明中键入抽象基类的名称后，将显示智能标记。 智能标记将提供自动实现基类方法的选项。

 通过“实现抽象基类”功能生成的方法存根将由文件 MethodStub.snippet 中定义的代码片段进行建模。 代码片段是可修改的。 有关详细信息，请参阅[演练：创建代码片段](../ide/walkthrough-creating-a-code-snippet.md)。

### <a name="generate-from-usage"></a>使用时生成
 通过“使用时生成”功能，用户能够在定义类和成员之前使用它们。 你可以为想要使用但尚未定义的任何类、构造函数、方法、属性、字段或枚举生成存根。 可以生成新的类型和成员而无需离开你在代码中的当前位置。 这将使工作流的中断降至最低。

 每个未定标识符下都显示一条波浪下划线。 将鼠标指针停留在标识符上时，工具提示中将显示一条错误消息。

 若要显示相应的选项，可以使用以下过程之一：

- 单击未定义的标识符。 在最左侧的字符下将显示一条短下划线。 将鼠标指针停留在短下划线上，将显示一个智能标记（图标）。 单击该智能标记。

- 单击未定义的标识符，然后按 CTRL+. （句点）。

- 右键单击未定义的标识符，然后单击“生成”。

  显示的选项可包括以下选项：

- **生成属性存根**

- **生成字段存根**

- **生成方法存根**

- **生成类**

- **生成新类型**（对于类、结构、接口或枚举）

## <a name="generate-event-handlers"></a>生成事件处理程序
 在代码编辑器中，IntelliSense 可帮助你将方法（事件处理程序）挂钩到事件字段。

 在 .cs 文件中的一个事件字段后键入 `+=` 运算符时，IntelliSense 提示你按 TAB 键这一选项。 这会插入委托的新实例，该委托指向处理事件的方法。

 ![按钮自动挂钩](../ide/media/vxautohookup.gif "vxAutoHookUp")

 如果按 TAB，IntelliSense 将自动为你完成该语句，并在代码编辑器中将事件处理程序引用显示为所选文本。 若要完成自动事件挂钩，IntelliSense 会提示你再次按 TAB 键，以便为事件处理程序创建空的存根。

 ![生成事件处理程序](../ide/media/vxgenerateeventhandler.gif "vxGenerateEventHandler")

> [!NOTE]
> 如果由 IntelliSense 创建的新委托引用现有的事件处理程序，IntelliSense 将在工具提示中传达此信息。 然后，可以修改此引用；已在代码编辑器中选定该文本。 否则，自动事件挂钩将在此时完成。

 如果按 TAB 键，IntelliSense 将引出具有正确签名的方法并将光标放在事件处理程序的正文中。

> [!NOTE]
> 使用“视图”菜单上的“向后导航”命令 (Ctrl+-) 可返回到事件挂钩语句。

 下面的任务演示 IntelliSense 如何自动将名为 `button1_Click` 的事件处理程序挂钩到名为 `button1.Click` 的事件字段。

## <a name="see-also"></a>请参阅
 [Visual Studio IDE](../ide/visual-studio-ide.md)
