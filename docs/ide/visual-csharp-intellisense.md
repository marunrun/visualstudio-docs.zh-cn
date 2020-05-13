---
title: C# IntelliSense
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- C#, IntelliSense
- IntelliSense [C#]
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 2ed5d86599fa99b9c1360b414b37ef95ab59082d
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "79307255"
---
# <a name="c-intellisense"></a>C# IntelliSense

在编辑器中进行编码以及在[即时模式](../ide/reference/immediate-window.md)命令窗口进行调试时，可以使用 C# IntelliSense。

## <a name="completion-lists"></a>完成列表

C# 中的 IntelliSense 完成列表包含来自列表成员、完成单词等的标记。 它提供到以下内容的快速访问：

- 类型或命名空间的成员

- 变量、命令和函数名称

- 代码片段

- 语言关键字

- 扩展方法

C# 中的完成列表也足够智能，可筛选出不相关的标记，并可基于上下文预先选择标记。 有关详细信息，请参阅[经过筛选的完成列表](#filtered-completion-lists)。

### <a name="code-snippets-in-completion-lists"></a>完成列表中的代码片段

在 C# 中，完成列表包含代码片段，可帮助你将预定义的代码正文轻松插入程序。 代码片段作为片段的[快捷方式文本](../ide/code-snippets-schema-reference.md#shortcut-element)出现在完成列表中。 有关 C# 中默认情况下可用的代码片段的详细信息，请参阅 [C# 代码片段](../ide/visual-csharp-code-snippets.md)。

### <a name="language-keywords-in-completion-lists"></a>完成列表中的语言关键字

在 C# 中，完成列表还包括语言关键字。 若要详细了解 C# 语言关键字，请参阅 [C# 关键字](/dotnet/csharp/language-reference/keywords/index)。

### <a name="extension-methods-in-completion-lists"></a>完成列表中的扩展方法

在 C# 中，完成列表包含位于作用域的扩展方法。

> [!NOTE]
> 完成列表不显示 <xref:System.String> 对象的所有扩展方法。

扩展方法使用不同于实例方法的图标。 有关列表图标的参考指南，请参阅[类视图和对象浏览器图标](../ide/class-view-and-object-browser-icons.md)。 当具有相同名称的实例方法和扩展方法都处于作用域时，完成列表将显示扩展方法图标。

### <a name="filtered-completion-lists"></a>经过筛选的完成列表

IntelliSense 使用筛选器从完成列表中删除不必要的成员。 C# 对针对这些项出现的完成列表进行筛选：

- 接口和基类  ：IntelliSense 自动从接口和基类完成列表、类声明基类和接口列表和约束列表中移除项。 例如，枚举不会出现在基类的完成列表中，因为枚举无法用于基类。 基类的完成列表仅包含接口和命名空间。 如果在列表中选择一个项，再键入逗号，则 IntelliSense 将从完成列表移除基类，因为 C# 不支持多重继承。 相同的行为也发生在约束子句中。

- **特性**：将特性应用于类型时，对完成列表进行筛选，从而使列表仅包含源自包含那些类型的命名空间的类型，如 <xref:System.Attribute>。

- Catch 子句 

- 对象初始值设定项  ：完成列表中将仅列出可进行初始化的成员。

- **关键字**：键入 `new` 并按空格键后  ，将显示完成列表。 基于代码的上下文将在列表中自动选择项。 例如，自动为声明和方法中的 return 语句在完成列表中选择项。

- **enum 关键字**：在枚举赋值的等号后按空格键  ，将显示完成列表。 基于代码的上下文将在列表中自动选择项。 例如，键入关键字 return 之后以及进行声明时，将在完成列表中自动选择项。

- **as 和 is 运算符**：键入 **或** 关键字后按空格键`as``is`，将自动显示经过筛选的完成列表。

- 事件  ：当键入关键字 `event` 时，完成列表仅包含委托类型。

- 当输入参数时，  参数将帮助自动根据匹配参数的首个方法重载进行排序。 如果有多个可用的方法重载，则可使用向上和向下箭头导航到列表中下一个可能的重载。

### <a name="most-recently-used-members"></a>最近使用的成员

IntelliSense 会记住最近在自动完成对象名称的[列表成员](../ide/using-intellisense.md)弹出框中选择的成员。 下次使用成员列表  时，将在顶部显示最近使用过的成员。 在每个 Visual Studio 会话之间，最近使用过的成员的历史记录将被清除。

### <a name="override"></a>override

键入 [override](/dotnet/csharp/language-reference/keywords/override) 并按空格键  后，IntelliSense 将在弹出的列表框中显示可以替代的全部有效基类成员。 在 `override` 之后键入方法的返回类型会提示 IntelliSense 仅显示返回相同类型的方法。 如果 IntelliSense 找不到任何匹配项，它会显示全部基类成员。

### <a name="ai-enhanced-intellisense"></a>AI-enhanced IntelliSense

[Visual Studio IntelliCode](/visualstudio/intellicode/intellicode-visual-studio) 提供人工智能改进的 IntelliSense 完成列表。 IntelliCode 预测供使用的最可能正确的 API，而不仅仅是呈现按字母顺序排列的成员列表。 它使用当前的代码上下文和模式来提供此动态列表。

## <a name="automatic-code-generation"></a>自动代码生成

### <a name="add-using"></a>添加 using

“添加 using”  IntelliSense 操作会自动向代码文件中添加所需 `using` 指令。 此功能能够使你专注于编写的代码上，而无需将注意力转换到代码的另一部分。

若要启动“添加 using”  操作，请将光标放在无法解析的类型引用上。 例如，创建控制台应用程序并将 `XmlReader` 添加到 `Main` 方法主体时，该代码行上将出现一条红色波浪线，因为无法解析该类型引用。 然后可以通过“快速操作”调用“添加 using”   。 只有当光标位于未绑定类型上时，才可看见“快速操作”  。

![添加 using、快速操作展开图像](../ide/media/addusing-quickaction.png)

单击错误灯泡图标，然后选择“using System.Xml;”  自动添加 using 指令。

### <a name="remove-and-sort-usings"></a>对 Using 进行删除和排序

“对 Using 进行删除和排序”选项对 **和** 声明进行排序和删除，而无需更改源代码的行为`using``extern`。 一段时间后，由于不必要和未经组织的`using`指令，源文件可能会变得臃肿且难以读取。 “对 Using 进行删除和排序”选项通过删除未使用的  **指令来压缩源代码，并通过对其进行排序提高可读性**`using`。 在“编辑”菜单上，选择“IntelliSense”，然后选择“组织 Using”    。

### <a name="implement-interface"></a>实现接口

IntelliSense 提供了一个选项，有助于在使用代码编辑器时实现[接口](/dotnet/csharp/language-reference/keywords/interface)。 通常情况下，若要正确实现接口，必须为类中接口的每个成员创建一个方法声明。 通过使用 IntelliSense，在类声明中键入接口名称后，将显示“快速操作”  灯泡。 该灯泡提供通过使用显式或隐式命名自动实现接口的选项。 在显式命名下，方法声明带有接口的名称。 在隐式命名下，方法声明不指示它们所属的接口。 只有通过接口实例（而不是类实例）才能访问显式命名的接口方法。 有关详细信息，请参阅[显式接口实现](/dotnet/csharp/programming-guide/interfaces/explicit-interface-implementation)。

实现接口将生成满足接口所需的最小数量的方法存根。 如果基类实现部分接口，则不会重新生成这些存根。

### <a name="implement-abstract-base-class"></a>实现抽象基类

IntelliSense 提供了一个选项，有助于在使用代码编辑器时自动实现抽象基类的成员。 通常情况下，实现抽象基类的成员需要在你的派生类中为抽象基类的每个方法创建新的方法定义。 使用 IntelliSense，在类声明中键入抽象基类的名称后，将显示“快速操作”  灯泡。 该灯泡将提供自动实现基类方法的选项。

通过“实现抽象基类  ”功能生成的方法存根将由文件 MethodStub.snippet  中定义的代码片段进行建模。 代码片段是可修改的。 有关详细信息，请参阅[演练：创建代码片段](../ide/walkthrough-creating-a-code-snippet.md)。

### <a name="generate-from-usage"></a>使用时生成

通过“使用时生成”  功能，用户能够在定义类和成员之前使用它们。 你可以为想要使用但尚未定义的任何类、构造函数、方法、属性、字段或枚举生成存根。 可以生成新的类型和成员而无需离开你在代码中的当前位置。 这将使工作流的中断降至最低。

每个未定义标识符下都会显示一条红色波浪下划线。 将鼠标指针停留在标识符上时，工具提示中将显示一条错误消息。 若要显示相应的选项，可以使用以下过程之一：

- 单击未定义的标识符。 标识符下将出现一个“快速操作”  错误灯泡。 单击错误灯泡。

- 单击未定义的标识符，然后按 Ctrl **.** +  （Ctrl + 句点）  。

- 右键单击未定义的标识符，然后单击“快速操作和重构”  。

显示的选项可包括以下选项：

- 生成属性 

- 生成字段 

- 生成方法 

- **生成类**

- **生成新类型**（对于类、结构、接口或枚举）

## <a name="generate-event-handlers"></a>生成事件处理程序

在代码编辑器中，IntelliSense 有助于将方法（事件处理程序）挂钩到事件字段。

在 .cs`+=`*文件中的一个事件字段后键入* 运算符时，IntelliSense 提示你按 Tab  这一选项。 这会插入委托的新实例，该委托指向处理事件的方法。

![按钮自动挂钩](../ide/media/vxautohookup.gif)

如果按 Tab，IntelliSense 将自动完成该语句，并在代码编辑器中将事件处理程序引用显示为所选文本  。 若要完成自动事件挂钩，IntelliSense 会提示你再次按 Tab 键，以便为事件处理程序创建空的存根  。

![生成事件处理程序](../ide/media/vxgenerateeventhandler.gif)

> [!NOTE]
> 如果由 IntelliSense 创建的新委托引用现有的事件处理程序，IntelliSense 将在工具提示中传达此信息。 然后，可以修改此引用；已在代码编辑器中选定该文本。 否则，自动事件挂钩将在此时完成。

如果按 Tab 键，IntelliSense 将引出具有正确签名的方法并将光标放在事件处理程序的正文中  。

> [!NOTE]
> 使用“视图”菜单上的“向后导航”命令 (Ctrl  ) 可返回到事件挂钩语句   + **-** 。

## <a name="see-also"></a>另请参阅

- [使用 IntelliSense](../ide/using-intellisense.md)
- [Visual Studio IDE](../get-started/visual-studio-ide.md)
