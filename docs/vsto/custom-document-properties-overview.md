---
title: 自定义文档属性概述
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], custom properties
- custom document properties
- document-level customizations [Office development in Visual Studio], custom properties
- Office documents [Office development in Visual Studio], custom properties
- _AssemblyLocation property
- _AssemblyName property
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7b3f4038a05478d8e2d747efa700c7ece02e4827
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62951183"
---
# <a name="custom-document-properties-overview"></a>自定义文档属性概述

生成的文档级项目时，Visual Studio 会将两个自定义属性添加到项目中的文档：\_程序集位置和\_程序集名称。 当用户打开的文档时，Microsoft Office 应用程序将检查这些自定义文档属性。 如果它们存在文档中，应用程序加载[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]，从而启动自定义项。 有关详细信息，请参阅[Visual Studio 中的体系结构的 Office 解决方案](../vsto/architecture-of-office-solutions-in-visual-studio.md)。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="assemblyname"></a>\_AssemblyName

此属性包含的接口中的 Office 解决方案加载程序组件的 CLSID [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]。 CLSID 值为 4E3C66D5-58 D 4-491E-A7D4-64AF99AF6E8B。 永远不应更改此值。

## <a name="assemblylocation"></a>\_AssemblyLocation

此属性包含用于自定义提供有关部署清单的详细信息的字符串。 有关清单的详细信息，请参阅[应用程序和部署清单在 Office 解决方案中](../vsto/application-and-deployment-manifests-in-office-solutions.md)。

 \_AssemblyLocation 属性值可以具有不同的格式，具体取决于解决方案的部署方式：

- 如果发布的解决方案安装从 Web 站点、 UNC 路径或 CD 或 USB 驱动器，_AssemblyLocation 属性具有格式*部署清单路径*|*SolutionID*。 以下字符串是一个示例：

     file://deployserver/MyShare/ExcelWorkbook1.vsto|74744e4b-e4d6-41eb-84f7-ad20346fe2d9

- 如果你正在运行或调试从 Visual Studio 解决方案，_AssemblyLocation 属性具有格式*DeploymentManifestName*|*SolutionID*| vstolocal。 以下字符串是一个示例：

     ExcelWorkbook1.vsto|74744e4b-e4d6-41eb-84f7-ad20346fe2d9|vstolocal

  *SolutionID*是一个 GUID，[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]使用其标识解决方案。 *SolutionID*生成项目时自动生成。 **Vstolocal**词表明到[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]，该程序集应加载从该文档所在的文件夹。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的 Office 解决方案的体系结构](../vsto/architecture-of-office-solutions-in-visual-studio.md)
- [文档级自定义项的体系结构](../vsto/architecture-of-document-level-customizations.md)
- [在 Office 解决方案中的应用程序和部署清单](../vsto/application-and-deployment-manifests-in-office-solutions.md)
- [如何：使用 ClickOnce 发布 Office 解决方案](https://msdn.microsoft.com/2b6c247e-bc04-4ce4-bb64-c4e79bb3d5b8)
- [如何：创建和修改自定义文档属性](../vsto/how-to-create-and-modify-custom-document-properties.md)
