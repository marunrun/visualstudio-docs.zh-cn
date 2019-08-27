---
title: 如何：自定义菜单和工具栏
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.renametoolbar
- vs.customize.toolbars
- vs.buttoneditor
- vs.customize.commands
- vs.newtoolbar
helpviewer_keywords:
- captions, customizing toolbar
- custom toolbars [Visual Studio]
- command buttons, customizing toolbar
- labels, customizing toolbar
- images [Visual Studio], toolbar buttons
- buttons [Visual Studio], custom toolbars
- toolbars [Visual Studio], creating in the IDE
- icons [Visual Studio], customizing toolbar
- commands [Visual Studio], customizing environment
- customizing toolbars
- toolbars [Visual Studio], customizing
- toolbars [Visual Studio], customizing in the IDE
ms.assetid: b570ae2f-5302-45dc-9cc9-8d4d1ad50603
caps.latest.revision: 31
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 91223021ce6f05b91d47e7b7019fb0c5c02243db
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63416788"
---
# <a name="how-to-customize-menus-and-toolbars-in-visual-studio"></a>如何：在 Visual Studio 中自定义菜单和工具栏
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在自定义 Visual Studio 时，你不仅可以添加和移除工具栏及菜单栏上的菜单，而且还可以添加和移除与任何给定工具栏或菜单有关的命令。

> [!WARNING]
> 自定义工具栏或菜单后，请确保在“自定义”对话框中继续选中其复选框。 否则，在关闭并重新打开 Visual Studio 之后，你所做的更改将不会保留。

 **本主题内容：**

- [添加、移除或移动菜单栏上的菜单](../ide/how-to-customize-menus-and-toolbars-in-visual-studio.md#bkmk_addmenu)

- [添加、移除或移动工具栏](../ide/how-to-customize-menus-and-toolbars-in-visual-studio.md#bkmk_addtoolbar)

- [自定义菜单或工具栏](../ide/how-to-customize-menus-and-toolbars-in-visual-studio.md#bkmk_customize)

- [重置菜单或工具栏](../ide/how-to-customize-menus-and-toolbars-in-visual-studio.md#bkmk_reset)

## <a name="bkmk_addmenu"></a>添加、移除或移动菜单栏上的菜单

1. 在菜单栏上，依次选择“工具”、“自定义”。

     此时将打开“自定义”对话框。

2. 在“命令”选项卡上，继续选中“菜单栏”选项按钮，继续在该选项旁的列表中选中“菜单栏”，然后执行下列一组步骤：

    - 若要添加菜单，请选择“添加新菜单”按钮，选择“修改所选内容”按钮，然后命名要添加的菜单。

         ![显示如何添加菜单的“自定义”对话框](../ide/media/addmenu.png "AddMenu")

    - 若要删除菜单，请在“控件”列表中选择该菜单，然后选择“删除”按钮。

    - 若要移动菜单栏内的菜单，请在“控件”列表中选择该菜单，然后选择“上移”或“下移”按钮。

## <a name="bkmk_addtoolbar"></a>添加、删除或移动工具栏

1. 在菜单栏上，依次选择“工具”、“自定义”。

     此时将打开“自定义”对话框。

2. 在“工具栏”选项卡上，执行下面一组步骤：

    - 若要添加工具栏，请选择“新建”按钮，指定要添加的工具栏的名称，然后选择“确定”按钮。

         ![显示如何添加工具栏的“自定义”对话框](../ide/media/addtoolbar.png "AddToolbar")

    - 若要删除自定义工具栏，请在“工具栏”列表中选择该工具栏，然后选择“删除”按钮。

        > [!IMPORTANT]
        > 你可以删除自己创建的工具栏，但无法删除默认的工具栏。

    - 若要将工具栏移动到其他停靠位置，请在“工具栏”列表中选择该工具栏，选择“修改所选内容”按钮，然后在随后显示的列表中选择一个位置。

         你也可以拖动工具栏的左边缘，将其移动到主停靠区域内的任何位置。

        > [!NOTE]
        > 有关如何改进工具栏的可用性和辅助功能的详细信息，请参阅[如何：设置 IDE 辅助功能选项](../ide/reference/how-to-set-ide-accessibility-options.md)。

## <a name="bkmk_customize"></a>自定义菜单或工具栏

1. 在菜单栏上，依次选择“工具”、“自定义”。

     此时将打开“自定义”对话框。

2. 在“命令”选项卡上，选择要自定义的元素类型的选项按钮。

3. 在该类型元素的列表中，选择要自定义的菜单或工具栏，然后执行下面一组步骤：

    - 若要添加命令，请选择“添加命令”按钮。

         在“添加命令”对话框中，依次选择“类别”列表中的项和“命令”列表中的项，然后选择“确定”按钮。

         ![Visual Studio 中的“添加命令”对话框](../ide/media/addcommand.png "AddCommand")

    - 若要删除命令，请在“控件”列表中选择该命令，然后选择“删除”按钮。

    - 若要重新排序命令，请在“控件”列表中选择一个命令，然后选择“上移”或“下移”按钮。

    - 若要将命令分组，请在“控件”列表中选择一个命令，选择“修改所选内容”按钮，然后在显示的菜单中选择“开始一组”。

## <a name="bkmk_reset"></a>重置菜单或工具栏

1. 在菜单栏上，依次选择“工具”、“自定义”。

     此时将打开“自定义”对话框。

2. 在“命令”选项卡上，选择要重置的元素类型的选项按钮。

3. 在该元素类型的列表中，选择要重置的菜单或工具栏。

4. 选择“修改所选内容”按钮，然后在显示的菜单中选择“重置”。

     还可以选择“全部重置”按钮，从而重置所有菜单和工具栏。
