---
title: 提取方法重构（C#） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vs.csharp.refactoring.extractmethod
dev_langs:
- CSharp
helpviewer_keywords:
- refactoring [C#], Extract Method
- Extract Method refactoring operation [C#]
ms.assetid: eeba11df-a815-4bec-9c21-8a831891b783
caps.latest.revision: 29
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6e6d5e7913a7433fd4b30da490f33dd614c3e2b2
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667544"
---
# <a name="extract-method-refactoring-c"></a>提取方法重构 (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**提取方法**是一项重构操作，它提供了一种简单的方法，可用于从现有成员的代码片段创建新方法。

 使用**提取方法**，您可以通过从现有成员的代码块内提取选择的代码来创建新方法。 新的、提取的方法包含选定的代码，并通过调用新方法替换现有成员中的选定代码。 将代码片段转换为自己的方法，可以快速准确地重新组织代码，以便更好地重复使用和提高可读性。

 **提取方法**具有以下优点：

- 通过强调离散的、可重用的方法来鼓励最佳编码做法。

- 鼓励通过良好的组织自行记录代码。

     当使用描述性名称时，高级方法可以更像是一系列注释。

- 鼓励创建更细化的方法来简化重写。

- 减少代码重复。

### <a name="to-use-extract-method"></a>使用提取方法

1. 创建名为 `ExtractMethod` 的控制台应用程序，然后将 `Program` 替换为下面的示例代码。

    ```csharp
    class A
    {
        const double PI = 3.141592;

        double CalculatePaintNeeded(double paintPerUnit, double radius)
        {
            // Select any of the following:
            // 1. The entire next line of code.
            // 2. The right-hand side of the next line of code.
            // 3. Just "PI *" of the right-hand side of the next line
            //    of code (to see the prompt for selection expansion).
            // 4.  All code within the method body.
            // ...Then invoke Extract Method.

            double area = PI * radius * radius;

            return area / paintPerUnit;
        }
    }
    ```

2. 选择要提取的代码片段：

    ```csharp
    double area = PI * radius * radius;
    ```

3. 在 "**重构**" 菜单上，单击 "**提取方法**"。

     此时将显示 "**提取方法**" 对话框。

     此外，还可以键入键盘快捷方式 CTRL + R、M 以显示 "**提取方法**" 对话框。

     您还可以右键单击所选代码，指向 "**重构**"，然后单击 "**提取方法**" 以显示 "**提取方法**" 对话框。

4. 在**新方法**的 "名称" 框中指定新方法的名称，如 `CircleArea`。

     "**预览方法签名**" 下会显示新方法签名的预览。

5. 单击“确定”。

## <a name="remarks"></a>备注
 使用 "**提取方法**" 命令时，会在同一类中的源成员后插入新方法。

## <a name="partial-types"></a>分部类型
 如果类是分部类型，则**提取方法**会立即在源成员后生成新的方法。 **提取方法**确定新方法的签名，并在新方法中的代码未引用任何实例数据时创建静态方法。

## <a name="generic-type-parameters"></a>泛型类型参数
 提取具有不受约束的泛型类型参数的方法时，除非为其赋值，否则生成的代码不会将 `ref` 修饰符添加到该参数。 如果提取的方法将支持引用类型作为泛型类型参数，则应将 `ref` 修饰符手动添加到方法签名中的参数。

## <a name="anonymous-methods"></a>匿名方法
 如果尝试提取部分匿名方法，其中包括对在匿名方法之外声明或引用的局部变量的引用，则 Visual Studio 将警告你有关可能的语义更改。

 当匿名方法使用局部变量的值时，将在执行匿名方法时获取值。 将匿名方法提取到其他方法中时，将在调用提取的方法时获取本地变量的值。

 下面的示例阐释了这种语义更改。 如果执行此代码，则将**11**打印到控制台。 如果使用 "**提取方法**" 将代码注释标记的代码区域提取到其自己的方法中，然后执行重构后的代码，则**10**将打印到控制台。

```csharp
class Program
{
    delegate void D();
    D d;
    static void Main(string[] args)
    {
        Program p = new Program();
        int i = 10;
        /*begin extraction*/
            p.d = delegate { Console.WriteLine(i++); };
        /*end extraction*/
        i++;
        p.d();
    }
}
```

 若要解决此问题，请在类的匿名方法字段中使用局部变量。

## <a name="see-also"></a>请参阅
 [重构 (C#)](../csharp-ide/refactoring-csharp.md)