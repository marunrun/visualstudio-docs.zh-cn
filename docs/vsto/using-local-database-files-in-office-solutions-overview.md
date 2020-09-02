---
title: 在 Office 解决方案中使用本地数据库文件概述
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62982236"
---
# <a name="use-local-database-files-in-office-solutions-overview"></a>在 Office 解决方案中使用本地数据库文件概述
  你可以在 Office 解决方案中包括数据库文件，如 SQL Server Express (*.mdf*) 文件或 Microsoft Office*访问 (文件。* 这使最终用户能够在不需要维护集中数据库的情况下维护本地数据库，例如，在仅在一台计算机上使用的本地清单解决方案中。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="import-the-database-file-into-a-project"></a>将数据库文件导入到项目中
 若要将数据库文件导入到项目中，请使用 " **数据源配置向导** " 创建基于数据库文件的数据源。 向导可将数据库文件和类型化数据集添加到项目。

## <a name="deploy-the-database-file"></a>部署数据库文件
 " **数据源配置向导** " 使用相对路径来创建到本地数据库文件的连接。 这使你可以将解决方案从一台计算机复制到另一台计算机，前提是你维护这些文件的相对位置。

 如果将解决方案部署到服务器，然后将文档分发给每个最终用户，则还必须手动分发数据库文件，并将其安装在相对于文档的同一位置。 这意味着，最终用户无法将该文档移到其计算机上的新位置，除非该用户也移动该数据库文件。

## <a name="local-database-files-and-caching-the-dataset"></a>本地数据库文件和缓存数据集
 在 Microsoft Office Excel 和 Microsoft Office Word 的文档级解决方案中，可以通过使用特性标记数据集实例来缓存文档中的数据集 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 。 使用 " **数据源配置向导**" 将数据库文件添加到项目中时，会自动将一个类型化数据集添加到您的项目中。 很少需要应用 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 到此数据集，因为数据已在用户的计算机上处于本地。 有关详细信息，请参阅 [缓存数据](../vsto/caching-data.md)。

## <a name="see-also"></a>另请参阅
- [将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [如何：用数据库中的数据填充文档](../vsto/how-to-populate-documents-with-data-from-a-database.md)
- [如何：使用主机控件中的数据更新数据源](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
- [缓存数据](../vsto/caching-data.md)
