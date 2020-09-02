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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62951183"
---
# <a name="custom-document-properties-overview"></a>自定义文档属性概述

生成文档级项目时，Visual Studio 会将两个自定义属性添加到项目中的文档： \_ AssemblyLocation 和 \_ AssemblyName。 当用户打开文档时，Microsoft Office 应用程序会检查这些自定义文档属性。 如果这些文件存在于文档中，则应用程序将加载 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ，这将启动自定义。 有关详细信息，请参阅 [Visual Studio 中的 Office 解决方案的体系结构](../vsto/architecture-of-office-solutions-in-visual-studio.md)。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="_assemblyname"></a>\_AssemblyName

此属性包含的 Office 解决方案加载程序组件中的接口的 CLSID [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。 CLSID 值为4E3C66D5-58D4-491E-A7D4-64AF99AF6E8B。 永远不应更改此值。

## <a name="_assemblylocation"></a>\_AssemblyLocation

此属性包含一个字符串，该字符串提供有关自定义项的部署清单的详细信息。 有关清单的详细信息，请参阅 [Office 解决方案中的应用程序和部署清单](../vsto/application-and-deployment-manifests-in-office-solutions.md)。

 \_AssemblyLocation 属性值的格式可以不同，具体取决于解决方案的部署方式：

- 如果将解决方案发布为从网站、UNC 路径或 CD 或 USB 驱动器进行安装，则 _AssemblyLocation 属性的格式为*DeploymentManifestPath* | *SolutionID*。 以下字符串是一个示例：

     file://deployserver/MyShare/ExcelWorkbook1.vsto|74744e4b-e4d6-41eb-84f7-ad20346fe2d9

- 如果正在运行或调试 Visual Studio 中的解决方案，则 _AssemblyLocation 属性的格式为*DeploymentManifestName* | *SolutionID*| vstolocal。 以下字符串是一个示例：

     Excelworkbook1.xlsx.log | 74744e4b-e4d6-41eb-84f7-ad20346fe2d9 | vstolocal

  *SolutionID*是用于标识解决方案的 GUID [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。 生成项目时，会自动生成 *SolutionID* 。 **Vstolocal**项指示 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 程序集应与文档从同一文件夹中加载。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中 Office 解决方案的体系结构](../vsto/architecture-of-office-solutions-in-visual-studio.md)
- [文档级自定义项的体系结构](../vsto/architecture-of-document-level-customizations.md)
- [Office 解决方案中的应用程序和部署清单](../vsto/application-and-deployment-manifests-in-office-solutions.md)
- [如何：使用 ClickOnce 发布 Office 解决方案](https://msdn.microsoft.com/2b6c247e-bc04-4ce4-bb64-c4e79bb3d5b8)
- [如何：创建和修改自定义文档属性](../vsto/how-to-create-and-modify-custom-document-properties.md)
