---
title: 源代码管理插件的测试指南 | Microsoft Docs
description: 了解如何使用 Visual Studio 测试源代码管理插件。 此概述包括常见的测试区域。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: overview
helpviewer_keywords:
- plug-ins, source control
- source control [Visual Studio SDK], testing plug-ins
- tests, source control plug-ins
- testing, source control plug-ins
- source control plug-ins, test guide
ms.assetid: 13b74765-0b7c-418e-8cd9-5f2e8db51ae5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a288beb618b0b539f53270928366349f47aee9e9
ms.sourcegitcommit: 19061b61759ce8e3b083a0e01a858e5435580b3e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97487720"
---
# <a name="test-guide-for-source-control-plug-ins"></a>源代码管理插件的测试指南
本节提供使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 测试源代码管理插件的指南。 概述性介绍了最常见的测试区域以及可能存在问题的一些更复杂的区域。 此概述并未提供测试用例的详尽列表。

> [!NOTE]
> 在针对最新 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 的一些 bug 修复和改进过程中，可能会发现以前在使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的早期版本时没有遇到过的现有源代码管理插件问题。 强烈建议针对本节中枚举的区域，测试现有的源代码管理插件，即使自 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的早期版本以来未对插件进行任何更改。

## <a name="common-preparation"></a>常规准备
 需要一台装有 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 和目标源代码管理插件的计算机。 另一台类似配置的计算机，可用于某些“在源代码管理中打开”测试。

## <a name="definition-of-terms"></a>术语的定义
 出于本测试指南的目的，指南使用以下术语定义：

 客户端项目：[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中支持源代码管理集成的任何可用项目类型（如 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]、[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 或 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]）。

 Web 项目：有四种类型的 Web 项目：文件系统、本地 IIS、远程站点和 FTP。

- 文件系统项目是在本地路径上创建的，但它们不需要安装 Internet Information Services (IIS)，因为它们是通过 UNC 路径在内部进行访问的，并且可以从 IDE 内部将其置于源代码管理之下，这与客户端项目非常相似。

- 本地 IIS 项目可与安装在同一台计算机上的 IIS 协同运作，并且可以通过指向本地计算机的 URL 进行访问。

- 远程站点项目也在 IIS 服务下创建，但它们处于 IIS 服务器计算机上的源代码管理下，而不是 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 内的源代码管理下。

- FTP 项目可以通过远程 FTP 服务器访问，但不能将其置于源代码管理之下。

  登记 - 源代码管理下的解决方案或项目的另一个术语。

  版本存储 - 正在通过源代码管理插件 API 访问的源代码管理数据库。

## <a name="test-areas-covered-in-this-section"></a>本部分涵盖的测试区域

- [测试区域 1：添加到源代码管理/从源代码管理打开](../../extensibility/internals/test-area-1-add-to-open-from-source-control.md)

  - 案例 1a：将解决方案添加到源代码管理中

  - 案例 1b：从源代码管理打开解决方案

  - 案例 1c：从源代码管理添加解决方案

- [测试区域 2：从源代码管理获取](../../extensibility/internals/test-area-2-get-from-source-control.md)

- [测试区域 3：签出/撤消签出](../../extensibility/internals/test-area-3-check-out-undo-checkout.md)

  - 事例 3：签出/撤消签出

  - 案例 3a：签出

  - 案例 3b：断开连接签出

  - 案例 3c：查询编辑/查询保存 (QEQS)

  - 案例 3d：无提示签出

  - 案例 3e：撤消签出

- [测试区域 4：签入](../../extensibility/internals/test-area-4-check-in.md)

  - 案例 4a：修改项

  - 案例 4b：添加文件

  - 案例 4c：添加项目

- [测试区域 5：更改源代码管理](../../extensibility/internals/test-area-5-change-source-control.md)

  - 案例 5a：绑定

  - 案例 5b：取消绑定

  - 案例 5c：重新绑定

- [测试区域 6：删除](../../extensibility/internals/test-area-6-delete.md)

- [测试区域 7：共享](../../extensibility/internals/test-area-7-share.md)

- [测试区域 8：插件切换](../../extensibility/internals/test-area-8-plug-in-switching.md)

  - 案例 8a：自动更改

  - 案例 8b：基于解决方案的更改

## <a name="see-also"></a>另请参阅
- [源代码管理插件](../../extensibility/source-control-plug-ins.md)
