---
title: 源代码管理 VSPackage 功能 |Microsoft Docs
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
ms.openlocfilehash: a01b9d8fbf5f8d0645b5245d21b05aba9e7dacea
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80705020"
---
# <a name="source-control-vspackage-features"></a>源代码管理 VSPackage 功能
本部分介绍源代码管理 VSPackage 的各种功能。 其中概述了此类 VSPackage 的注册和选择详细信息，并讨论了三个与源代码管理相关的功能：处理查询编辑查询-Save (QEQS) 事件、符号替换和自定义用户界面 (UI) 用于源代码管理函数。

## <a name="in-this-section"></a>本节内容
- [注册和选择](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)

 介绍包注册和选择机制。

- [查询编辑查询保存](../../extensibility/internals/query-edit-query-save-source-control-vspackage.md)

 说明查询编辑查询-保存事件的角色，以及源代码管理 VSPackage 如何处理这些事件。

- [图形控件](../../extensibility/internals/glyph-control-source-control-vspackage.md)

 介绍标志符号控件的级别以及如何实现它们。

- [自定义用户界面](../../extensibility/internals/custom-user-interface-source-control-vspackage.md)

 概述源代码管理 VSPackage 可以指定的 UI 元素。

## <a name="related-sections"></a>相关章节
- [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)

 讨论如何创建一个源代码管理 VSPackage，该控件不仅提供源代码管理功能，还可用于自定义 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 源代码管理 UI。
