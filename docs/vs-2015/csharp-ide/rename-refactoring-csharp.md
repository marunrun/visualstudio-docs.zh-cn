---
title: 重命名重构 (C#) |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 3f1c31d858fbe7a5183456bfc7fcc1e602d4e051
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65686042"
---
# <a name="rename-refactoring-c"></a>重命名重构 (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**重命名**是 Visual Studio 集成的开发环境 (IDE) 提供了一种简单的方法可以重命名代码符号，例如字段、 局部变量、 方法、 命名空间、 属性和类型的标识符中的重构功能。 **重命名**只能更改在注释并在字符串中的名称，并且若要更改的声明和调用的标识符。  
  
> [!NOTE]
> 当使用针对 Visual Studio 源代码管理，再尝试执行重命名重构获取最新版本的源。  
  
 重命名重构为可从以下 Visual Studio 功能：  
  
|功能|在 IDE 中重构的行为|  
|-------------|----------------------------------------|  
|代码编辑器|当将光标置于特定类型的代码符号上，在代码编辑器中，重命名重构功能才可用。 如果光标位于此位置，可以调用**重命名**键入键盘快捷键 （CTRL + R、 CTRL + R），或选择命令**重命名**从智能标记、 快捷菜单上或命令**重构**菜单。|  
|类视图|类视图中选择一个标识符，重命名重构时，可以从快捷菜单并**重构**菜单。|  
|对象浏览器|对象浏览器中选择一个标识符，重命名重构后，才可从**重构**菜单。|  
|Windows 窗体设计器的属性网格|在中**属性网格**的 Windows 窗体设计器中，更改控件的名称将会启动该控件重命名操作。 **重命名**对话框不会出现。|  
|“解决方案资源管理器”|在中**解决方案资源管理器**即**重命名**命令出现在快捷菜单上。 如果选定的源代码文件包含其类名为的文件的名称相同的类，可以使用此命令以同时重命名的源文件，并执行重命名重构。<br /><br /> 例如，如果创建默认基于 Windows 的应用程序，然后将 Form1.cs 重命名为 TestForm.cs 源文件名 Form1.cs 将更改为 TestForm.cs 和 Form1 类和所有引用的类将重命名为 TestForm。 **注意：** **撤消**命令 (CTRL + Z) 将只撤消重命名重构代码中，并将的更改的文件名称回原始名称。 <br /><br /> 如果选定的源代码文件不包含其名称为文件名，与相同的类**重命名**命令，在**解决方案资源管理器**将仅重命名的源文件，而不会执行重命名重构。|  
  
## <a name="rename-operations"></a>重命名操作  
 当您执行**重命名**，重构引擎将在下表中所述执行特定于每个代码符号，重命名操作。  
  
|代码符号|重命名操作|  
|-----------------|----------------------|  
|字段|声明和此字段的用法更改为新的名称。|  
|本地变量|声明和变量的用法更改为新的名称。|  
|方法|该方法并对该方法的所有引用的名称更改为新名称。 **注意：** 当您重命名的扩展方法时，重命名操作将传播到方法的作用域，而不考虑扩展方法是否正在使用作为静态方法或实例方法中的所有实例。 有关详细信息，请参阅[扩展方法](https://msdn.microsoft.com/library/175ce3ff-9bbf-4e64-8421-faeb81a0bb51)。|  
|命名空间|命名空间的名称更改为新的名称在声明中，所有`using`语句和完全限定的名称。 **注意：** 重命名命名空间时[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]还会更新**Default Namespace**上的属性**应用程序**页**项目设计器**。 此属性不能通过选择重置**撤消**从**编辑**菜单。 若要重置**默认 Namespace**属性值，必须修改中的属性**项目设计器**。 有关详细信息，请参阅[应用程序页](../ide/reference/application-page-project-designer-csharp.md)。|  
|属性|声明和用法的属性更改为新的名称。|  
|类型|所有声明和类型的所有用法更改为新名称，包括构造函数和析构函数。 为分部类型重命名操作将会传播到所有部分。|  
  
#### <a name="to-rename-an-identifier"></a>若要重命名标识符  
  
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
  
2. 将光标置于`MethodB`，在方法声明或方法调用。  
  
3. 从**重构**菜单中，选择**重命名**。 **重命名**对话框随即出现。  
  
     此外可以右键单击光标，指向**重构**上下文菜单，然后单击**重命名**以显示**重命名**对话框。  
  
4. 在中**新的名称**字段中，键入`MethodC`。  
  
5. 选择**在注释中的搜索**复选框。  
  
6. 单击 **“确定”**。  
  
7. 在中**预览更改**对话框中，单击**应用**。  
  
#### <a name="to-rename-an-identifier-using-smart-tags"></a>若要重命名标识符使用智能标记  
  
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
  
2. 声明中`MethodB`中，键入或 backspace 方法标识符。 此标识符下将显示智能标记提示。  
  
    > [!NOTE]
    > 仅可以调用重命名重构在标识符声明中使用智能标记。  
  
3. 键入的键盘快捷方式 SHIFT + ALT + F10，，然后按向下箭头以显示智能标记菜单。  
  
     或  
  
     将鼠标指针移动智能标记提示符，以显示智能标记。 然后将鼠标指针移至该智能标记，并单击向下箭头以显示智能标记菜单。  
  
4. 选择**重命名\<identifer1 >' 到 '\<identifier2 >'** 菜单项调用重命名重构而无需更改代码的预览。 对所有引用 **\<identifer1 >** 将自动更新为 **\<identifier2 >**。  
  
     或  
  
     选择**带预览重命名**菜单项调用重命名重构与更改代码的预览。 **预览更改**对话框将出现。  
  
## <a name="remarks"></a>备注  
  
## <a name="renaming-implemented-or-overridden-members"></a>重命名实现或重写的成员  
 当您**重命名**实现/重写或是实现/重写的其他类型中的成员的成员[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]显示一个对话框，说明重命名操作将导致级联更新。 如果单击**继续**、 重构引擎以递归方式查找，并将重命名库中的所有成员和具有的派生的类型实现/替代关系与要重命名的成员。  
  
 下面的代码示例包含具有实现/重写关系的成员。  
  
 [!code-csharp[CsUsingCsIDERefactor#1](../snippets/csharp/VS_Snippets_VBCSharp/CsUsingCsIDERefactor/CS/Class1.cs#1)]  
  
 在上一示例中，重命名`C.Method()`也将重命名`Ibase.Method()`因为`C.Method()`实现`Ibase.Method()`。 接下来，重构引擎以递归方式发现`Ibase.Method()`由实现`Derived.Method()`并将重命名`Derived.Method()`。 重构引擎不会重命名`Base.Method()`，因为`Derived.Method()`不重写`Base.Method()`。 重构引擎将在此处停止除非你有**重命名重载**签入**重命名**对话框。  
  
 如果**重命名重载**处于选中状态，将重命名重构引擎`Derived.Method(int i)`因为它重载`Derived.Method()`，`Base.Method(int i)`因为由重写`Derived.Method(int i)`，和`Base.Method()`的重载，因为它`Base.Method(int i)`.  
  
> [!NOTE]
> 重命名引用的程序集中定义的成员时，对话框中的文字重命名会导致生成错误。  
  
## <a name="renaming-properties-of-anonymous-types"></a>重命名匿名类型的属性  
 当您重命名匿名类型中的属性时，重命名操作将传播到其他具有相同的属性的匿名类型中的属性。 以下示例说明了此行为。  
  
```csharp  
var a = new { ID = 1};  
var b = new { ID = 2};  
```  
  
 在前面的代码中，重命名`ID`将更改`ID`两个语句中因为它们具有相同的基础匿名类型。  
  
```csharp  
var companyIDs =  
    from c in companylist  
    select new { ID = c.ID, Name = c.Name};  
  
var orderIDs =  
    from o in orderlist  
    select new { ID = o.ID, Item = o.Name};  
```  
  
 在前面的代码中，重命名`ID`将仅重命名的一个实例`ID`因为`companyIDs`和`orderIDs`不具有相同的属性。  
  
## <a name="see-also"></a>请参阅  
 [重构 (C#)](../csharp-ide/refactoring-csharp.md)   
 [匿名类型](https://msdn.microsoft.com/library/59c9d7a4-3b0e-475e-b620-0ab86c088e9b)