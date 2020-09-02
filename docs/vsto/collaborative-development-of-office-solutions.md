---
title: 开发 Office 解决方案的协作开发
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62949482"
---
# <a name="collaborative-development-of-office-solutions"></a>开发 Office 解决方案的协作开发
  多个开发人员可以采用与在其他 Visual Studio 项目上协作的相同方式来处理 Office 项目。 即使 Office 安装在不同的位置，Visual Studio 也会正确地在每台计算机上查找 Microsoft Office 安装。 但是，需要注意一些重要的注意事项。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="debug-properties-are-not-shared"></a>调试属性不共享
 调试属性不在源控件下的多个用户中共享。 Visual Basic 和 Visual c # 项目将调试属性存储在用户特定文件中， * (.vbproj*或文件 *名称*) ，并且此文件不受源代码管理。 如果有多个用户正在调试，则每个用户都必须手动输入调试属性。

 如果项目位于网络共享而不是源代码管理中，则必须执行一些额外的步骤以使协作开发人员能够打开解决方案并测试程序集。

## <a name="source-control-requires-checking-out-all-files"></a>源代码管理需要签出所有文件
 如果对项目使用源代码管理，则应在每次更改代码文件时（甚至是默认情况下隐藏的文件），在代码文件中的所有文件 **解决方案资源管理器** (，如 *ThisDocument*、 *ThisWorkbook*或 *ThisAddIn* 代码) 文件。 如果仅签出顶级代码文件，则所做的更改可能会丢失。

 进行更改后，请重新检查所有文件。 有关项目中隐藏代码文件的详细信息，请参阅 [Visual Studio 环境中的 Office 项目](../vsto/office-projects-in-the-visual-studio-environment.md)。

## <a name="security-for-informal-collaboration-on-a-network"></a>网络上的非正式协作的安全性
 对于位于网络位置 (例如 Servername 共享) 中的所有文档级解决方案 \\ \\ *Servername* \\ *Sharename* ，必须将完全限定的位置添加到正在使用的 Microsoft Office 应用程序中的受信任文件夹列表。 选择此选项以在主文件夹下包含子目录，或者将调试文件夹和生成文件夹专门添加到受信任文件夹列表。 有关如何执行此操作的详细信息，请参阅 [向文档授予信任](../vsto/granting-trust-to-documents.md)。

 在生成时自动生成的临时证书不受密码保护。 证书包含开发人员的登录名和其他个人信息。 如果部署由临时证书签名的自定义项，则其他人可以访问此信息。

## <a name="see-also"></a>另请参阅
- [保护 Office 解决方案](../vsto/securing-office-solutions.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
- [构建 Office 解决方案](../vsto/building-office-solutions.md)
