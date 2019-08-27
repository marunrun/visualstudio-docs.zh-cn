---
title: 合作开发 Office 解决方案
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], collaborative development
- Office development in Visual Studio, collaboration
- source control [Office development in Visual Studio]
- collaborative development [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 76c26a110d88d3dee8bf7540647ea0bfde4e7c4f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62949482"
---
# <a name="collaborative-development-of-office-solutions"></a>合作开发 Office 解决方案
  多个开发人员可以从事方式协同工作上的其他 Visual Studio 项目完全相同的 Office 项目。 即使在不同的位置安装 Office，visual Studio 正确定位每台计算机上的 Microsoft Office 安装。 但是，有需要注意的一些重要注意事项。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="debug-properties-are-not-shared"></a>调试不共享属性
 调试属性不在源控件下的多个用户中共享。 Visual Basic 和 VisualC#项目调试属性存储在特定于用户的文件 (*ProjectName*。 vbproj.user 或*ProjectName*。 csproj.user)，但此文件不在源代码管理下. 如果有多个用户正在调试，则每个用户都必须手动输入调试属性。

 如果项目存储在源代码管理中而不是网络共享上，则必须采取一些额外的步骤使协作的开发人员能够打开解决方案并测试程序集。

## <a name="source-control-requires-checking-out-all-files"></a>源代码管理需要签出的所有文件
 如果为你的项目使用源代码管理，您应该看看下的代码文件中的文件的所有**解决方案资源管理器**(如*ThisDocument*， *ThisWorkbook*，或*ThisAddIn*代码文件) 每次更改的代码文件，即使是默认情况下隐藏的文件。 如果签出只有顶级代码文件时，所做的更改可能会丢失。

 进行更改后，检查中的所有文件备份。 有关在项目中的隐藏的代码文件的详细信息，请参阅[Visual Studio 环境中的 Office 项目](../vsto/office-projects-in-the-visual-studio-environment.md)。

## <a name="security-for-informal-collaboration-on-a-network"></a>在网络上的非正式协作的安全性
 在网络位置的所有文档级解决方案 (如\\ \\ *Servername*\\*Sharename*)，必须将完全限定的位置添加到你正在使用的 Microsoft Office 应用程序中的受信任的文件夹列表。 选择选项以包括的主文件夹下的子目录或专门添加调试和生成的受信任的文件夹列表中的文件夹。 有关如何执行此操作的详细信息，请参阅[向文档授予信任](../vsto/granting-trust-to-documents.md)。

 在生成时自动生成的临时证书不是安全的密码。 证书中包含开发人员的登录名和其他个人信息。 如果部署的临时证书所签名的自定义项，其他人可以访问此信息。

## <a name="see-also"></a>请参阅
- [保护 Office 解决方案](../vsto/securing-office-solutions.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
- [生成 Office 解决方案](../vsto/building-office-solutions.md)
