---
title: 使用 Visual C++ 代码（类设计器） | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.cpplimitation
helpviewer_keywords:
- Visual C++, Class Designer
- Class Designer, Visual C++ support
- Class Designer, limitations
- Class Designer, tasks in Visual C++
- Visual C++, class diagrams
- C++, class diagrams
- C++, Class Designer
ms.assetid: f5b40921-2ef7-4de0-b595-45b44c79ffa6
caps.latest.revision: 27
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 020535ac73c48be74e56100c7b6f9c49b69e50dc
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75851305"
---
# <a name="working-with-visual-c-code-class-designer"></a>使用 Visual C++ 代码（类设计器）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

类设计器将显示一个称为*类图*的可视化设计图面，其在项目中提供代码元素的可视化表现形式。 可以使用类图来设计和可视化项目中的类和其他类型。

 类设计器支持以下 C++ 代码元素：

- 类（与托管类形状类似，只不过它可以具有多重继承关系）

- 匿名类（显示类视图为匿名类型生成的名称）

- 模板类

- 结构

- Enum

- 宏（显示宏的处理后视图）

- Typedef

> [!NOTE]
> 与 UML 类图不同的时你可以在建模项目中创建。 有关详细信息，请参阅 [UML 类图：参考](../modeling/uml-class-diagrams-reference.md)。

## <a name="troubleshooting-type-resolution-and-display-issues"></a>类型解析和显示问题的疑难解答

### <a name="location-of-source-files"></a>源文件的位置
 类设计器不会持续跟踪源文件的位置。 因此，如果修改项目结构或移动项目中的源文件，则类设计器会失去对类型的跟踪（尤其是 typedef、基类或关联类型的源类型）。 可能会收到错误，如“类设计器无法显示此类型”  。 如果收到错误，要将修改过的或被重新定位的源代码再次拖到类图中以重新显示。

### <a name="update-and-performance-issues"></a>更新和性能问题
 对于 Visual C++ 项目，在源文件中所做的更改要出现在类图中可能需要 30 到 60 秒的时间。 这种延迟也可能导致类设计器引发错误“选定内容中未找到任何类型”  。 如果收到此类错误，请在错误消息中单击“取消”  ，并等待代码元素出现在类视图中。 之后，类设计器应可以显示此类型。

 如果类图未使用你在代码中所做的更改进行更新，则可能需要关闭关系图，并重新打开它。

### <a name="type-resolution-issues"></a>类型解析问题
 以下原因可能会导致类设计器无法解析类型：

- 该类型所在的项目或程序集未从包含类图的项目进行引用。 若要纠正此错误，请添加一个对包含该类型的项目或程序集的引用。 有关详细信息，请参阅 [NIB 如何：使用“添加引用”对话框添加或移除引用](https://msdn.microsoft.com/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)。

- 由于该类型未处于正确的范围内，因此类设计器无法找到它。 确保代码未缺失 `using`、`imports` 或 `#include` 语句。 还请确保未将该类型（或相关类型）移出它原来所在的命名空间。

- 该类型不存在（或已被注释掉）。 若要更正此错误，请确保未注释掉或删除该类型。

- 类型位于由 #import 指令引用的库中。 可行的解决方法是：手动将生成的代码（.tlh 文件）添加到头文件的 #include 指令中。

  最有可能看到的有关类型解析问题的错误是：无法在类图“\<element>”中找到一个或多个形状的代码  。 此错误消息不一定表示你的代码错误。 它仅指示选件类设计器无法显示你的代码。 你可以尝试以下方法。

- 确保该类型存在。 确保你没有无意中注释掉或删除源代码。

- 确保类设计器支持你输入的类型。 请参阅 [C++ 代码元素的限制](#limitations)。

- 尝试解析的类型。 该类型所在的项目或程序集未从包含类图的项目进行引用。 若要纠正此错误，请添加一个对包含该类型的项目或程序集的引用。 有关详细信息，请参阅 [NIB 如何：使用“添加引用”对话框添加或移除引用](https://msdn.microsoft.com/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)。

- 确保该类型位于正确的范围，因此选件类设计器可以找到它。 确保代码未缺失 `using`、`imports` 或 `#include` 语句。 还请确保未将该类型（或相关类型）移出它原来所在的命名空间。

### <a name="troubleshooting-other-error-messages"></a>排除其他错误消息
 在 Microsoft Developer Network (MSDN) 公共论坛中，可以找到有关对错误和警告进行疑难解答的帮助。 请参阅 [Visual Studio 类设计器论坛](https://social.msdn.microsoft.com/Forums/en-US/vsclassdesigner/threads?page=1)。

## <a name="limitations"></a>C++ 代码元素的限制

- 当加载 Visual C++ 项目时，类设计器将以只读方式运行。 可以更改类图，但无法将类图的更改保存回源代码。

- 类设计器支持本机 C++ 语义。 对于编译为托管代码的 Visual C++ 项目，类设计器将仅可视化本机类型的代码元素。 因此，可以向项目添加类图，但类设计器将不允许你可视化其 `IsManaged` 属性设置为 `true` 的元素（即值类型和引用类型）。

- 对于 Visual C++ 项目，类设计器只能读取类型的定义。 例如，假定你在头 (.h) 文件中定义了一个类型并在实现 (.cpp) 文件中定义了其成员。 如果对实现 (.cpp) 文件调用“查看类图”，则类设计器不会显示任何内容。 又比如，如果对使用 `#include` 语句以包含其他文件但不包含任何实际类定义的 .cpp 文件调用“查看类图”，则类设计器也不会显示任何内容。

- 定义 COM 接口和类型库的 IDL (.idl) 文件不会显示在关系图中，除非将其编译为本机 C++ 代码。

- 类设计器不支持全局函数和变量。

- 类设计器不支持联合。 这是一种特殊类型的类，在其中仅分配联合的最大数据成员所需的内存量。

- 类设计器不显示基本数据类型，如 `int` 和 `char`。

- 类设计器不显示在当前项目外部定义的类型（如果此项目不具有对这些类型的正确引用）。

- 类设计器可以显示嵌套类型，但不能显示嵌套类型与其他类型之间的关系。

- 类设计器无法显示 void 类型或从 void 类型派生的类型。

## <a name="see-also"></a>另请参阅
 [设计和查看类和类型](../ide/designing-and-viewing-classes-and-types.md)使用类图和[其他类型（类设计器）](../ide/working-with-classes-and-other-types-class-designer.md)使用[类图（类设计器）设计类图（）](../ide/working-with-class-diagrams-class-designer.md) [设计类和类型（类设计器）](../ide/designing-classes-and-types-class-designer.md)在类设计器中的视觉对象[ C++枚举](../ide/visual-cpp-enumerations-in-class-designer.md)中[类设计器视觉对象C++ ](../ide/visual-cpp-structures-in-class-designer.md)枚举[ C++ ](../ide/visual-cpp-typedefs-in-class-designer.md)中的可视化[ C++类](../ide/visual-cpp-classes-in-class-designer.md)[添加有关类设计器错误的其他信息](../ide/additional-information-about-class-designer-errors.md)类设计器
