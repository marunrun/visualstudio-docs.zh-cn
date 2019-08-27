---
title: Office 项目中的辅助功能
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, accessibility
- shortcut keys [Office development in Visual Studio]
- Ribbon [Office development in Visual Studio], shortcut keys
- accessibility [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a54c9d5322b35092d635edd00e3b200ee67997a9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62945214"
---
# <a name="accessibility-in-office-projects"></a>Office 项目中的辅助功能

Microsoft Visual Studio 和 Microsoft Office 包含许多辅助功能，使你能够构建符合标准的可访问性要求的自定义解决方案。 Microsoft 发布了有关在 Web 上找到的可访问性准则。 有关详细信息，请参阅[辅助功能网站](http://go.microsoft.com/fwlink/?LinkID=37113)。

在大多数情况下，Visual Studio 中的 Office 项目满足辅助功能标准或公开属性，可设置为使可访问你的解决方案。 但是，有一些功能的访问受到限制。

[!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="accessibility-at-design-time"></a>在设计时可访问性

### <a name="use-shortcut-keys-in-document-level-projects"></a>在文档级项目中使用键盘快捷方式
 在 Visual Studio 中打开 Microsoft Office Word 文档或 Microsoft Office Excel 工作簿时，一次只有一个应用程序接收的快捷键命令。 默认情况下，Visual Studio 接收所有快捷方式命令，但您可以使 Word 或 Excel 文档通过选择具有焦点时接收它们**动态键盘方案**上**键盘设置**页**选项**对话框。 有关详细信息，请参阅[Microsoft Office Word 键盘、 Microsoft Office 键盘设置选项对话框](../vsto/microsoft-office-word-keyboard-microsoft-office-keyboard-settings-options-dialog-box.md)和[Microsoft Office Excel 键盘、 Microsoft Office 键盘设置选项对话框](../vsto/microsoft-office-excel-keyboard-microsoft-office-keyboard-settings-options-dialog-box.md).

### <a name="display-shortcut-keys-for-the-ribbon-in-document-level-projects"></a>在文档级项目中的功能区显示键盘快捷方式
 在 Visual Studio 中打开 Word 文档或 Excel 工作簿时，不能按**Alt**键可查看选项卡控件和功能区上的控件的键盘快捷方式。 若要在设计器中打开文档或工作簿时，请查看键盘快捷方式，请执行以下步骤。

#### <a name="to-view-shortcut-keys-for-ribbon-tabs-and-controls-in-the-designer"></a>若要在设计器中查看有关功能区选项卡和控件的键盘快捷方式

1. 在 Visual Studio 中，在**工具**菜单上，单击**选项**。

2. 展开**Office 工具**节点，然后选择**Microsoft Office Excel 键盘**或**Microsoft Office Word 键盘**根据。

3. 选择**动态键盘方案**。

     将出现一条表明必须重新启动 Visual Studio 的更改才会生效。

4. 单击 **“确定”**。

5. 重新启动 Visual Studio 中，并重新打开你的项目。

6. 打开你的项目的文档或工作簿设计器。

7. 按**F6**为功能区显示键盘快捷方式。

## <a name="accessibility-at-runtime"></a>在运行时可访问性

### <a name="windows-forms-controls-on-office-documents"></a>Office 文档上的 Windows 窗体控件
 Windows 窗体控件公开可访问性属性来提供有关控件的辅助功能，如屏幕读取器的信息。 控件对文档级自定义项中的 Office 文档时，可以充分利用这些辅助功能属性。 有关详细信息，请参阅[提供 Windows 窗体上控件的辅助功能信息](/dotnet/framework/winforms/controls/providing-accessibility-information-for-controls-on-a-windows-form)。

 但是，有一些可访问性限制在运行时在 Excel 工作簿或 Word 文档上托管 Windows 窗体控件时：

- 不能为另一控件选项卡。

- 文档上的控件被禁用时为 100%以外的任何更改文档的缩放设置。

  有关限制的文档上的 Windows 窗体控件的信息，请参阅[限制的 Windows 窗体控件上的 Office 文档](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)。

### <a name="actions-panes-and-custom-task-panes"></a>操作窗格和自定义任务窗格
 当操作窗格或自定义任务窗格具有焦点时，你访问控件相同的方式来访问 Windows 窗体应用程序上的控件。 若要将光标移动操作窗格和文档之间，可以按**F6**。

 有关操作窗格和自定义任务窗格的详细信息，请参阅[操作窗格概述](../vsto/actions-pane-overview.md)并[自定义任务窗格](../vsto/custom-task-panes.md)。

### <a name="display-modes"></a>显示模式

Visual Studio 具有以下限制与相关显示模式：

- 文档的缩放设置更改为 100%以外的任何将停用 Word 文档或 Excel 工作表上的控件。

- **新的项目**对话框的如果不显示控件正确用户更改到的计算机的辅助功能选项**使用高对比度**。

您可以使用放大镜来克服这些限制。 放大镜是创建一个单独的窗口，显示放大屏幕的一部分的 Windows 中的显示实用工具。

## <a name="see-also"></a>请参阅

- [开发 Office 解决方案](../vsto/developing-office-solutions.md)
- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [针对残障人士的辅助功能](../ide/reference/accessibility-for-people-with-disabilities.md)
- [Visual Studio 的辅助功能](../ide/reference/accessibility-features-of-visual-studio.md)