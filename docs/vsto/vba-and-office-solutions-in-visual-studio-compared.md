---
title: Visual Studio 中的 VBA 和 Office 解决方案比较
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- VBA code, managed code extensions
- managed code extensions [Office development in Visual Studio], VBA compared to
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 24e7d3674712a17d940b94637db808c0d91d2d6a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62982126"
---
# <a name="vba-and-office-solutions-in-visual-studio-compared"></a>Visual Studio 中的 VBA 和 Office 解决方案比较
  Microsoft Visual Basic for Applications (VBA) 使用与 Office 应用程序紧密集成的非托管代码。 你可以通过使用 Visual Studio 创建 Microsoft Office 项目以便充分利用 .NET Framework 和 Visual Studio 设计工具。

 有关可以使用 Visual Studio 创建的 Office 解决方案的类型的信息，请参阅 [office 解决方案开发概述 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)。

## <a name="comparison"></a>比较
 下表提供了 VBA 解决方案和 Visual Studio 中的 Office 解决方案之间的基本比较。

|VBA 解决方案|Visual Studio 中的 Office 解决方案|
|-------------------|---------------------------------------|
|使用已连接到特定文档并随之保留的代码。|使用与文档级自定义项的文档 (分开存储的代码) ，或在应用程序 (为 VSTO 外) 接程序加载的程序集中存储代码。|
|使用 Office 对象模型和 VBA API。|提供对 Office 对象模型和 [!INCLUDE[dnprdnshort](../sharepoint/includes/dnprdnshort-md.md)] API 的访问权限。|
|专为宏录制而设计，具有更简洁的开发人员体验。|专为安全性、更轻松的代码维护和使用完整的 Visual Studio 集成开发环境 (IDE) 的能力而设计。|
|适用于通过与 Office 应用程序紧密集成而受益的解决方案。|适用于从 Visual Studio 和 [!INCLUDE[dnprdnshort](../sharepoint/includes/dnprdnshort-md.md)]的完整资源中受益的解决方案。|
|具有针对企业的限制，尤其是在安全性和部署方面。|设计用于企业中。|

 使用 VBA 执行某些操作仍可更轻松地快速完成。 具体而言，以下操作可能适合继续使用 VBA：

- 自定义工作表函数。

- 宏录制。

## <a name="combine-vba-solutions-and-office-solutions-created-by-using-visual-studio"></a>结合使用 Visual Studio 创建的 VBA 解决方案和 Office 解决方案
 可以从使用 Visual Studio 创建的 Office 解决方案中调用 VBA 代码，也可以从 VBA 调用使用 Visual Studio 创建的 Office 解决方案中的代码。 特定方法根据 Office 解决方案是 VSTO 外接程序还是文档级自定义项而有所不同。 有关详细信息，请参阅 [从其他 Office 解决方案调用 VSTO 外接程序中的代码](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md) 和 [组合 VBA 和文档级自定义项](../vsto/combining-vba-and-document-level-customizations.md)。

## <a name="see-also"></a>另请参阅
- [Office 解决方案开发概述 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [从其他 Office 解决方案调用 VSTO 外接程序中的代码](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md)
- [合并 VBA 和文档级自定义项](../vsto/combining-vba-and-document-level-customizations.md)
- [文档级自定义项的体系结构](../vsto/architecture-of-document-level-customizations.md)
- [Architecture of VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md)
- [保护 Office 解决方案](../vsto/securing-office-solutions.md)
- [开始 &#40;Visual Studio 中的 Office 开发&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
