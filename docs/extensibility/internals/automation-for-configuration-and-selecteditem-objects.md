---
title: Configuration 和 SelectedItem 对象的自动化 |Microsoft Docs
description: 了解如何通过在 Shell 互操作中使用配置和 SelectedItem 对象自动执行 Visual Studio 生成和选定项处理。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], SelectedItem object
- automation [Visual Studio SDK], builds
ms.assetid: 120377f1-51aa-4445-b2f7-06ab7fc2b47f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5bc4b23662efe688146a7266d1b061d2d9611a45
ms.sourcegitcommit: b1b747063ce0bba63ad2558fa521b823f952ab51
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/26/2020
ms.locfileid: "96190065"
---
# <a name="automation-for-configuration-and-selecteditem-objects"></a>Configuration 和 SelectedItem 对象的自动化

你可以在 Visual Studio 中自动执行生成和选定项处理。

## <a name="automation-for-builds"></a>生成自动化

生成或配置具有实现时提供的自动化模型 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider> 。 有关详细信息，请参阅[了解生成配置](../../ide/understanding-build-configurations.md)。

如果创建 VSPackage 并想要控制配置选项，则必须使用自动化模型。

## <a name="automation-for-selecteditem"></a>SelectedItem 自动化

不需要为对象提供实现， `SelectedItem` 因为 Visual Studio 包含标准实现。 不过，您可以 `SelectedItem` 根据需要实现对象。 必须实现一个包含接口的对象 `SelectedItem` ，并返回对方法的调用的响应，并 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> `VSITEMID` 将设置为 [__VSHPROPID。VSHPROPID_ExtSelectedItem](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_ExtSelectedItem>)。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A>
- [参与自动化模型](../../extensibility/internals/contributing-to-the-automation-model.md)
- [了解生成配置](../../ide/understanding-build-configurations.md)
