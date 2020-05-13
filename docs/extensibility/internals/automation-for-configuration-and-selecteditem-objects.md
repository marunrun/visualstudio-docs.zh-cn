---
title: 配置和选定项目对象的自动化 |微软文档
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
ms.openlocfilehash: 0341cdf56b32b8b1ac77104b3f3e813ae0610767
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709970"
---
# <a name="automation-for-configuration-and-selecteditem-objects"></a>配置和选定项目的自动化

您可以在可视化工作室中自动执行生成和选定项目进程。

## <a name="automation-for-builds"></a>生成自动化

生成或配置具有实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider>时提供的自动化模型。 有关详细信息，请参阅[了解生成配置](../../ide/understanding-build-configurations.md)。

如果创建 VSPackage 并希望控制配置选项，则必须使用自动化模型。

## <a name="automation-for-selecteditem"></a>选定项目的自动化

您不必为对象提供实现，`SelectedItem`因为 Visual Studio 包含标准实现。 但是，如果您愿意，`SelectedItem`可以实现该对象。 您必须实现包含接口的对象，`SelectedItem`并将对<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A>`VSITEMID`设置为__VSHPROPID的方法的调用返回响应[。VSHPROPID_ExtSelectedItem](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_ExtSelectedItem>)。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A>
- [为自动化模型做出贡献](../../extensibility/internals/contributing-to-the-automation-model.md)
- [了解生成配置](../../ide/understanding-build-configurations.md)
