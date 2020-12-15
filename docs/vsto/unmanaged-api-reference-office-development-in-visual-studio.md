---
title: 'Visual Studio 中的 Office 开发 (非托管 API 参考) '
description: 非托管 API 参考用于帮助加载托管 VSTO 外接程序。还可以通过实现此接口来创建自己的 VSTO 外接程序加载程序组件。
ms.custom: SEO-VS-2020
titleSuffix: ''
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
ms.openlocfilehash: 9dbb64b54d9b0dd9a244d9a614fbce211d1edfc5
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97522690"
---
# <a name="unmanaged-api-reference-office-development-in-visual-studio"></a>Visual Studio 中的 Office 开发 (非托管 API 参考) 

从 2007 Microsoft Office 系统开始，Office 应用程序使用 [IManagedAddin 接口](../vsto/imanagedaddin-interface.md) 接口调入包含在中的 VSTO 外接程序加载程序组件 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。 此组件用于帮助加载托管 VSTO 外接程序。可以通过实现此接口来创建自己的 VSTO 外接程序加载程序组件。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="in-this-section"></a>在本节中

[IManagedAddin 接口](../vsto/imanagedaddin-interface.md)

一种 COM 接口，可以通过实现该接口来在 Office 应用程序中加载和卸载 VSTO 托管外接程序。
