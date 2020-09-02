---
title: " (c # ) 封装字段重构 |Microsoft Docs"
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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 0b4f5ddbe7eab925b06584f00b04bed3c74e9811
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667574"
---
# <a name="encapsulate-field-refactoring-c"></a>封装字段重构 (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

" **封装字段** " 重构操作使您能够快速从现有字段创建属性，然后使用对新属性的引用无缝更新您的代码。

 当某个 [字段](https://msdn.microsoft.com/library/3cbb2f61-75f8-4cce-b4ef-f5d1b3de0db7) 为 [公共](https://msdn.microsoft.com/library/0ae45d16-a551-4b74-9845-57208de1328e)字段时，其他对象可以直接访问该字段，并且可以对其进行修改，该字段由拥有该字段的对象检测。 通过使用 [属性](https://msdn.microsoft.com/library/e295a8a2-b357-4ee7-a12e-385a44146fa8) 封装字段，你可以禁止直接访问字段。

 若要创建新属性，" **封装字段** " 操作将更改要封装为 [私有](https://msdn.microsoft.com/library/654c0bb8-e6ac-4086-bf96-7474fa6aa1c8)字段的访问修饰符，然后为该字段生成 [get](https://msdn.microsoft.com/library/a52de048-fbe0-41b0-82ec-8e4ac04d3a71) 和 [set](https://msdn.microsoft.com/library/30d7e4e5-cc2e-4635-a597-14a724879619) 访问器。 在某些情况下，仅生成 `get` 访问器（如当字段声明为只读时）。

 重构引擎将在 "**封装字段**" 对话框的 "**更新引用**" 部分中指定的区域中，用对新属性的引用更新您的代码。

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

2. 在 [代码编辑器](../ide/writing-code-in-the-code-and-text-editor.md)中，将光标放在声明中要封装的字段的名称上。 在下面的示例中，将光标置于单词 `width` 上：

    ```csharp
    public int width, height;
    ```

3. 在 " **重构** " 菜单上，单击 " **封装字段**"。

     此时将显示 " **封装字段** " 对话框。

     还可以键入键盘快捷方式 CTRL + R、E 以显示 " **封装字段** " 对话框。

     您还可以右键单击光标，指向 " **重构**"，然后单击 " **封装字段** " 以显示 " **封装字段** " 对话框。

4. 指定设置。

5. 按 ENTER，或单击 **"确定"** 按钮。

6. 如果选择了 " **预览引用更改** " 选项，则 " **预览引用更改** " 窗口随即打开。 单击“应用”按钮。

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
 仅当游标与字段声明位于同一行时，才可以进行 " **封装字段** " 操作。

 对于声明多个字段的声明，" **封装字段** " 使用逗号作为字段之间的边界，并在与光标最接近的行和行上启动重构。 还可以通过在声明中选择字段的名称来指定想要封装的字段。

 通过此重构操作生成的代码将由封装字段代码片段功能来建模。 代码片段是可修改的。 有关详细信息，请参阅[代码片段](../ide/code-snippets.md)。

## <a name="see-also"></a>另请参阅
 ) [Visual c # 代码段](../ide/visual-csharp-code-snippets.md)[重构 (c #](../csharp-ide/refactoring-csharp.md)