---
title: 使用 Visual Studio 创建 VSTO 外接程序
titleSuffix: ''
ms.custom: seodec18
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e64d97b948f38b4c9b5943d5e561aa865d4f765f
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69551662"
---
# <a name="create-vsto-add-ins-for-office-by-using-visual-studio"></a>使用 Visual Studio 创建 VSTO 外接程序
  可以使用 Visual Studio 中的 Microsoft Office 开发人员工具来创建可扩展 Office 的 .NET Framework 应用程序。 这些应用程序也称为“Office 解决方案”。

 Office 开发人员工具提供了一些功能，可帮助你创建适合于各种业务需求的 Office 解决方案。 这些工具包括项目模板和可视化设计器，前者有助于你通过使用 Visual Basic 或 Visual C# 创建 Office 解决方案，后者有助于你为 Office 解决方案创建自定义用户界面。

[!include[Add-ins note](includes/addinsnote.md)]

 有关 Office 开发的最新信息，请访问 MSDN 上的以下开发中心：

- 使用[Visual studio 开发人员门户进行 Office 开发](http://go.microsoft.com/fwlink/?LinkId=123844)包含指向产品信息、代码示例、视频和社区资源的链接, 这些链接指向有关使用 Visual Studio 将 Office 应用程序自定义为解决方案的一部分的信息。

- [Microsoft Office 开发人员中心](http://go.microsoft.com/fwlink/?LinkId=83467)包含一些链接, 这些链接指向技术文章、代码示例、下载、社区信息、支持以及有关 office 自定义项和 office Business Applications (oba) 的其他文档。

## <a name="in-this-section"></a>本节内容
- [Visual Studio &#40;中的 Office 开发入门&#41;](../vsto/getting-started-office-development-in-visual-studio.md)

 提供一些链接，这些链接指向有关如何配置开发计算机以创建 Office 解决方案、如何开始创建 Office 解决方案以及 Visual Studio 中的 Office 开发的新增功能的信息。

- [升级和迁移 Office 解决方案](../vsto/upgrading-and-migrating-office-solutions.md)

 提供一些链接，这些链接指向有关使用 Visual Studio 早期版本创建的项目的升级过程的信息。

- [Visual Studio 中 Office 解决方案的体系结构](../vsto/architecture-of-office-solutions-in-visual-studio.md)

 提供一些链接，这些链接指向有关 Office 解决方案的工作原理的信息，其中包括有关文档级自定义项和 VSTO 外接程序的信息。

- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)

 提供有关如何在 Visual Studio 中创建和配置 Office 项目的信息。

- [开发 Office 解决方案](../vsto/developing-office-solutions.md)

 提供有关如何在 Office 解决方案中使用托管代码的信息，其中包括如何自定义 Office 用户界面、使用数据以及解决问题的信息。

- [Excel 解决方案](../vsto/excel-solutions.md)

 提供有关如何实现 Excel 自动化、创建 Excel 解决方案以及了解特定于 Excel 的全球化问题的信息。

- [InfoPath 解决方案](../vsto/infopath-solutions.md)

 提供有关如何创建 InfoPath 的表单模板和 VSTO 外接程序的信息。

- [Outlook 解决方案](../vsto/outlook-solutions.md)

 提供有关如何实现 Outlook 自动化以及创建 Outlook VSTO 外接程序和窗体区域的信息。

- [PowerPoint 解决方案](../vsto/powerpoint-solutions.md)

 提供有关如何实现 PowerPoint 自动化和创建 PowerPoint VSTO 外接程序的信息。

- [项目解决方案](../vsto/project-solutions.md)

 提供有关如何自动 Microsoft Office 项目和创建 project VSTO 外接程序的信息。

- [Visio 解决方案](../vsto/visio-solutions.md)

 提供有关如何实现 Visio 自动化和创建 Visio VSTO 外接程序的信息。

- [Word 解决方案](../vsto/word-solutions.md)

 提供有关如何实现 Word 自动化和创建 Word 解决方案的信息。

- [构建 Office 解决方案](../vsto/building-office-solutions.md)

 提供有关在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中生成 Office 项目和其他类型项目之间的差异的信息。

- [调试 Office 项目](../vsto/debugging-office-projects.md)

 提供有关在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中调试 Office 项目和其他类型项目之间的差异的信息。

- [保护 Office 解决方案](../vsto/securing-office-solutions.md)

 提供有关 Office 解决方案中安全功能的工作原理的信息。

- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)

 提供有关如何让用户使用 Office 解决方案，以及在选择部署方法时要考虑的主要问题的信息。

- [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)

 提供指向示例应用程序和主题的链接，这些主题提供有关执行常规任务的分步说明。

- [Visual Studio &#40;中的常规参考 Office 开发&#41;](../vsto/general-reference-office-development-in-visual-studio.md)

 提供指向有关 Office 主互操作程序集、清单、用户界面元素和错误消息的详细信息的链接。

- [Visual Studio &#40;中的托管引用 Office 开发&#41;](../vsto/managed-reference-office-development-in-visual-studio.md)

 提供指向有关在 Office 项目中使用的针对 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]的 API 命名空间和类型的链接。 对于在 Office 项目中使用的针对 .NET Framework 3.5 的有关命名空间和类型的 API 参考文档，请参阅下列 Visual Studio 2008 文档中的参考资料部分：[2007 系统托管参考](http://go.microsoft.com/fwlink/?LinkId=160658)。

- [Visual Studio 中&#40;的非托管 API 参考 Office 开发&#41;](../vsto/unmanaged-api-reference-office-development-in-visual-studio.md)

 包含一些链接，这些链接指向有关可以使用 COM 接口执行各种操作（例如加载和卸载 Office 应用程序中托管 VSTO 外接程序）方面的信息。

## <a name="related-sections"></a>相关章节
- [Visual Studio 开发人员门户中的 Office 开发](http://go.microsoft.com/fwlink/?LinkId=123844)提供其他资源, 例如技术文章、视频和博客。

- [Visual Studio 开发人员中心](http://go.microsoft.com/fwlink/?LinkID=99124)提供其他 Visual Studio 资源, 例如技术文章、视频和博客。

- [Office Business Applications 开发人员门户](http://go.microsoft.com/fwlink/?LinkId=99125)提供有关 Office Business Applications (Oba) 以及如何使用 Office 系统平台生成这些信息的信息。

- [MSDN library Microsoft Office 开发部分](http://go.microsoft.com/fwlink/?LinkId=149870)MSDN library 的区域, 可在其中找到有关开发多个版本的 Office (不特定于使用 Visual Studio 的 Office 开发) 的解决方案的文章和参考文档。

- [Visual Studio 中的应用程序开发](https://msdn.microsoft.com/97490c1b-a247-41fb-8f2c-bc4c201eff68)包含指向一些主题的链接, 这些主题说明如何使用 Visual Studio 设计、开发、调试和部署 web 应用程序、XML web 服务和传统客户端应用程序。

- [Visual Studio 中的 .NET Framework 编程](/previous-versions/visualstudio/visual-studio-2010/k1s94fta(v=vs.100))讨论 .NET Framework 在 Visual Basic 和视觉对象C#中的应用程序开发。
