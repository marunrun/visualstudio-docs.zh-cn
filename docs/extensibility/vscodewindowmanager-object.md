---
title: VSCodeWindowManager 对象 |Microsoft Docs
description: 了解 VSCodeWindowManager 对象，该对象负责管理修饰，例如下拉栏。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 7a5c602a1cf46382e5a8b5c688501b2406e4a6d0
ms.sourcegitcommit: dd96a95d87a039525aac86abe689c30e2073ae87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2021
ms.locfileid: "97863989"
---
# <a name="vscodewindowmanager-object"></a>VSCodeWindowManager 对象

语言服务实现代码窗口管理器，负责管理修饰 (例如，下拉栏) 。 有关详细信息，请参阅 [使用旧版 API 自定义代码窗口](/previous-versions/visualstudio/visual-studio-2015/extensibility/customizing-code-windows-by-using-the-legacy-api?preserve-view=true&view=vs-2015)。

下表显示了对象中的接口 `VSCodeWindowManager` 。

|接口|说明|
|---------------|-----------------|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|允许在代码窗口中添加或删除修饰 (例如下拉栏) 。|