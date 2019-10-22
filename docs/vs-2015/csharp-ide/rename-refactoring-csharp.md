---
title: 重命名重构C#（） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vs.csharp.refactoring.rename
dev_langs:
- CSharp
helpviewer_keywords:
- refactoring [C#], Rename
- Rename refactoring [C#]
ms.assetid: 268942fc-b142-4dfa-8d90-bedd548c2e4f
caps.latest.revision: 45
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 0db7696268e5e3d24d005fbf35a08b330f2dc849
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667481"
---
# <a name="rename-refactoring-c"></a>重命名重构 (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**重命名**是 Visual Studio 集成开发环境（IDE）中的一项重构功能，它提供了一种简单的方法来重命名代码符号的标识符，如字段、本地变量、方法、命名空间、属性和类型。 **Rename**可用于更改注释和字符串中的名称，以及更改标识符的声明和调用。

> [!NOTE]
> 使用 Visual Studio 的源代码管理时，请先获取最新版本的源，然后再尝试执行重命名重构。

 可从以下 Visual Studio 功能获得重命名重构：

|功能|IDE 中重构的行为|
|-------------|----------------------------------------|
|代码编辑器|在代码编辑器中，将光标置于特定类型的代码符号上时，可使用 "重命名" 重构。 当光标位于此位置时，可以通过键入键盘快捷方式（CTRL + R、CTRL + R）或从智能标记、快捷菜单或 "**重构**" 菜单中选择 "**重命名**" 命令，来调用 "**重命名**" 命令。|
|类视图|在类视图中选择标识符时，可以从快捷菜单和 "**重构**" 菜单中选择 "重命名" 重构。|
|对象浏览器|在对象浏览器中选择标识符时，只能从 "**重构**" 菜单中使用 "重命名重构"。|
|Windows 窗体设计器的属性网格|在 Windows 窗体设计器的**属性网格**中，更改控件的名称将为该控件启动重命名操作。 "**重命名**" 对话框不会出现。|
|“解决方案资源管理器”|在**解决方案资源管理器**中，快捷菜单上有一个 "**重命名**" 命令。 如果选定的源文件包含类名称与文件名相同的类，则可以使用此命令同时重命名源文件和执行重命名重构。<br /><br /> 例如，如果您创建一个基于 Windows 的默认应用程序，然后将 Form1.cs 重命名为 TestForm.cs，则源文件名称 Form1.cs 将更改为 TestForm.cs，类 Form1 以及对该类的所有引用都将被重命名为 TestForm。 **注意：** "**撤消**" 命令（CTRL + Z）将只撤消代码中的重命名重构，而不会将文件名更改回原始名称。 <br /><br /> 如果所选的源文件不包含名称与文件名相同的类，则**解决方案资源管理器**中的 "**重命名**" 命令将仅重命名源文件，而不会执行重命名重构。|

## <a name="rename-operations"></a>重命名操作
 执行**重命名**时，重构引擎执行特定于每个代码符号的重命名操作，如下表所述。

|代码符号|重命名操作|
|-----------------|----------------------|
|字段|将该字段的声明和用法更改为新名称。|
|局部变量|将变量的声明和用法更改为新名称。|
|方法|将方法的名称和对该方法的所有引用更改为新名称。 **注意：** 重命名扩展方法时，重命名操作将传播到处于范围内的方法的所有实例，而不考虑扩展方法是用作静态方法还是实例方法。 有关详细信息，请参阅[扩展方法](https://msdn.microsoft.com/library/175ce3ff-9bbf-4e64-8421-faeb81a0bb51)。|
|Namespace|将命名空间的名称更改为声明中的新名称、所有 `using` 语句和完全限定的名称。 **注意：** 重命名命名空间时，[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 还会更新 "**项目设计器**" 的 "**应用程序**" 页上的 "**默认命名空间**" 属性。 通过从 "**编辑**" 菜单中选择 "**撤消**"，无法重置此属性。 若要重置**默认命名空间**属性值，必须在 "**项目设计器**" 中修改属性。 有关详细信息，请参阅[应用程序页](../ide/reference/application-page-project-designer-csharp.md)。|
|Property|将属性的声明和用法更改为新名称。|
|键入|将类型的所有声明和所有用法都更改为新名称，包括构造函数和析构函数。 对于分部类型，重命名操作将传播到所有部分。|

#### <a name="to-rename-an-identifier"></a>重命名标识符

1. 创建名为 `RenameIdentifier` 的控制台应用程序，然后将 `Program` 替换为下面的示例代码。

    ```csharp
    class ProtoClassA
    {
        // Invoke on 'MethodB'.
        public void MethodB(int i, bool b) { }
    }

    class ProtoClassC
    {
        void D()
        {
            ProtoClassA MyClassA = new ProtoClassA();

            // Invoke on 'MethodB'.
            MyClassA.MethodB(0, false);
        }
    }
    ```

2. 将光标置于方法声明或方法调用中 `MethodB` 上。

3. 从 "**重构**" 菜单中，选择 "**重命名**"。 此时将显示 "**重命名**" 对话框。

     您还可以右键单击光标，指向上下文菜单上的 "**重构**"，然后单击 "**重命名**" 以显示 "**重命名**" 对话框。

4. 在 "**新建名称**" 字段中，键入 `MethodC`。

5. 选中 "**在注释中搜索**" 复选框。

6. 单击“确定”。

7. 在 "**预览更改**" 对话框中，单击 "**应用**"。

#### <a name="to-rename-an-identifier-using-smart-tags"></a>使用智能标记重命名标识符

1. 创建名为 `RenameIdentifier` 的控制台应用程序，然后将 `Program` 替换为下面的示例代码。

    ```csharp
    class ProtoClassA
    {
        // Invoke on 'MethodB'.
        public void MethodB(int i, bool b) { }
    }

    class ProtoClassC
    {
        void D()
        {
            ProtoClassA MyClassA = new ProtoClassA();

            // Invoke on 'MethodB'.
            MyClassA.MethodB(0, false);
        }
    }
    ```

2. 在 `MethodB` 的声明中，在方法标识符上键入或 backspace。 智能标记提示将显示在此标识符下。

    > [!NOTE]
    > 只能在标识符声明中使用智能标记调用重命名重构。

3. 键入键盘快捷方式 SHIFT + ALT + F10，然后按向下键显示智能标记菜单。

     或

     将鼠标指针移到智能标记提示符上方以显示智能标记。 然后，将鼠标指针移到智能标记上，并单击向下箭头以显示智能标记菜单。

4. 选择 "将 **\<identifer1 >" 重命名为 "\<identifier2 >"** 菜单项，以便在不预览代码更改的情况下调用重命名重构。 对 **\<identifer1 >** 的所有引用都将自动更新为 **\<identifier2 >** 。

     或

     选择 "**使用预览进行重命名**" 菜单项，通过对代码所做的更改进行预览来调用重命名重构。 将显示 "**预览更改**" 对话框。

## <a name="remarks"></a>备注

## <a name="renaming-implemented-or-overridden-members"></a>重命名实现或重写的成员
 当您**重命名**实现/重写的成员，或由其他类型中的成员实现/重写的成员时，[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 将显示一个对话框，该对话框指示重命名操作将导致级联更新。 如果单击 "**继续**"，则重构引擎将以递归方式查找和重命名基类型和派生类型中的所有成员，这些成员具有实现/替代与要重命名的成员的关系。

 下面的代码示例包含具有实现/重写关系的成员。

 [!code-csharp[CsUsingCsIDERefactor#1](../snippets/csharp/VS_Snippets_VBCSharp/CsUsingCsIDERefactor/CS/Class1.cs#1)]

 在上面的示例中，重命名 `C.Method()` 也会重命名 `Ibase.Method()`，因为 `C.Method()` 实现 `Ibase.Method()`。 接下来，重构引擎会以递归方式看到 `Ibase.Method()` 由 `Derived.Method()` 实现，`Derived.Method()` 重命名。 重构引擎不会重命名 `Base.Method()`，因为 `Derived.Method()` 不重写 `Base.Method()`。 除非在 "**重命名**" 对话框中选中了**重命名重载**，否则重构引擎将在此处停止。

 如果检查了**重命名重载**，则重构引擎会将 `Derived.Method(int i)` 重命名，因为它重载了 `Derived.Method()`、`Base.Method(int i)`，因为它是由 `Derived.Method(int i)` 重写的，并且 `Base.Method()` 因为它是 `Base.Method(int i)` 的重载。

> [!NOTE]
> 重命名在引用的程序集中定义的成员时，将出现一个对话框，说明重命名将导致生成错误。

## <a name="renaming-properties-of-anonymous-types"></a>重命名匿名类型的属性
 在匿名类型中重命名属性时，重命名操作将传播到具有相同属性的其他匿名类型的属性。 下面的示例阐释了这一行为。

```csharp
var a = new { ID = 1};
var b = new { ID = 2};
```

 在前面的代码中，重命名 `ID` 会更改两个语句 `ID`，因为它们具有相同的基础匿名类型。

```csharp
var companyIDs =
    from c in companylist
    select new { ID = c.ID, Name = c.Name};

var orderIDs =
    from o in orderlist
    select new { ID = o.ID, Item = o.Name};
```

 在前面的代码中，重命名 `ID` 仅会重命名 `ID` 的一个实例，因为 `companyIDs` 和 `orderIDs` 不具有相同的属性。

## <a name="see-also"></a>请参阅
 [重构（C#）](../csharp-ide/refactoring-csharp.md) [匿名类型](https://msdn.microsoft.com/library/59c9d7a4-3b0e-475e-b620-0ab86c088e9b)