---
title: 通过主互操作程序集面向 Office 应用程序
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- assemblies [Office development in Visual Studio], PIA references
- primary interop assemblies [Office development in Visual Studio], adding references to
- Office primary interop assemblies in Visual Studio, adding references to
- Office applications [Office development in Visual Studio], automating
- application development [Office development in Visual Studio], automating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 60e351a15af4994d2bf64a800e3019501cf0571d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545764"
---
# <a name="how-to-target-office-applications-through-primary-interop-assemblies"></a>如何：通过主互操作程序集面向 Office 应用程序
  在创建新的 Office 项目时，Visual Studio 会自动添加对生成该项目所需的 Microsoft Office 主互操作程序集 (PIA) 的引用。 在以下方案中，必须添加对其他 PIA 的引用：

- 想要在项目中使用其他 Microsoft Office 应用程序的功能。 例如，你可能想要在 Microsoft Office Word 的项目中使用 Microsoft Office Excel 中的功能。

- 你想要自动化在 Visual Studio 中没有专用项目的 Microsoft Office 应用程序，如 Microsoft Office Access。

  [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="to-add-a-reference-to-a-primary-interop-assembly"></a>添加对主互操作程序集的引用

1. 打开 Office 项目，并选择 "**解决方案资源管理器**中的项目名称。

2. 在“项目”菜单上，单击“添加引用”   。

3. 在 "**框架**" 选项卡上的 "**组件名称**" 列表中，选择所需的 PIA。 有关可用 Microsoft Office 主互操作程序集的详细信息，请参阅[Office 主互操作程序集](../vsto/office-primary-interop-assemblies.md)。

     如果项目面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本，则默认情况下，程序集引用的 "**嵌入互操作类型**" 属性设置为 " **True** "。 通过使用此设置，你的解决方案在最终用户计算上不需要 PIA。 有关详细信息，请参阅[设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)。

    > [!NOTE]
    > 在 Office 项目中，始终使用 "**添加引用**" 对话框的 " **.net** " 选项卡而不是 " **COM** " 选项卡添加对 office pia 的引用。有关详细信息，请参阅[Office 主互操作程序集](../vsto/office-primary-interop-assemblies.md)。

4. 单击 **“确定”** 。

     程序集名称出现在**解决方案资源管理器**的 "**引用**" 文件夹中。

## <a name="see-also"></a>请参阅
- [Office 主互操作程序集](../vsto/office-primary-interop-assemblies.md)
- [在 Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)
- [开发 Office 解决方案](../vsto/developing-office-solutions.md)
- [如何：安装 Office 主互操作程序集](../vsto/how-to-install-office-primary-interop-assemblies.md)
