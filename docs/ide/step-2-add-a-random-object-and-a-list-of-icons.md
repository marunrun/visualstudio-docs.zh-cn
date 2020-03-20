---
title: 步骤 2：添加 Random 对象和图标列表
ms.date: 11/04/2016
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.assetid: 95faea28-eddc-4cfa-95fb-3b34b5a976d7
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1f4731778ebb3acbdc3bb7d9b5827c1015541d98
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "77579421"
---
# <a name="step-2-add-a-random-object-and-a-list-of-icons"></a>步骤 2：添加 Random 对象和图标列表

在本步骤中，你要为游戏创建一组匹配的符号。 每个符号将添加到窗体上 TableLayoutPanel 中的两个随机单元格。 为此，请使用两个 `new` 语句创建两个对象。 第一个是 <xref:System.Random> 对象，类似于数学测验游戏中使用的对象。 此代码中使用它来随机选择 TableLayoutPanel 中的单元格。 第二个对象是用于存储随机选择的符号的 <xref:System.Collections.Generic.List%601> 对象，你可能没有见过。

## <a name="to-add-a-random-object-and-a-list-of-icons"></a>添加 random 对象和图标列表

1. 在“解决方案资源管理器”  中，选择“Form1.cs”  （如果使用 C#）或“Form1.vb”  （如果使用 Visual Basic），然后在菜单栏上选择“查看”   > “代码”  。 也可以按 F7 键或在“解决方案资源管理器”中双击“Form1”    。

     这会显示 Form1 的后台代码模块。

2. 在现有代码中，添加以下代码。

     [!code-csharp[VbExpressTutorial4Step2_3_4#1](../ide/codesnippet/CSharp/step-2-add-a-random-object-and-a-list-of-icons_1.cs)]
     [!code-vb[VbExpressTutorial4Step2_3_4#1](../ide/codesnippet/VisualBasic/step-2-add-a-random-object-and-a-list-of-icons_1.vb)]

      > [!IMPORTANT]
      > 使用此页右上角的编程语言控件查看 C# 代码片段或 Visual Basic 代码片段。<br><br>![Docs.Microsoft.com 的编程语言控件](../ide/media/docs-programming-language-control.png)

      如果你使用 C#，请确保将代码放在左大括号后面，紧靠类声明 (`public partial class Form1 : Form`) 之后。 如果你使用 Visual Basic，请将代码放在紧靠类声明 (`Public Class Form1`) 之后。

3. 添加 List 对象时，请注意打开的“IntelliSense”  窗口。 下面是一个 C# 示例，但在 Visual Basic 中添加列表时会显示类似文本。

     ![显示 Click 事件的“属性”窗口](../ide/media/express_listintellisense.png)<br/>***IntelliSense** 窗口*

    > [!NOTE]
    > IntelliSense 窗口仅在手动输入代码时显示。 如果你复制和粘贴代码，则不显示。

     如果你分小段查看代码（和备注），理解起来会更容易。 你的程序可以使用 list 对象跟踪多个不同类型的项目。 列表可以包含数字、true/false 值、文本或其他对象。 你甚至可以有一个包含其他 list 对象的 list 对象。 列表中的项目称为“元素”，每个列表只包含一种元素。 所以数字列表只包含数字，你不能向该列表中添加文本。 同样，你也不能向 true/false 值列表中添加数字。

     当使用 `List` 语句创建 `new` 对象时，你需要指定要在其中存储的数据类型。 因此，“IntelliSense”窗口顶部的工具提示会显示列表中的元素类型  。 同样，这也是 `List<string>`（C# 中）和 `List(Of String)`（Visual Basic 中）的含义：它是包含 `string` 数据类型的元素的 `List` 对象。 程序使用字符串来存储文本，该文本是“IntelliSense”窗口右侧的工具提示将告诉你的文本  。

4. 请考虑为什么在 Visual Basic 中必须首先创建临时数组，但在 C# 中可以使用一条语句创建列表。 这是因为 C# 语言具有“集合初始值设定项”，从而准备了可以接受值的列表  。 在 Visual Basic 中，你可以使用集合初始值设定项。 但是，为了与以前版本的 Visual Basic 兼容，我们建议您使用上面的代码。

     当你将集合初始值设定项与 `new` 语句一同使用时，在创建新的 list 对象后，程序将使用你在大括号内提供的数据填充它。 在本例中，会获取名为“图标”的字符串列表，该列表会初始化以包含十六个字符串。 其中每个字符串都是单个字母，它们都对应于将在标签中出现的图标。 因此，该游戏将包含一对感叹号、一对大写的 N 字母、一对逗号等。 （这些字符设置为 Webdings 字体时，将显示为符号，例如公交车、自行车、蜘蛛等。）list 对象将总共包含十六个字符串，每个字符串对应于 TableLayoutPanel 面板中的一个单元格。

    > [!NOTE]
    > 在 Visual Basic 中，可以获得相同的结果，但是字符串首先放入临时数组中，该数组然后转换为 list 对象。 数组类似于列表，但也有不同之处，例如数组在创建时具有固定大小。 列表可以根据需要收缩或增长，这在此程序中非常重要。

## <a name="to-continue-or-review"></a>继续或查看

- 要转到下一个教程步骤，请参阅[**步骤 3：向每个标签分配一个随机图标**](../ide/step-3-assign-a-random-icon-to-each-label.md)。

- 若要返回上一个教程步骤，请参阅[步骤 1：创建项目并向窗体添加表](../ide/step-1-create-a-project-and-add-a-table-to-your-form.md)。
