---
title: 步骤 7：向窗体添加对话框组件
ms.date: 08/30/2019
ms.assetid: ea98c55e-6213-4893-ba7b-f19d7f119527
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a9697bf6cf84c2a74daac2017b4f63d52a7019b6
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/25/2020
ms.locfileid: "77579275"
---
# <a name="step-7-add-dialog-components-to-your-form"></a>步骤 7：向窗体添加对话框组件

要启用应用以打开图片文件并选择背景色，请在此步骤中，将 <xref:System.Windows.Forms.OpenFileDialog> 组件和 <xref:System.Windows.Forms.ColorDialog> 组件添加到窗体中。

组件在某些方面与控件相似。 使用“工具箱”  向窗体添加一个组件，然后使用“属性”  窗口设置该组件的属性。 但与控件不同，向窗体添加组件不会添加用户可从窗体中查看的可见项。 相反，这将提供可使用代码触发的某些行为。 该组件可打开“打开文件”对话框  。

## <a name="to-add-dialog-components-to-your-form"></a>向窗体添加对话框组件

1. 选择“Windows 窗体设计器”（“Form1.cs [设计]”），然后打开“工具箱”中的“对话框”组     。

    > [!NOTE]
    > “工具箱”  中的“对话框”  组具有可用于打开多个有用的对话框的组件，这些对话框可用于打开和保存文件、浏览文件夹以及选择字体和颜色。 在此项目中使用两个对话框组件：OpenFileDialog 和 ColorDialog。

1. 要向窗体添加一个名为“openFileDialog1”的组件，请双击“OpenFileDialog”   。 要向窗体添加一个名为“colorDialog1”  的组件，请双击“工具箱”  中的“ColorDialog”  。 （将在下一个教程步骤中使用后一个组件。）“Windows 窗体设计器”的底部（在“图片查看器”窗体下方）会出现一个区域，其中包含与已添加的两个对话框组件对应的图标，如下图所示   。

     ![对话框组件](../ide/media/express_dialogsadded.png)<br>对话框组件 

1. 在“Windows 窗体设计器”  底部区域中选择“openFileDialog1”  图标。 设置以下两个属性：

    - 将 Filter 属性设置为以下值（可以复制粘贴以下内容）  ：

        ```
        JPEG Files (*.jpg)|*.jpg|PNG Files (*.png)|*.png|BMP Files (*.bmp)|*.bmp|All files (*.*)|*.*
        ```

    - 将“Title”属性设置为以下内容  ：**选择一个图片文件**

         Filter 属性设置指定在“选择图片”文件对话框中显示的文件类型的种类   。

    > [!TIP]
    > 要查看其他应用程序中的“打开文件”  对话框的示例，请打开“记事本”  或“画图”  ，然后在菜单栏上选择“文件”   > “打开”  。 请注意，文件名旁有一个下拉列表，你可以在其中选择文件类型。 <br/><br/>你刚才已使用“OpenFileDialog”组件中的“筛选器”属性在应用中进行了此设置   。 还请注意“属性”窗口中的 Title 和 Filter 属性是如何加粗的    。 IDE 执行上述操作是为了显示其默认值已更改的任何属性。

## <a name="next-steps"></a>后续步骤

* 要转到下一个教程步骤，请参阅[步骤 8：  为“显示图片”按钮事件处理程序编写代码](../ide/step-8-write-code-for-the-show-a-picture-button-event-handler.md)。

* 要返回上一个教程步骤，请参阅[步骤 6：命名按钮控件](../ide/step-6-name-your-button-controls.md)。

## <a name="see-also"></a>请参阅

* [教程 2：创建计时数学测验](tutorial-2-create-a-timed-math-quiz.md)
* [教程 3：创建匹配游戏](tutorial-3-create-a-matching-game.md)
