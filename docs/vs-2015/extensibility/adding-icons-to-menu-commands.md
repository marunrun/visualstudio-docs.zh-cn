---
title: 将图标添加到菜单命令 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- icons [Visual Studio], adding to toolbars
- toolbars [Visual Studio], adding icons to commands
- commands [Visual Studio], adding icons
ms.assetid: 362a0c7e-5729-4297-a83f-1aba1a37fd44
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 940bef878e7360cd3709b6b3403eff2261948e0e
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "58936965"
---
# <a name="adding-icons-to-menu-commands"></a>将图标添加到菜单命令
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

命令可出现在菜单和工具栏。 在工具栏上很常见的命令将使用只是一个图标 （为节省空间） 时菜单上显示命令通常显示带图标和文本。  
  
 图标是 16 像素宽乘 16 像素高和可以是 8 位颜色深度 （256 色） 或 32 位颜色深度 （真彩色）。 首选 32 位颜色图标。 通常在单个位图中的单个水平行中排列图标，尽管允许多个位图。 此位图是以及可用在位图中的单个图标在.vsct 文件中声明的。 请参阅参考[Bitmaps 元素](../extensibility/bitmaps-element.md)的更多详细信息。  
  
## <a name="adding-an-icon-to-a-command"></a>将图标添加到命令  
 以下过程假设你拥有现有 VSPackage 项目与菜单命令。 若要了解如何执行此操作，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。  
  
1.  使用的颜色深度为 32 位创建位图。 图标始终是 16 x 16，因此此位图必须为 16 像素高和宽为 16 像素的倍数。  
  
     每个图标放置在单个行中彼此位图上。 使用 alpha 通道来指示位置中的每个图标的透明度。  
  
     如果使用 8 位颜色深度，使用洋红`RGB(255,0,255)`的透明度。 但是，最好是 32 位颜色图标。  
  
2.  将图标文件复制到你的 VSPackage 项目中的资源目录。 在解决方案资源管理器，将图标添加到项目。 （选择资源，并在上下文菜单上单击添加，然后选择现有项，并选择图标文件。）  
  
3.  在编辑器中打开.vsct 文件。  
  
4.  添加`GuidSymbol`具有的名称元素**testIcon**。 创建 GUID (**工具 / 创建 GUID**，然后选择**注册表格式**并单击复制) 将其粘贴到`value`属性。 结果应如下所示：  
  
    ```xml  
    <!-- Create your own GUID -->  
    <GuidSymbol name="testIcon" value="{00000000-0000-0000-0000-0000}">  
    ```  
  
5.  添加`<IDSymbol>`图标。 `name`属性是图标的 ID 和`value`指示上条带，其位置。 如果只是一个图标，将添加 1。 结果应如下所示：  
  
    ```xml  
    <!-- Create your own GUID -->  
    <GuidSymbol name="testIcon" value="{00000000-0000-0000-0000-0000}">  
        <IDSymbol name="testIcon1" value="1" />  
    </GuidSymbol>  
    ```  
  
6.  创建`<Bitmap>`在`<Bitmaps>`.vsct 文件来表示包含图标的位图的部分。  
  
    -   设置`guid`值的名称与`<GuidSymbol>`在上一步中创建的元素。  
  
    -   设置`href`位图文件的相对路径的值 (在这种情况下**资源\\< 图标文件名\>**。  
  
    -   设置`usedList`IDSymbol 前面创建的值。 此属性指定要在 VSPackage 中使用的图标的以逗号分隔列表。 不在列表的图标是排除窗体编译。  
  
         位图块应如下所示：  
  
        ```xml  
        <Bitmap guid="testIcon" href="Resources\<icon file name>" usedList="testIcon1"/>  
        ```  
  
7.  中的现有`<Button>`元素中，设置`Icon`到前面创建的 GUIDSymbol 和 IDSymbol 值的元素。 下面是使用这些值的 Button 元素示例：  
  
    ```xml  
    <Button guid="guidAddIconCmdSet" id="cmdidMyCommand" priority="0x0100" type="Button">  
        <Parent guid="guidAddIconCmdSet" id="MyMenuGroup" />  
        <Icon guid="testIcon" id="testIcon1" />  
        <Strings>  
            <ButtonText>My Command name</ButtonText>  
        </Strings>  
    </Button>  
    ```  
  
8.  测试您的图标。 生成项目并启动调试。 在实验实例中，找到的命令。 它应显示该图标已添加。  
  
## <a name="see-also"></a>请参阅  
 [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)   
 [VSCT XML 架构参考](../extensibility/vsct-xml-schema-reference.md)
