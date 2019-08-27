---
title: 封装字段重构 (C#) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vs.csharp.refactoring.encapsulatefield
dev_langs:
- CSharp
helpviewer_keywords:
- Encapsulate Field refactoring operation [C#]
- refactoring [C#], Encapsulate Field
ms.assetid: bf714a04-ab1e-49ce-99ce-dda1ebb1a17f
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 0e2ad3b2d89db83d3b9fa38438abdbde61e72bfe
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65681390"
---
# <a name="encapsulate-field-refactoring-c"></a>封装字段重构 (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**封装字段**重构操作，可从现有字段，快速创建一个属性，然后对新属性的引用无缝地更新你的代码。  
  
 当[字段](https://msdn.microsoft.com/library/3cbb2f61-75f8-4cce-b4ef-f5d1b3de0db7)是[公共](https://msdn.microsoft.com/library/0ae45d16-a551-4b74-9845-57208de1328e)，其他对象可以直接访问该字段，并可以修改它未检测到拥有该字段的对象。 通过使用[属性](https://msdn.microsoft.com/library/e295a8a2-b357-4ee7-a12e-385a44146fa8)要封装这个字段，可以禁止对字段的直接访问。  
  
 若要创建新的属性，**封装字段**操作将会更改想要封装到的字段的访问修饰符[专用](https://msdn.microsoft.com/library/654c0bb8-e6ac-4086-bf96-7474fa6aa1c8)，然后生成[获取](https://msdn.microsoft.com/library/a52de048-fbe0-41b0-82ec-8e4ac04d3a71)并[设置](https://msdn.microsoft.com/library/30d7e4e5-cc2e-4635-a597-14a724879619)该字段的访问器。 在某些情况下，仅生成 `get` 访问器（如当字段声明为只读时）。  
  
 重构引擎对中指定的区域中的新属性的引用更新你的代码**更新引用**一部分**封装字段**对话框。  
  
### <a name="to-create-a-property-from-a-field"></a>从字段创建属性  
  
1. 创建名为 `EncapsulateFieldExample` 的控制台应用程序，然后将 `Program` 替换为下面的示例代码。  
  
    ```csharp  
    class Square  
    {  
        // Select the word 'width' and then use Encapsulate Field.  
        public int width, height;  
    }  
    class MainClass  
    {  
        public static void Main()  
        {  
            Square mySquare = new Square();  
            mySquare.width = 110;  
            mySquare.height = 150;  
            // Output values for width and height.  
            Console.WriteLine("width = {0}", mySquare.width);  
            Console.WriteLine("height = {0}", mySquare.height);  
        }  
    }  
    ```  
  
2. 在中[代码编辑器](../ide/writing-code-in-the-code-and-text-editor.md)，将光标放在声明中，你想要封装的字段的名称。 在下面的示例中，将光标置于单词 `width` 上：  
  
    ```csharp  
    public int width, height;  
    ```  
  
3. 上**重构**菜单上，单击**封装字段**。  
  
     **封装字段**对话框随即出现。  
  
     此外可以键入键盘快捷键 CTRL + R、 E 来显示**封装字段**对话框。  
  
     此外可以右键单击光标，指向**重构**，然后单击**封装字段**以显示**封装字段**对话框。  
  
4. 指定设置。  
  
5. 按 ENTER，或单击**确定**按钮。  
  
6. 如果所选**预览引用更改**选项，则**预览引用更改**窗口随即打开。 单击**应用**按钮。  
  
     源文件中会显示以下 `get` 和 `set` 访问器代码：  
  
    ```csharp  
    public int Width  
    {  
        get { return width; }  
        set { width = value; }  
    }  
    ```  
  
     `Main` 方法中的代码也将更新为新的 `Width` 属性名称。  
  
    ```csharp  
    Square mySquare = new Square();  
    mySquare.Width = 110;  
    mySquare.height = 150;  
    // Output values for width and height.  
    Console.WriteLine("width = {0}", mySquare.Width);  
    ```  
  
## <a name="remarks"></a>备注  
 **封装字段**操作时，才可以将光标置于字段声明的同一行。  
  
 对于声明多个字段的声明**封装字段**使用逗号作为字段之间的边界，并启动重构和光标所在的同一行上最近的游标的字段。 还可以通过在声明中选择字段的名称来指定想要封装的字段。  
  
 通过此重构操作生成的代码将由封装字段代码片段功能来建模。 代码片段是可修改的。 有关详细信息，请参阅[代码片段](../ide/code-snippets.md)。  
  
## <a name="see-also"></a>请参阅  
 [重构 (C#)](../csharp-ide/refactoring-csharp.md)   
 [Visual C# 代码片段](../ide/visual-csharp-code-snippets.md)