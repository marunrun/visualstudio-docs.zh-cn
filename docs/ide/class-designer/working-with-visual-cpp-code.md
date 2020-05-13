---
title: 使用 C++ 代码（类设计器）
ms.date: 06/21/2017
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.cpplimitation
helpviewer_keywords:
- C++, Class Designer
- Class Designer, C++ support
- Class Designer, limitations
- Class Designer, tasks in C++
- C++, class diagrams
- C++, class diagrams
- C++, Class Designer
ms.assetid: f5b40921-2ef7-4de0-b595-45b44c79ffa6
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 54087a719b0079ba32ff08ff1e08ad01f5e64ed0
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75596744"
---
# <a name="work-with-c-code-in-class-designer"></a>在类设计器中使用 C++ 代码

类设计器会显示一个称为类图的可视化设计曲面，它在项目中提供代码元素的可视化表现形式   。 可以使用类图来设计和可视化项目中的类和其他类型。

类设计器支持以下 C++ 代码元素  ：

- 类（与托管类形状类似，只不过它可以具有多重继承关系）

- 匿名类（显示类视图为匿名类型生成的名称）

- 模板类

- 结构

- Enum

- 宏（显示宏的处理后视图）

- Typedef

> [!NOTE]
> 与 UML 类图不同的时你可以在建模项目中创建。 有关详细信息，请参阅 [UML 类图：参考](../../modeling/what-s-new-for-design-in-visual-studio.md)。

## <a name="troubleshoot-type-resolution-and-display-issues"></a>类型解析和显示问题的疑难解答

### <a name="location-of-source-files"></a>源文件的位置

类设计器不会持续跟踪源文件的位置  。 因此，如果修改项目结构或移动项目中的源文件，则类设计器会失去对类型的跟踪（尤其是 typedef、基类或关联类型的源类型）  。 可能会收到错误，如“类设计器无法显示此类型”  。 如果收到错误，要将修改过的或被重新定位的源代码再次拖到类图中以重新显示。

### <a name="update-and-performance-issues"></a>更新和性能问题

对于 C++ 项目，在源文件中所做的更改要出现在类图中可能需要 30 到 60 秒的时间。 这种延迟也可能导致类设计器引发错误“选定内容中未找到任何类型”   。 如果收到此类错误，请在错误消息中单击“取消”，并等待代码元素出现在类视图中   。 之后，类设计器应该可以显示此类型  。

如果类图未使用你在代码中所做的更改进行更新，则可能需要关闭关系图，并重新打开它。

### <a name="type-resolution-issues"></a>类型解析问题

以下原因可能会导致类设计器无法解析类型  ：

- 该类型所在的项目或程序集未从包含类图的项目进行引用。 若要纠正此错误，请添加一个对包含该类型的项目或程序集的引用。 有关详细信息，请参阅[管理项目中的引用](../managing-references-in-a-project.md)。

- 由于该类型未处于正确的范围内，因此类设计器无法找到它  。 确保代码未缺失 `using`、`imports` 或 `#include` 语句。 还请确保未将该类型（或相关类型）移出它原来所在的命名空间。

- 该类型不存在（或已被注释掉）。 若要更正此错误，请确保未注释掉或删除该类型。

- 类型位于由 #import 指令引用的库中。 可行的解决方法是：手动将生成的代码（.tlh 文件）添加到头文件的 #include 指令中。

- 确保类设计器支持你输入的类型  。 请参阅 [C++ 代码元素的限制](#limitations-for-c-code-elements)。

最有可能看到的有关类型解析问题的错误是：无法在类图“**element>”中找到一个或多个形状的代码\<** 。 此错误消息不一定表示你的代码错误。 它仅指示选件类设计器无法显示你的代码。 你可以尝试以下方法：

- 确保该类型存在。 确保你没有无意中注释掉或删除源代码。

- 尝试解析的类型。 该类型所在的项目或程序集未从包含类图的项目进行引用。 若要纠正此错误，请添加一个对包含该类型的项目或程序集的引用。 有关详细信息，请参阅[管理项目中的引用](../managing-references-in-a-project.md)。

- 确保该类型位于正确的范围，因此选件类设计器可以找到它。 确保代码未缺失 `using`、`imports` 或 `#include` 语句。 还请确保未将该类型（或相关类型）移出它原来所在的命名空间。

### <a name="troubleshoot-other-error-messages"></a>其他错误消息的疑难解答

在 Microsoft Developer Network (MSDN) 公共论坛中，可以找到有关对错误和警告进行疑难解答的帮助。 请参阅 [Visual Studio 类设计器论坛](https://social.msdn.microsoft.com/Forums/en-US/home?forum=vsclassdesigner)。

## <a name="limitations-for-c-code-elements"></a>C++ 代码元素的限制

- 加载 C++ 项目时，类设计器  将以只读方式运行。 可以更改类图，但无法将类图的更改保存回源代码。

- 类设计器仅支持本机 C++ 语义  。 对于编译为托管代码的 C++ 项目，类设计器  将仅可视化本机类型的代码元素。 因此，可以向项目添加类图，但类设计器将不允许你可视化其 **属性设置为** 的元素（即值类型和引用类型）`IsManaged``true`。

- 对于 C++ 项目，类设计器  只能读取类型的定义。 例如，假定你在头 (.h) 文件中定义了一个类型并在实现 (.cpp) 文件中定义了其成员。 如果对实现 (.cpp) 文件调用“查看类图”，则类设计器不会显示任何内容  。 又比如，如果对使用 `#include` 语句以包含其他文件但不包含任何实际类定义的 .cpp 文件调用“查看类图”，则类设计器也不会显示任何内容  。

- 定义 COM 接口和类型库的 IDL (.idl) 文件不会显示在关系图中，除非将其编译为本机 C++ 代码。

- 类设计器不支持全局函数和变量  。

- 类设计器不支持联合  。 这是一种特殊类型的类，在其中仅分配联合的最大数据成员所需的内存量。

- 类设计器不显示基本数据类型，如 **和**`int``char`。

- 类设计器不显示在当前项目外部定义的类型（如果此项目没有对这些类型的正确引用）  。

- 类设计器可以显示嵌套类型，但不能显示嵌套类型与其他类型之间的关系  。

- 类设计器无法显示 void 类型或从 void 类型派生的类型  。

## <a name="see-also"></a>另请参阅

- [设计和查看类与类型](designing-and-viewing-classes-and-types.md)
- [有关类设计器错误的附加信息](additional-information-about-errors.md)
- [类设计器中的 C++ 类](visual-cpp-classes.md)
- [类设计器中的 C++ 结构](visual-cpp-structures.md)
- [类设计器中的 C++ 枚举](visual-cpp-enumerations.md)
- [类设计器中的 C++ Typedef](visual-cpp-typedefs.md)
