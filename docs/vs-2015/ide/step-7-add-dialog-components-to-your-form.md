---
title: 步骤 7：向窗体添加对话框组件 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: ea98c55e-6213-4893-ba7b-f19d7f119527
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b58f76dc5137ac0e281f109ee78f3ed43f907400
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72646960"
---
# <a name="step-7-add-dialog-components-to-your-form"></a>步骤 7：向窗体添加对话框组件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

要启用程序以打开图片文件并选择背景色，请在此步骤中，将“OpenFileDialog”组件和“ColorDialog”组件添加到窗体中。

 组件在某些方面与控件相似。 使用工具箱向窗体添加一个组件，然后使用“属性”窗口设置该组件的属性。 但与控件不同，向窗体添加组件不会添加用户可从窗体中查看的可见项。 相反，这将提供可使用代码触发的某些行为。 该组件可打开“打开文件”对话框。

 ![视频链接](../data-tools/media/playvideo.gif "PlayVideo")有关本主题的视频版本，请参阅[教程1：在 Visual Basic 中创建图片查看器-视频 3](http://go.microsoft.com/fwlink/?LinkId=205213)或[教程1：在视频3中C#创建图片查看器](http://go.microsoft.com/fwlink/?LinkId=205202)。 这些视频使用 Visual Studio 的早期版本，因此在一些菜单命令和其他用户界面元素上略有差异。 但是，概念和过程与当前版本的 Visual Studio 大同小异。

### <a name="to-add-dialog-components-to-your-form"></a>向窗体添加对话框组件

1. 选择 Windows 窗体设计器（Form1.cs [设计] 或 Form1.vb [设计]），然后打开工具箱中的“对话框”组。

    > [!NOTE]
    > 工具箱中的“对话框”组具有可用于打开多个有用的对话框的组件，这些对话框可用于打开和保存文件、浏览文件夹以及选择字体和颜色。 在此项目中会使用以下两个对话框组件：“OpenFileDialog”和“ColorDialog”。

2. 要向窗体添加一个名为“openFileDialog1”的组件，请双击“OpenFileDialog”。 要向窗体添加一个名为“colorDialog1”的组件，请双击工具箱中的“ColorDialog”。 （在下一个教程步骤中使用该程序。）你应在 Windows 窗体设计器的底部看到一个区域（位于图片查看器窗体下方），其中包含你添加的两个对话框组件的图标，如下图所示。

     ![对话框组件](../ide/media/express-dialogsadded.png "Express_DialogsAdded")对话框组件

3. 在 Windows 窗体设计器底部区域中选择“openFileDialog1”图标。 设置以下两个属性：

    - 将 Filter 属性设置为以下值（可以复制粘贴以下内容）：

        ```
        JPEG Files (*.jpg)|*.jpg|PNG Files (*.png)|*.png|BMP Files (*.bmp)|*.bmp|All files (*.*)|*.*
        ```

    - 将 Title 属性设置为以下内容：“选择一个图片文件”

         Filter 属性设置指定在“选择图片”文件对话框中显示的文件类型的种类。

    > [!NOTE]
    > 要查看其他应用程序中的“打开文件”对话框的示例，请打开“记事本”或“画图”，然后在菜单栏上选择“文件”、“打开”。 请注意“文件类型”下拉列表是如何在底部出现的。 刚才已使用“OpenFileDialog”组件中的 Filter 属性进行了此设置。 还请注意“属性”窗口中的 Title 和 Filter 属性是如何加粗的。 IDE 执行上述操作是为了显示其默认值已更改的任何属性。

### <a name="to-continue-or-review"></a>继续或查看

- 要转到下一个教程步骤，请参阅[步骤 8：为“显示图片”按钮事件处理程序编写代码](../ide/step-8-write-code-for-the-show-a-picture-button-event-handler.md)。

- 要返回上一个教程步骤，请参阅[步骤 6：命名按钮控件](../ide/step-6-name-your-button-controls.md)。
