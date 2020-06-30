---
title: 非托管 API 参考（Visual Studio 中的 Office 开发）
ms.date: 08/14/2019
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, reference
- Office development in Visual Studio, unmanaged API reference
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4c1616d24ae9b2c072df4e5708eb98e86611a83d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540980"
---
# <a name="unmanaged-api-reference-office-development-in-visual-studio"></a>非托管 API 参考（Visual Studio 中的 Office 开发）

从 2007 Microsoft Office 系统开始，Office 应用程序使用[IManagedAddin 接口](../vsto/imanagedaddin-interface.md)接口调入包含在中的 VSTO 外接程序加载程序组件 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。 此组件用于帮助加载托管 VSTO 外接程序。可以通过实现此接口来创建自己的 VSTO 外接程序加载程序组件。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="in-this-section"></a>本节内容

[IManagedAddin 接口](../vsto/imanagedaddin-interface.md)

一种 COM 接口，可以通过实现该接口来在 Office 应用程序中加载和卸载 VSTO 托管外接程序。
