---
title: 将计算机配置为开发 Office 解决方案
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, installing tools
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7a0304c217599e790b8cfa9e738245927336470e
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88801836"
---
# <a name="configure-a-computer-to-develop-office-solutions"></a>将计算机配置为开发 Office 解决方案

若要为 Microsoft Office 创建 VSTO 外接程序和自定义项，请安装 Visual Studio、.NET Framework 和 Microsoft Office 的受支持版本。

|软件|支持的版本|
|--------------|------------------------|
|Visual Studio 2017| 具有 **Office/SharePoint 开发** 工作负荷的任何版本。|
|.NET framework|-.NET Framework 4 或更高版本。|
|Microsoft Office|<ul><li>任何 Office suite 版本，包括适用于企业 Microsoft 365 应用。</li><li>以下任一独立应用程序：<br /><br /> <ul><li>Excel</li><li>InfoPath（仅 Office 2013 和 Office 2010）</li><li>Outlook</li><li>PowerPoint</li><li>Project</li><li>Visio</li><li>Word</li></ul></li></ul><br /> Visual Basic for Applications (VBA) 必须作为 Office 的一部分安装。 **重要提示：** 不支持单击运行的 Office 2010 应用程序版本。|

有关详细安装步骤，请参阅 [如何：将计算机配置为开发 Office 解决方案](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)。

## <a name="if-project-templates-dont-appear-or-they-dont-work-in-visual-studio"></a>如果项目模板不显示或在 Visual Studio 中不起作用

如果你安装受支持的 Visual Studio 版本、.NET Framework 和 Microsoft Office，但是 Office 项目模板不显示在 Visual Studio 的 " **新建项目** " 对话框中，或者在你尝试使用它时收到错误，请检查以下内容：

- 确保你已经在计算机上安装了 Microsoft Office 开发人员工具。

     Office 开发人员工具是 Visual Studio 的可选组件，但它们随 Visual Studio 一起自动安装。 如果通过指定要安装的功能来自定义 Visual Studio 安装，请在安装过程中选择 **“Microsoft Office 开发人员工具”** 来安装这些工具。

     若要确保安装这些工具，请启动 Visual Studio 安装程序，并选择 " **修改** " 按钮。 选中 **“Microsoft Office 开发人员工具”** 复选框，然后选择 **“更新”** 按钮。

- 请确保未运行通过 "即用即用" 提供的 Office 版本。 请参阅 [如何：验证 Outlook 是否是计算机上的即用即用应用程序](/previous-versions/office/developer/office-2010/ff864733(v=office.14))。

- 确保你只运行 Microsoft Office 的一个版本。

如果继续遇到问题，请参阅 [Office 解决方案中的错误的其他支持](../vsto/additional-support-for-errors-in-office-solutions.md)。

## <a name="see-also"></a>请参阅
- [开始 &#40;Visual Studio 中的 Office 开发&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [如何：将计算机配置为开发 Office 解决方案](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)
- [如何：安装 Visual Studio Tools for Office 运行时可再发行组件](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)
- [如何：安装 Office 主互操作程序集](../vsto/how-to-install-office-primary-interop-assemblies.md)
- [按 Office 应用程序和项目类型提供的功能](../vsto/features-available-by-office-application-and-project-type.md)