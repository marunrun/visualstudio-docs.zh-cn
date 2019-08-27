---
title: 创建/打开 VSTO 系统项目的 VBA 访问权限
decsprition: You must explicitly enable access to the Office VBA project system before you can create or open a Visual Studio Tools for Office system project
titleSuffix: Visual Studio Tools for Microsoft Office
ms.custom: seodec18
ms.date: 08/14/2019
ms.topic: conceptual
f1_keywords:
- vst.project.vbawrongversion
- VST.Project.VBASecurityGenericError
- VST.Project.VBASecurityPermissions
- VST.SelectDocWizard.MissingCOM
- VST.Project.VBASecurityNotSet
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 3199b23f7ad1bb45fd509d2a9b5cd21da1a49971
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69551542"
---
# <a name="enable-access-to-vba-to-create-or-open-a-visual-studio-tools-for-the-microsoft-office-system-project"></a>启用对 VBA 的访问以创建或打开 Microsoft Office 系统项目的 Visual Studio Tools

您必须显式启用对 Microsoft Office 中的 Visual Basic for Applications (VBA) 项目系统的访问, 然后才能创建或打开 Microsoft Office 系统项目的 Visual Studio Tools。

 Microsoft Office 开发项目需要访问 Microsoft Office Word 和 Microsoft Office Excel 中的 Visual Basic for Applications (VBA) 项目系统, 即使这些项目不使用 Visual Basic for Applications。 Visual Basic 和 C# 项目中控件的设计时支持均需依赖 Visual Basic for Applications 项目系统。

 有些 Microsoft Office 宏病毒会尝试自动运行 Visual Basic for Applications 项目系统来进行传播。 如果启用对 Visual Basic for Applications 项目系统的访问，就失去了帮助防止宏病毒传播的安全保护。 不过，由于正常的宏安全性设置仍然起作用，因此你为 Office 应用程序维护的宏安全级别和受信任的发行者列表将确定是否有任何宏可以在计算机上运行。

> [!NOTE]
> 这仅适用于开发计算机。 最终用户计算机不需要启用此选项即可运行 Office 解决方案。

 值得注意的是，如果计算机此前已经感染宏病毒，则禁用对 Visual Basic for Applications 项目系统的访问本身并不会防止感染病毒，而只能帮助阻止某些病毒传播到其他文档。 默认情况下该选项为禁用状态，从而为你的计算机提供一层额外保护，但如果遵循以下最佳安全做法，即使启用该选项，也不会使你的计算机更易受病毒感染。

 防御 Office 宏病毒的最佳方式是在高或非常高的安全级别上运行 Office, 只信任来自已验证的来源的宏, 并使其保持最新的安全修补程序和病毒扫描程序。

 你可以启用或禁用对**Visual Basic 项目的 "信任访问**" 选项。

 如果看到 VBA 或 COM 错误，则可以修复 Office 的安装。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="to-enable-or-disable-access-to-visual-basic-projects"></a>启用或禁用对 Visual Basic 项目的访问

1. 单击 **“文件”** 选项卡。

2. 单击“选项”。

3. 单击 "**信任中心**", 然后单击 "**信任中心设置**"。

4. 在 "**信任中心**", 单击 "**宏设置**"。

5. 选中或取消选中 **"信任对 VBA 项目对象模型的访问权限"** 以启用或禁用对 Visual Basic 项目的访问。

6. 单击 **“确定”** 。

### <a name="to-enable-or-disable-access-to-visual-basic-projects-with-the-2007-microsoft-office-system"></a>使用 2007 Microsoft Office 系统启用或禁用对 Visual Basic 项目的访问

1. 在 Word 或 Excel 中的 "**工具**" 菜单上, 指向 "**宏**", 然后单击 "**安全**"。

2. 在 "**安全**" 对话框中, 单击 "**受信任的发布者**" 选项卡。

3. 选择 "启用" 或 "清除" 以禁用,**信任对 Visual Basic 项目的访问**。

4. 单击 **“确定”** 。

## <a name="to-set-your-office-macro-security-level"></a>设置 Office 宏安全级别

1. 单击 **“文件”** 选项卡。

2. 单击“选项”。

3. 单击 "**信任中心**", 然后单击 "**信任中心设置**"。

4. 在 "**信任中心**", 单击 "**宏设置**"。

5. 在 "**宏设置**" 部分中, 选择所需的设置。

6. 单击 **“确定”** 。

### <a name="to-set-your-office-macro-security-level-with-the-2007-microsoft-office-system"></a>将 Office 宏安全级别设置为 2007 Microsoft Office 系统

1. 在 Word 或 Excel 中的 "**工具**" 菜单上, 指向 "**宏**", 然后单击 "**安全**"。

2. 在 "**安全级别**" 选项卡上, 选择所需的设置。

    "**安全级别**" 选项卡包含有关每个级别的详细信息。 有关详细信息，请参阅“Office 帮助”中的“宏安全级”主题。

### <a name="to-install-vba-with-the-2007-microsoft-office-system"></a>通过 2007 Microsoft Office 系统安装 VBA

1. 在 "控制面板" 中, 运行 "**添加或删除程序**" 或 "**程序和功能**"。

2. 选择 "**当前安装的程序**" 列表中的 "Office"。

3. 单击“更改”。

4. 选择 "**添加或删除功能**", 然后单击 "**继续**"。

5. 选择 "**选择应用程序的高级自定义**", 然后单击 "**下一步**"。

6. 在 "**选择应用程序和工具的更新选项**" 列表中展开 " **Office 共享功能**"。

7. 打开 " **Visual Basic for Applications**" 旁边的下拉菜单, 然后单击 "**从我的电脑运行**"。

8. 单击 **“继续”** 。

9. 单击 **“关闭”** 。

## <a name="to-repair-your-installation-of-office"></a>修复 Office 安装

1. 在 "控制面板" 中, 运行 "**添加或删除程序**" 或 "**程序和功能**"。

2. 在 "**当前安装的程序**" 列表中选择 Office 版本。

3. 单击“更改”。

4. 选择 "**重新安装或修复**", 然后单击 "**下一步**"。

5. 选择 "**检测并修复 Office 安装中的错误**", 然后单击 "**安装**"。

## <a name="see-also"></a>请参阅
- [保护 Office 解决方案](../vsto/securing-office-solutions.md)
