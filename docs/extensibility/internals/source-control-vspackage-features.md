---
title: 源代码管理 VSPackage 功能 |Microsoft Docs
description: 了解源代码管理 VSPackage 的功能，包括注册/选择详细信息，以及一些与源代码管理相关的主要功能。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control packages, features
ms.assetid: 26c3ffda-22b8-4345-9fb6-2883f37699aa
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8dd887488adc5813ad51c9fa2a25648e25ab4876
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2021
ms.locfileid: "97876215"
---
# <a name="source-control-vspackage-features"></a>源代码管理 VSPackage 功能
本部分介绍源代码管理 VSPackage 的各种功能。 其中概述了此类 VSPackage 的注册和选择详细信息，并讨论了三个源代码管理相关的功能：处理 Query-Edit Query-Save (QEQS) 事件、符号替换和自定义用户界面 (UI) 用于源代码管理函数。

## <a name="in-this-section"></a>本节内容
- [注册和选择](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)

 介绍包注册和选择机制。

- [查询编辑查询保存](../../extensibility/internals/query-edit-query-save-source-control-vspackage.md)

 说明 Query-Edit Query-Save 事件的角色，以及源代码管理 VSPackage 如何处理这些事件。

- [图形控件](../../extensibility/internals/glyph-control-source-control-vspackage.md)

 介绍标志符号控件的级别以及如何实现它们。

- [自定义用户界面](../../extensibility/internals/custom-user-interface-source-control-vspackage.md)

 概述源代码管理 VSPackage 可以指定的 UI 元素。

## <a name="related-sections"></a>相关章节
- [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)

 讨论如何创建一个源代码管理 VSPackage，该控件不仅提供源代码管理功能，还可用于自定义 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 源代码管理 UI。
