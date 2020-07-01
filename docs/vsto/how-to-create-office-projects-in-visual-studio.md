---
title: 如何：在 Visual Studio 中创建 Office 项目
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VST.SelectDocWizard.Page1
- VST.SelectDocWizard.Http
- VST.SelectDocWizard.Extension
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- add-ins [Office development in Visual Studio], creating projects
- Office applications [Office development in Visual Studio], creating
- Office projects [Office development in Visual Studio]
- projects [Office development in Visual Studio], creating
- document-level customizations [Office development in Visual Studio], creating
- application-level add-ins [Office development in Visual Studio], creating projects
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c70668f2d4cb9597e00a7e3848b78b9f2ed49db7
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547558"
---
# <a name="how-to-create-office-projects-in-visual-studio"></a>如何：在 Visual Studio 中创建 Office 项目
  你可以使用 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 来创建 Microsoft Office 应用程序的 VSTO 外接程序和文档级自定义项。 有关这些项目类型的详细信息，请参阅[Office 解决方案开发概述 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-create-a-vsto-add-in-project"></a>创建 VSTO 外接程序项目

1. 在“文件”菜单上，选择“新建” > “项目”************。 如果集成开发环境（IDE）设置为使用 [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] 开发设置，请在 "**文件**" 菜单上选择 "**新建**  >  **项目**"。

    将显示“新建项目”对话框。

   > [!NOTE]
   > 默认情况下，Office 项目均面向 [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]。 有关详细信息，请参阅[.NET Framework 客户端配置文件](/dotnet/framework/deployment/client-profile)。

2. 在 "模板" 窗格中要使用的语言节点下，展开 " **Office/SharePoint**"。

3. 选择 " **Office 外接程序**" 节点。

4. 在项目模板列表中，选择 VSTO 外接程序项目模板。 有关可用 VSTO 外接程序项目模板的列表，请参阅[Office 项目模板概述](../vsto/office-project-templates-overview.md)。

   > [!NOTE]
   > 如果在选择 " **Office 外接程序**" 节点时项目模板不可见，请确保在对话框顶部的组合框中选择了 " **.NET Framework 4**或更高版本"。 Office 项目模板对于 .NET Framework 的两个版本均为可见。

5. 在 "**名称**" 框中，键入项目的名称。 默认情况下，项目名称也可用作解决方案名称。

6. 在 "**位置**" 框中，输入要在其中创建项目的路径。 你可以使用绝对路径和通用命名约定 (UNC) 路径。 不允许使用 HTTP、FTP 或其他协议的路径。

    位置具有以下格式：

   * [*驱动器*\]\:

   * \\\\*服务器* \\*共享*

     不允许在该位置中使用以下字符：

   * 星号 (*)

   * 竖线 (|)

   * 冒号 (:)（接在驱动器号之后的情况除外）

   * 双引号 (")（包含空格的路径不需要引号。）

   * 小于号 (\<)

   * 大于号 (>)

   * 问号 (?)

   * 百分号 (%)

7. 选择“确定”  按钮。

   ::: moniker range="vs-2017"

   > [!NOTE]
   > 创建外接程序项目时，要始终对其进行保存。 不能将其创建为临时项目。 有关临时项目的详细信息，请参阅[临时项目](../ide/creating-solutions-and-projects.md#create-a-temporary-project)。

   ::: moniker-end

### <a name="to-create-a-document-level-customization-project"></a>若要创建文档级自定义项目

1. 在“文件”菜单上，选择“新建” > “项目”************。 如果 IDE 设置为使用 Visual Basic 开发设置，请在 "**文件**" 菜单上选择 "**新建**  >  **项目**"。

    将显示“新建项目”对话框。

2. 在 "模板" 窗格中要使用的语言节点下，展开 " **Office/SharePoint**"。

3. 选择“Office 外接程序” **** 节点。

4. 在项目模板列表中，选择一个文档级项目模板。 有关可用文档级项目模板的列表，请参阅[Office 项目模板概述](../vsto/office-project-templates-overview.md)。

   > [!NOTE]
   > 如果在选择 " **Office 外接程序**" 节点时项目模板不可见，请确保已选中 **.NET Framework 4**或更高版本。

5. 在 "**名称**" 框中，键入项目的名称。 默认情况下，此名称还用于文档。 如果 IDE 设置为使用 Visual C# 开发设置或常规开发设置，请输入位置和解决方案名称。

   > [!NOTE]
   > 不能在项目位置路径或项目名称中使用代理项字符。 此外，如果计划部署脱机使用的解决方案，则该项目名称中的字符必须符合 HTTP 协议规范。

6. 选择“确定”  按钮。

    将打开“Visual Studio Tools for Office 项目向导” **** 。

7. 如果要为解决方案创建新文档，请选择 "**创建新文档**"，如果要自定义现有文档，请选择 "**复制现有文档**"。

    如果创建新文档，请在 "**名称**" 框中指定名称，然后使用 "**格式**" 框选择文档格式。 有关可用格式的详细信息，请参阅[文档级自定义项的体系结构](../vsto/architecture-of-document-level-customizations.md)。

    如果使用现有文档，请在 "**现有文档的完整路径**" 框中指定文档的位置。 可以使用绝对路径和 UNC 路径。 不允许使用 HTTP、FTP 或其他协议的路径指定文档位置。

    位置具有以下格式：

   - [*驱动器*\]\:

   - \\\\*服务器* \\*共享*

     不允许在该位置中使用以下字符：

   - 星号 (*)

   - 竖线 (|)

   - 冒号 (:)（接在驱动器号之后的情况除外）

   - 双引号 (")（包含空格的路径不需要引号。）

   - 小于号 (\<)

   - 大于号 (>)

   - 问号 (?)

   - 百分号 (%)

   > [!NOTE]
   > 如果在 [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] 项目中使用现有文档，则只能使用在 [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] 项目中创建的或转换为该项目格式的文档。 类似地，如果在 Word 2010 项目中使用现有文档，则只能使用在 Word 2010 中创建的或转换为该文档格式的文档。 如果使用 Word 早期版本创建的文档，将禁用文档中的某些功能。 如果尝试编写使用这些功能的代码，可能会在项目中出现错误。 若要转换文档，请在或 Word 2010 中打开它， [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] 在功能区上的 "**文件**" 选项卡上，选择 "**信息**  >  **转换**"。

8. 选择 **“完成”**。

9. 在以下情况中将项目文件夹及其子文件夹添加到 Word“信任中心”中的受信任位置的列表中：

   - 正在创建一个基于*docm*文件的 Word 文档，该文档包含一个或 Windows 窗体控件的 VBA 项目。 将项目文件夹添加到受信任位置的列表将有助于确保文档在设计时能够按预期正常工作。

   - 正在创建基于*dotx*文件的 Word 模板项目。 必须将项目文件夹添加到受信任位置列表中，以便可以运行并调试项目。

     有关如何向受信任位置添加文档的详细信息，请参阅 Microsoft Office Online 网站[创建、删除或更改文件的受信任位置](https://support.office.com/article/Create-remove-or-change-a-trusted-location-for-your-files-f5151879-25ea-4998-80a5-4208b3540a62)。

## <a name="see-also"></a>另请参阅
- [Office 项目模板概述](../vsto/office-project-templates-overview.md)
- [开发 Office 解决方案的协作开发](../vsto/collaborative-development-of-office-solutions.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
- [VSTO 外接程序编程入门](../vsto/getting-started-programming-vsto-add-ins.md)
