---
title: 配置计算机以开发 Office 解决方案
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
ms.openlocfilehash: e559ddfec8570077a78fe980632366b4a57605de
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62930956"
---
# <a name="configure-a-computer-to-develop-office-solutions"></a>配置计算机以开发 Office 解决方案

若要为 Microsoft Office 创建 VSTO 外接程序和自定义项，请安装 Visual Studio、.NET Framework 和 Microsoft Office 的受支持版本。

|软件|受支持的版本|
|--------------|------------------------|
|Visual Studio 2017| 与任何版本**Office/SharePoint 开发**工作负荷。|
|.NET Framework|-.NET Framework 4 或更高版本。|
|Microsoft Office|<ul><li>任何 Office 套件版本，包括 Office Professional Plus for Office 365。</li><li>以下任一独立应用程序：<br /><br /> <ul><li>Excel</li><li>InfoPath（仅 Office 2013 和 Office 2010）</li><li>Outlook</li><li>PowerPoint</li><li>项目</li><li>Visio</li><li>字</li></ul></li></ul><br /> Visual Basic for Applications (VBA) 必须作为 Office 的一部分安装。 **重要提示：** Office 2010 应用程序的“即点即用”版本不受支持。|

有关详细的安装步骤，请参阅[如何：配置计算机以开发 Office 解决方案](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)。

## <a name="if-project-templates-dont-appear-or-they-dont-work-in-visual-studio"></a>如果不显示项目模板，或它们不适用于 Visual Studio 中

如果你安装受支持的版本的 Visual Studio、.NET Framework 和 Microsoft Office，但是 Office 项目模板不显示在 Visual Studio**新的项目**对话框中，或收到错误，当尝试使用其中一个，检查以下各项：

- 确保你已经在计算机上安装了 Microsoft Office 开发人员工具。

     Office 开发人员工具是可选组件的 Visual Studio 中，但它们与 Visual Studio 一起自动安装。 如果通过指定要安装的功能来自定义 Visual Studio 安装，请在安装过程中选择 **“Microsoft Office 开发人员工具”** 来安装这些工具。

     若要确保安装这些工具，请启动 Visual Studio 安装程序，然后选择**修改**按钮。 选中 **“Microsoft Office 开发人员工具”** 复选框，然后选择 **“更新”** 按钮。

- 请确保你未正在运行的即用已传送的 Office 版本。 请参阅[如何：验证 Outlook 是否是一台计算机上的即用应用程序](/previous-versions/office/developer/office-2010/ff864733(v=office.14))。

- 确保运行只有一个版本的 Microsoft Office。

如果继续遇到问题，请参阅[Office 解决方案错误的其他支持](../vsto/additional-support-for-errors-in-office-solutions.md)。

## <a name="see-also"></a>请参阅
- [开始&#40;Visual Studio 中的 Office 开发&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [如何：配置计算机以开发 Office 解决方案](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)
- [如何：安装 Visual Studio Tools for Office runtime 可再发行组件](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)
- [如何：安装 Office 主互操作程序集](../vsto/how-to-install-office-primary-interop-assemblies.md)
- [按 Office 应用程序和项目类型提供的功能](../vsto/features-available-by-office-application-and-project-type.md)