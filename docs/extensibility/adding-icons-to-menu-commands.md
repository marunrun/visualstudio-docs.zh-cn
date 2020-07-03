---
title: 向菜单命令添加图标 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- icons [Visual Studio], adding to toolbars
- toolbars [Visual Studio], adding icons to commands
- commands [Visual Studio], adding icons
ms.assetid: 362a0c7e-5729-4297-a83f-1aba1a37fd44
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c9f038dc43c1705a7cef47eb09a17607c535e307
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903443"
---
# <a name="add-icons-to-menu-commands"></a>向菜单命令添加图标
菜单和工具栏上都可以出现命令。 在工具栏上，通常在菜单上显示命令（以节省空间）命令，命令通常同时出现同时包含图标和文本。

 图标宽度为16像素，高为16像素，可以为8位颜色深度（256色）或32位颜色深度（真彩色）。 32位颜色图标是首选的。 尽管允许使用多个位图，图标通常在单个位图的单个水平行中排列。 此位图是在 *.vsct*文件中声明的，以及位图中可用的各个图标。 有关更多详细信息，请参阅[位图元素](../extensibility/bitmaps-element.md)的参考。

## <a name="add-an-icon-to-a-command"></a>向命令添加图标
 以下过程假定你已有一个具有菜单命令的现有 VSPackage 项目。 若要了解如何执行此操作，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

1. 创建颜色深度为32位的位图。 图标总是 16 x 16，因此，此位图的高度必须为16像素，宽为16像素。

     每个图标都放置在单个行中彼此相邻的位图上。 使用 alpha 通道指示每个图标中的透明度位置。

     如果使用8位颜色深度，请使用洋红色 `RGB(255,0,255)` 作为透明度。 但是，建议采用32位颜色图标。

2. 将图标文件复制到 VSPackage 项目中的*Resources*目录。 在**解决方案资源管理器**中，将图标添加到项目。 （选择 "**资源**"，并在上下文菜单上单击 "**添加**"，然后单击 "**现有项**"，然后选择图标文件。）

3. 在编辑器中打开 *.vsct*文件。

4. 添加 `GuidSymbol` 名称为**testIcon**的元素。 创建 guid （"**工具**"  >  "**创建 guid**"，然后选择 "**注册表格式**" 并单击 "**复制**"）并将其粘贴到属性中 `value` 。 结果应如下所示：

    ```xml
    <!-- Create your own GUID -->
    <GuidSymbol name="testIcon" value="{00000000-0000-0000-0000-0000}">
    ```

5. `<IDSymbol>`为图标添加。 `name`特性是图标的 ID， `value` 指示其在条带上的位置（如果有）。 如果只有一个图标，请添加1。 结果应如下所示：

    ```xml
    <!-- Create your own GUID -->
    <GuidSymbol name="testIcon" value="{00000000-0000-0000-0000-0000}">
        <IDSymbol name="testIcon1" value="1" />
    </GuidSymbol>
    ```

6. `<Bitmap>`在 `<Bitmaps>` *.vsct*文件的节中创建，以表示包含图标的位图。

    - 将 `guid` 值设置为 `<GuidSymbol>` 你在上一步中创建的元素的名称。

    - 将 `href` 值设置为位图文件的相对路径（在本例中为 "**资源" \\<图标 \> 文件名**。

    - 将 `usedList` 值设置为之前创建的 IDSymbol。 此属性指定要在 VSPackage 中使用的图标的逗号分隔列表。 不在列表中的图标被排除在窗体上。

         位图块应如下所示：

        ```xml
        <Bitmap guid="testIcon" href="Resources\<icon file name>" usedList="testIcon1"/>
        ```

7. 在现有 `<Button>` 元素中，将 `Icon` 元素设置为之前创建的 GUIDSymbol 和 IDSymbol 值。 下面是包含这些值的 Button 元素示例：

    ```xml
    <Button guid="guidAddIconCmdSet" id="cmdidMyCommand" priority="0x0100" type="Button">
        <Parent guid="guidAddIconCmdSet" id="MyMenuGroup" />
        <Icon guid="testIcon" id="testIcon1" />
        <Strings>
            <ButtonText>My Command name</ButtonText>
        </Strings>
    </Button>
    ```

8. 测试图标。 生成项目并启动调试。 在实验实例中，找到命令。 它应显示你添加的图标。

## <a name="see-also"></a>另请参阅
- [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)
- [.VSCT XML 架构引用](../extensibility/vsct-xml-schema-reference.md)
