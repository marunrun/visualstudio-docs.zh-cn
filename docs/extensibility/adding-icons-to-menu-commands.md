---
title: 向菜单命令添加图标 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: f4b71f981472451766f526cf62e975e571cf46da
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740154"
---
# <a name="add-icons-to-menu-commands"></a>向菜单命令添加图标
命令可以同时出现在菜单和工具栏上。 在工具栏上，通常只显示一个图标（以节省空间）的命令，而在菜单上，命令通常同时显示一个图标和文本。

 图标宽 16 像素 x 16 像素高，可以是 8 位颜色深度（256 种颜色）或 32 位颜色深度（真色）。 32 位颜色图标优先。 图标通常排列在单个位图中的单个水平行中，尽管允许多个位图。 此位图在 *.vsct*文件中声明，以及位图中可用的单个图标。 有关详细信息，请参阅[Bitmap 元素](../extensibility/bitmaps-element.md)的引用。

## <a name="add-an-icon-to-a-command"></a>向命令添加图标
 以下过程假定您具有具有菜单命令的现有 VSPackage 项目。 要了解如何执行此操作，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

1. 创建颜色深度为 32 位的位图。 图标始终为 16 x 16，因此此位图必须高 16 像素，并且倍数为 16 像素宽。

     每个图标都放在一行的位图上。 使用 alpha 通道指示每个图标中的透明度位置。

     如果使用 8 位颜色深度，请使用品红色`RGB(255,0,255)`作为透明度。 但是，32 位颜色图标是首选。

2. 将图标文件复制到 VSPackage 项目中的 *"资源"* 目录。 在**解决方案资源管理器**中，将图标添加到项目中。 （选择 **"资源**"，并在上下文菜单上单击"**添加**"，然后"**添加现有项目**"，然后选择图标文件。

3. 打开编辑器中的 *.vsct*文件。

4. 添加名称`GuidSymbol`为**testIcon**的元素。 创建 GUID（**工具** > **创建 GUID**，然后选择**注册表格式**，然后单击 **"复制**"），并将其粘贴`value`到属性中。 结果应如下所示：

    ```xml
    <!-- Create your own GUID -->
    <GuidSymbol name="testIcon" value="{00000000-0000-0000-0000-0000}">
    ```

5. 为图标`<IDSymbol>`添加 a。 属性`name`是图标的 ID，指示`value`其在条带上的位置（如果有）。 如果只有一个图标，则添加 1。 结果应如下所示：

    ```xml
    <!-- Create your own GUID -->
    <GuidSymbol name="testIcon" value="{00000000-0000-0000-0000-0000}">
        <IDSymbol name="testIcon1" value="1" />
    </GuidSymbol>
    ```

6. 在`<Bitmap>``<Bitmaps>`*.vsct*文件部分中创建 一个，以表示包含图标的位图。

    - 将`guid`值设置为在上一步骤中`<GuidSymbol>`创建的元素的名称。

    - 将`href`值设置为位图文件的相对路径（在本例中 **，资源\\<\>图标文件名**。

    - 将`usedList`该值设置为您之前创建的 IDSymbol。 此属性指定要在 VSPackage 中使用的图标的逗号分隔列表。 列表中未显示的图标将排除表单编译。

         位图块应如下所示：

        ```xml
        <Bitmap guid="testIcon" href="Resources\<icon file name>" usedList="testIcon1"/>
        ```

7. 在现有`<Button>`元素中，将`Icon`元素设置为您之前创建的 GUIDSymbol 和 IDSymbol 值。 下面是具有这些值的 Button 元素的示例：

    ```xml
    <Button guid="guidAddIconCmdSet" id="cmdidMyCommand" priority="0x0100" type="Button">
        <Parent guid="guidAddIconCmdSet" id="MyMenuGroup" />
        <Icon guid="testIcon" id="testIcon1" />
        <Strings>
            <ButtonText>My Command name</ButtonText>
        </Strings>
    </Button>
    ```

8. 测试图标。 生成项目并启动调试。 在实验实例中，找到命令。 它应显示您添加的图标。

## <a name="see-also"></a>请参阅
- [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)
- [VSCT XML 架构引用](../extensibility/vsct-xml-schema-reference.md)
