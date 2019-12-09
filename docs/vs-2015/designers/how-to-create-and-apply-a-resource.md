---
title: 如何创建和应用资源 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
f1_keywords:
- VS.XamlDesigner.CreateResource
- VS.XamlDesigner.EditResource
ms.assetid: 3ff4006d-659d-4073-9a41-06ff85e6cfdf
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ab048fe69ca89086e9811e5277dccb86aeee6194
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300864"
---
# <a name="how-to-create-and-apply-a-resource"></a>如何创建和应用资源
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

XAML 设计器中元素的样式和模板存储在称作资源的可重用实体中。 样式可设置元素属性并重用这些设置以便多个元素实现一致的外观。 [ControlTemplate](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.controltemplate.aspx) 定义控件的外观，并且可作为资源应用。 有关详细信息，请参阅[快速入门：设置控件的样式](https://go.microsoft.com/fwlink/?LinkID=248239)和[快速入门：控件模板](https://go.microsoft.com/fwlink/?LinkID=247982)。

 每当从现有属性、[样式](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.style.aspx)或 `ControlTemplate` 创建新资源时，可在“创建资源”对话框中将资源定义为应用程序级别、文档级别或元素级别。 这些级别决定了可使用资源的位置。 例如，如果定义元素级别的资源，则该资源只能应用于在其上创建资源的元素。 还可以选择将资源存储在资源字典中，资源字典是可在另一个项目中再次使用的单独文件。

### <a name="to-create-a-new-resource"></a>创建新资源的步骤

1. 在 XAML 设计器中打开一个 XAML 文件后，创建一个元素，或在“文档大纲”窗口中选择一个元素。

2. 在“属性”窗口中，选择属性标记，该标记显示为属性值右侧的一个方框符号，然后选择“转换为新资源”。 白色方框符号指示默认值，而黑色方框符号通常指示已应用了某个本地资源

     将出现用于创建资源的相应对话框。 当从画笔创建资源时，就会出现此对话框：

     !["创建资源" 对话框](../designers/media/xaml-create-resource.png "xaml_create_resource")

3. 在“名称(关键字)”框中，输入关键字名称。 这是当希望其他元素可以引用该资源时，可以使用的名称。

4. 在“定义位置”下，选择指定想要在其中定义资源的位置的选项：

    - 若要使该资源对应用程序中的任何文档可用，则选择“应用程序”。

    - 若要使该资源仅对当前文档可用，则选择“此文档”。

    - 若要使该资源仅对从中创建了该资源的元素或其子元素可用，则选择“此文档”，然后在下拉列表中，选择 *element*: *name*。

    - 若要在可在其他项目中重用的资源字典文件中定义该资源，则单击“资源字典”，然后在下拉列表中选择一个现有的资源字典文件，如“StandardStyles.xaml”。

5. 选择“确定”按钮以创建资源并将其应用于从其中创建了该资源的元素。

### <a name="to-apply-a-resource-to-an-element-or-property"></a>将资源应用于某个元素或属性的步骤

1. 在“文档大纲”窗口中，选择想要向其应用资源的元素。

2. 执行下列操作之一：

   - 将资源应用于属性。 在“属性”窗口中，选择属性值旁边的属性标记，再选择“本地资源”或“系统资源”，然后从显示的列表中选择可用的资源。

      如果看不到希望看到的资源，可能是因为该资源的类型与属性的类型不匹配。

   - 将样式或控件模板资源应用于控件。 在“文档大纲”窗口中打开某个控件的上下文菜单，选择“编辑模板”或“编辑其他模板”，选择“应用资源”，然后从显示的列表中选择控件模板的名称。

     > [!NOTE]
     > “编辑模板”用于应用控件模板。 “编辑其他模板”用于应用其他模板类型。

     资源可应用于兼容的任何位置。 例如，画笔资源可应用于  **控件的“前景”** <xref:Windows.UI.Xaml.Controls.TextBox>属性。

### <a name="to-edit-a-resource"></a>编辑资源的步骤

1. 选择美工板上或“文档大纲”窗口中的某个元素。

2. 在“属性”窗口中，选择属性右侧的“默认”或“本地”属性标记，然后选择“编辑资源”，以打开“编辑资源”对话框。

3. 修改该资源的选项。

## <a name="see-also"></a>请参阅
 [使用 XAML 设计器创建 UI](../designers/creating-a-ui-by-using-xaml-designer-in-visual-studio.md)
