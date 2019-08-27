---
title: 在 Office 解决方案中的应用程序和部署清单
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- manifests [Office development in Visual Studio]
- deployment manifests [Office development in Visual Studio]
- application manifests [Office development in Visual Studio]
- assemblies [Office development in Visual Studio], updating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: d22d58eb8a2264d5c7765a15726db556c7d5569f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62942897"
---
# <a name="application-and-deployment-manifests-in-office-solutions"></a>在 Office 解决方案中的应用程序和部署清单
  应用程序清单是一个 XML 文件，该文件提供由 Office 解决方案使用的信息来定位和更新其程序集。 应用程序清单可结合部署清单一起使用，部署清单是一个存储在服务器上的 XML 文件，提供定位最新版本的应用程序清单和程序集所需的信息。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="manifest-structure-for-office-solutions"></a>Office 解决方案的清单结构
 对于通过使用 Visual Studio 中的 Office 开发工具创建的 Microsoft Office 解决方案，所有清单都基于标准的 ClickOnce 架构。 在部署 Office 解决方案时，文档级和 VSTO 外接程序项目的应用程序清单都位于 ClickOnce 缓存。 部署清单不可复制到客户端计算机。

 应用程序和 Office 项目的部署清单的内容的信息，请参阅[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)并[Office 解决方案的部署清单](../vsto/deployment-manifests-for-office-solutions.md)。

## <a name="create-application-and-deployment-manifests"></a>创建应用程序和部署清单
 应用程序清单可作为生成过程的一部分自动创建。 每次生成文档级项目时，部署清单的位置就会作为自定义文档属性嵌入到该文档。 对于 VSTO 外接程序，部署清单的位置存储在注册表中。

 有关详细信息**发布向导**，请参阅[使用 ClickOnce 部署 Office 解决方案](../vsto/deploying-an-office-solution-by-using-clickonce.md)。

 详细了解如何清单与 Office 解决方案配合使用，请参阅[部署 Office 解决方案](../vsto/deploying-an-office-solution.md)。

## <a name="see-also"></a>请参阅

- [文档级自定义项的体系结构](../vsto/architecture-of-document-level-customizations.md)
- [VSTO 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
- [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)
- [Office 解决方案的部署清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)
- [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)