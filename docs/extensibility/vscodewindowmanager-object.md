---
title: VSCode窗口管理器对象 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSCodeWindowManager
helpviewer_keywords:
- VsCodeWindowManager object
- views [Visual Studio SDK], VSCodeWindowManager object
ms.assetid: e313add5-afdb-4d8d-abd1-764e1fc10c44
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 17bc9462af55ec9621654bd39cd65a2091f3f73f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740415"
---
# <a name="vscodewindowmanager-object"></a>VSCode窗口管理器对象

语言服务实现代码窗口管理器，并负责管理修饰（例如，下拉栏）。 有关详细信息，请参阅[使用旧 API 自定义代码窗口](/visualstudio/extensibility/customizing-code-windows-by-using-the-legacy-api?view=vs-2015)。

下表显示了对象中的`VSCodeWindowManager`接口。

|接口|描述|
|---------------|-----------------|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|允许将修饰（如下拉栏）添加到代码窗口或从代码窗口中删除。|
