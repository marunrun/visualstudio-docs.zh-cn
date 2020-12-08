---
title: 如何：安装 Office 主互操作程序集
description: 了解如何在安装 Office (Pia) 安装 Microsoft Office 主互操作程序集。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- primary interop assemblies [Office development in Visual Studio], installing
- Office primary interop assemblies, installing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 15a55650f2e4a434343c9128cc8f28117b54288e
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2020
ms.locfileid: "96845877"
---
# <a name="how-to-install-office-primary-interop-assemblies"></a>如何：安装 Office 主互操作程序集
  当你安装 Office 时，安装 Microsoft Office 主互操作程序集 (PIA)。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="to-install-the-pias-when-you-install-office"></a>安装 Office 时安装 PIA

1. 确保具有不超过 2.0 版本的 .NET Framework。

2. 安装 Microsoft Office 并确保为要扩展的应用程序选择 " **.Net 可编程性支持** " 功能 (此功能包含在默认的安装) 中。

    > [!WARNING]
    > 默认情况下，当你生成 PIA 时，PIA 嵌入到你的解决方案中，因此你不必将 Pia 分发给用户作为使用 VSTO 外接程序或自定义项的先决条件。

## <a name="see-also"></a>请参阅
- [Office 主互操作程序集](../vsto/office-primary-interop-assemblies.md)
- [如何：通过主互操作程序集面向 Office 应用程序](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)
- [如何：将计算机配置为开发 Office 解决方案](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)
- [如何：安装 Visual Studio Tools for Office 运行时可再发行组件](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)
- [Office 解决方案开发概述 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [开始 &#40;Visual Studio 中的 Office 开发&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
