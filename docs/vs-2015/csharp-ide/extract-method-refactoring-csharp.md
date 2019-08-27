---
title: 提取方法重构 (C#) |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 5a889250e641e004bdb0d89f6965c43c3d6b8e2a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68155252"
---
# <a name="extract-method-refactoring-c"></a>提取方法重构 (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**提取方法**是重构操作，可轻松地从中的现有成员的代码段创建一个新的方法。  
  
 使用**提取方法**，可以通过提取一组中的现有成员的代码块中的代码创建一个新的方法。 新的提取方法包含所选的代码，并中的现有成员的所选的代码替换为调用新方法。 打开代码片段到其自己的方法，您可以快速并准确地重新组织代码，以便更好地重用和可读性。  
  
 **提取方法**具有以下优点：  
  
- 鼓励通过强调离散、 可重复使用方法的最佳编码实践。  
  
- 鼓励自文档化代码中通过较好的组织。  
  
     具说明性的名称时使用的高级方法可以像读取一系列的注释。  
  
- 鼓励创建精细的方法，以简化重写。  
  
- 可以减少代码重复。  
  
### <a name="to-use-extract-method"></a>若要使用提取方法  
  
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
  
2. 选择你想要提取的代码片段：  
  
    ```csharp  
    double area = PI * radius * radius;  
    ```  
  
3. 上**重构**菜单上，单击**提取方法**。  
  
     **提取方法**对话框随即出现。  
  
     或者，也可以键入键盘快捷键 CTRL + R、 M 显示**提取方法**对话框。  
  
     您还可以右键单击所选代码中，指向**重构**，然后单击**提取方法**以显示**提取方法**对话框。  
  
4. 指定的名称的新方法，如`CircleArea`，请在**新的方法名称**框。  
  
     新的方法签名的预览显示在下**预览方法签名**。  
  
5. 单击 **“确定”** 。  
  
## <a name="remarks"></a>备注  
 当你使用**提取方法**命令时，同一个类中的源成员之后插入新方法。  
  
## <a name="partial-types"></a>分部类型  
 如果此类是分部类型，然后**提取方法**生成紧跟源成员的新方法。 **提取方法**确定新方法，通过新方法中的代码不引用任何实例数据时创建的静态方法的签名。  
  
## <a name="generic-type-parameters"></a>泛型类型参数  
 当您提取具有不受约束的泛型类型参数的方法时，生成的代码将不添加`ref`给该参数的修饰符除非值分配给它。 如果提取的方法将支持引用类型作为泛型类型参数，则应手动添加`ref`到方法签名中的参数修饰符。  
  
## <a name="anonymous-methods"></a>匿名方法  
 如果你尝试提取匿名方法，包括对本地变量声明或匿名方法外部引用的引用的一部分，然后 Visual Studio 会警告您可能有语义更改。  
  
 当匿名方法使用本地变量的值时，是在匿名方法执行时间点获取的值。 当匿名方法提取到另一种方法时，在发生的对提取的方法的调用获取本地变量的值。  
  
 下面的示例说明了这一语义更改。 如果执行此代码，然后**11**将打印到控制台。 如果您使用**提取方法**若要提取的代码注释标记到其自己的方法的代码区域，然后执行重构的代码，然后**10**将打印到控制台。  
  
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
  
 若要解决这种情况下，请在类中的匿名方法字段中使用的本地变量。  
  
## <a name="see-also"></a>请参阅  
 [重构 (C#)](../csharp-ide/refactoring-csharp.md)