---
title: VSCodeWindowManager 对象 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSCodeWindowManager
helpviewer_keywords:
- VsCodeWindowManager object
- views [Visual Studio SDK], VSCodeWindowManager object
ms.assetid: e313add5-afdb-4d8d-abd1-764e1fc10c44
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c67fb719c6ec87e7707a406e2e7f67cd71569b39
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73189033"
---
# <a name="vscodewindowmanager-object"></a>VSCodeWindowManager 对象

语言服务实现代码窗口管理器，负责管理修饰（例如，下拉栏）。 有关详细信息，请参阅[使用旧版 API 自定义代码窗口](/visualstudio/extensibility/customizing-code-windows-by-using-the-legacy-api?view=vs-2015)。

下表显示 `VSCodeWindowManager` 对象中的接口。

|接口|描述|
|---------------|-----------------|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|允许在代码窗口中添加或移除修饰（如下拉栏）。|