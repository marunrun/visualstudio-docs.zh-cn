---
title: 部署项目类型 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], managed-code
- projects [Visual Studio SDK], aggregator
ms.assetid: 7f132f67-8589-464c-90dc-0d57ae02aa8f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 835e85ade4d309d0b5692aa9b857476cd6b5927a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708788"
---
# <a name="deploy-project-types"></a>部署项目类型
[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]安装一个新的项目类型聚合器 *（Project聚合器2.dll*）以及用于重新分发的 Windows 安装程序包 （*ProjectAg聚合器2.msi*）。 您必须将新的聚合器用于托管代码项目类型。 ProjectAg聚合器2围绕[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]项目聚合器中阻止托管代码项目类型正常工作的限制进行工作。 以下步骤描述如何更改 VSPackage 以使用新的聚合器。

1. 从解决方案中删除本机层次结构包装器项目。

2. 从设置中删除任何本机层次结构包装二进制文件。

3. 将*Project 聚合器2.msi*添加到您的设置中。
