---
title: 开始使用源代码管理插件 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, getting started
- getting started, source control plug-ins
ms.assetid: 46ac1f9f-4ecc-4a72-88d3-4c7e1647e1cb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: efc21e07830614d9d3041b2d2d231fd82c652114
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708349"
---
# <a name="get-started-with-source-control-plug-ins"></a>开始使用源代码管理插件
要创建源代码管理插件，必须创建一个 DLL，该 DLL 实现源代码管理插件 API 中定义的函数，然后注册 DLL[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]使其可用于源代码版本控件。

 源代码管理插件 API 的三个版本（版本 1.1、1.2 和 1.3）可用于源代码管理插件。此处记录的源代码管理插件 API 是版本 1.3。 它设计为与支持版本 1.1 和 1.2 的源代码管理插件完全兼容。 [源代码管理插件 API 版本 1.3 部分中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-3.md)详细介绍了源代码管理插件 API 的最新版本中支持的新功能。

## <a name="in-this-section"></a>在本节中
- [如何：安装源代码管理插件](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)

 描述如何使注册表项插入源代码管理 DLL 所需的注册表项。

- [源代码管理插件 API 版本 1.3 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-3.md)

 简要概述对版本 1.3 中的源代码管理插件 API 所做的更改。

- [源代码管理插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)

 简要概述对版本 1.2 中的源代码管理插件 API 所做的更改。

## <a name="related-sections"></a>相关章节
- [源代码管理插件](../../extensibility/source-control-plug-ins.md)

 提供源代码管理插件 API 中所有元素的完整列表。

- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)

 定义源代码管理插件 SDK 并描述包含的资源。
