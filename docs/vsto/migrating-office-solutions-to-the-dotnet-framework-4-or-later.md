---
title: 迁移到.NET Framework 4 或更高版本的 Office 解决方案
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.Project.TargetFrameworkWarning
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office projects [Office development in Visual Studio], migrating to .NET Framework 4
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 729fafd1f6dfdf889293c9686f455be8de5a81fc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62970368"
---
# <a name="migrate-office-solutions-to-the-net-framework-4-or-later"></a>迁移到.NET Framework 4 或更高版本的 Office 解决方案
  如果 Office 项目的目标框架更改为[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]或更高版本从.NET Framework 的早期版本，执行一些其他步骤可能还需要继续开发和最终用户计算机上运行该解决方案。 有关详细信息，请参阅[所需更改即可运行迁移到.NET Framework 4 或.NET Framework 4.5 的 Office 项目](../vsto/required-changes-to-run-office-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)。

 此外，可能无法再编译该项目。 对于不同版本的 .NET Framework，Office 项目的一些功能具有不同的编程模型。 当 Office 项目的目标框架从 .NET Framework 的早期版本更改为 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本时，必须对项目进行以下代码更改：

- [更新迁移到.NET Framework 4 或.NET Framework 4.5 的 Excel 和 Word 项目](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)

- [更新迁移到.NET Framework 4 或.NET Framework 4.5 的 Office 项目中的功能区自定义](/visualstudio/vsto/update-ribbon-customizations-in-office-projects-to-migrate-to-dotnet-framework-4-or-4-5)

- [更新迁移到.NET Framework 4 或.NET Framework 4.5 的 Outlook 项目中的窗体区域](../vsto/updating-form-regions-in-outlook-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)

  当从 Visual Studio 的早期版本升级该项目时，Office 项目的目标框架将更改。 有关详细信息，请参阅[升级和迁移 Office 解决方案](../vsto/upgrading-and-migrating-office-solutions.md)。

  对于原因的详细信息的 Office 项目中的某些功能具有不同的编程模型，当你针对[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]或更高版本，请参阅[更改为面向.NET Framework 4 或.NET Framework 4.5Office项目的设计](../vsto/changes-to-the-design-of-office-projects-that-target-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)并[Visual Studio Tools for Office runtime 概述](../vsto/visual-studio-tools-for-office-runtime-overview.md)。

## <a name="see-also"></a>请参阅
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
- [如何：面向 .NET Framework 的某个版本](../ide/how-to-target-a-version-of-the-dotnet-framework.md)
- [对 Office 解决方案中的错误进行故障排除](../vsto/troubleshooting-errors-in-office-solutions.md)
- [Office 解决方案错误的其他支持](../vsto/additional-support-for-errors-in-office-solutions.md)
