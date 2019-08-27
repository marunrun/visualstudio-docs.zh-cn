---
title: 使用本地数据库文件在 Office 解决方案概述
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], data
- data [Office development in Visual Studio], local
- local data [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: ea260a6286c8a923d56ab7a5088b55de57004489
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62982236"
---
# <a name="use-local-database-files-in-office-solutions-overview"></a>使用本地数据库文件在 Office 解决方案概述
  可以包括数据库文件，如 SQL Server Express (*.mdf*) 文件或 Microsoft Office Access (*.mdb*) 文件，在 Office 解决方案中的。 这使最终用户能够在其中维护集中式的数据库不是必需的例如在只有一台计算机使用的本地清单解决方案的情况下对本地数据库进行维护。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="import-the-database-file-into-a-project"></a>数据库文件导入项目
 若要将数据库文件导入你的项目，请使用**数据源配置向导**创建基于数据库文件的数据源。 该向导将数据库文件和类型化数据集添加到你的项目。

## <a name="deploy-the-database-file"></a>将数据库文件部署
 **数据源配置向导**使用相对路径来创建连接到本地数据库文件。 这使您可以将解决方案从一台计算机复制到另一个，如果要保留文件的相对位置。

 如果你将解决方案部署到服务器，然后将分发到每个最终用户的文档，必须手动分发数据库的文件并安装在同一位置相对于文档。 这意味着，最终用户不能将文档移到新位置上他或她的计算机，除非他或她还将移动数据库文件。

## <a name="local-database-files-and-caching-the-dataset"></a>本地数据库文件和缓存数据集
 在 Microsoft Office Excel 和 Microsoft Office Word 文档级解决方案中，可以通过将标记具有属性的数据集实例缓存在文档中的数据集<xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute>。 当您将数据库文件添加到你的项目通过使用**数据源配置向导**，类型化数据集将自动添加到你的项目。 很少需要应用<xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute>到此数据集，因为数据已经是本地用户的计算机上。 有关详细信息，请参阅[缓存数据](../vsto/caching-data.md)。

## <a name="see-also"></a>请参阅
- [将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [如何：用数据库中的数据填充文档](../vsto/how-to-populate-documents-with-data-from-a-database.md)
- [如何：使用主机控件中的数据更新数据源](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
- [缓存数据](../vsto/caching-data.md)
