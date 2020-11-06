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
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e88885d339e55b7c3df1312b4a72c59d2959bbcc
ms.sourcegitcommit: ba966327498a0f67d2df2291c60b62312f40d1d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2020
ms.locfileid: "93414340"
---
# <a name="vscodewindowmanager-object"></a>VSCodeWindowManager 对象

语言服务实现代码窗口管理器，负责管理修饰 (例如，下拉栏) 。 有关详细信息，请参阅 [使用旧版 API 自定义代码窗口](/previous-versions/visualstudio/visual-studio-2015/extensibility/customizing-code-windows-by-using-the-legacy-api?preserve-view=true&view=vs-2015)。

下表显示了对象中的接口 `VSCodeWindowManager` 。

|接口|说明|
|---------------|-----------------|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|允许在代码窗口中添加或删除修饰 (例如下拉栏) 。|