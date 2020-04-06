---
title: 源代码管理插件测试指南 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: e6b3f8e76e977472a3459697a650b32dae657c22
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704379"
---
# <a name="test-guide-for-source-control-plug-ins"></a>源代码管理插件的测试指南
本节提供有关使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]测试源代码管理插件的指导。 提供了最常见的测试区域以及一些可能有问题的更复杂的区域的广泛概述。 此概述并非详尽无遗地列出了测试用例。

> [!NOTE]
> 某些错误修复和对最新[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE 的改进可能会发现现有源代码管理插件的问题，这些问题以前在使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的早期版本时未遇到。 强烈建议您测试现有源代码管理插件本节中列举的区域，即使自以前的版本以来未对插件进行任何更改[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

## <a name="common-preparation"></a>常见准备
 需要安装具有[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]和目标源控制插件的计算机。 第二台计算机类似配置，可用于某些开源控制测试。

## <a name="definition-of-terms"></a>术语的定义
 在本测试指南中，请使用以下术语定义：

 客户端项目 支持源代码管理集成[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的任何可用项目类型（例如 ， [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)][!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]或[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]。

 Web 项目有四种类型的 Web 项目：文件系统、本地 IIS、远程站点和 FTP。

- 文件系统项目是在本地路径上创建的，但它们不需要安装 Internet 信息服务 （IIS），因为它们是通过 UNC 路径在内部访问的，并且可以从 IDE 内部置于源代码管理之下，就像客户端项目一样。

- 本地 IIS 项目使用安装在同一台计算机上的 IIS，并且使用指向本地计算机的 URL 进行访问。

- 远程站点项目也根据 IIS 服务创建，但它们被置于 IIS 服务器计算机上的源代码管理之下，而不是从[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE 内部。

- FTP 项目通过远程 FTP 服务器访问，但不能置于源代码管理之下。

  登记源代码管理下的解决方案或项目的另一个术语。

  版本存储 正在通过源代码管理插件 API 访问的源代码管理数据库。

## <a name="test-areas-covered-in-this-section"></a>本节涵盖的测试区域

- [测试区域 1：从源代码管理添加/打开](../../extensibility/internals/test-area-1-add-to-open-from-source-control.md)

  - 案例 1a：向源代码管理添加解决方案

  - 案例 1b：源代码管理的开放解决方案

  - 案例 1c：从源代码管理添加解决方案

- [测试区域 2：从源代码管理获取](../../extensibility/internals/test-area-2-get-from-source-control.md)

- [测试区域 3：签出/撤消签出](../../extensibility/internals/test-area-3-check-out-undo-checkout.md)

  - 案例 3：签出/撤消签出

  - 案例 3a：签出

  - 案例 3b：已断开连接结帐

  - 案例 3c：查询编辑/查询保存 （QEQS）

  - 案例 3d：静默结帐

  - 案例 3e：撤消签出

- [测试区域 4：签入](../../extensibility/internals/test-area-4-check-in.md)

  - 案例 4a：修改的项目

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

## <a name="see-also"></a>请参阅
- [源代码管理插件](../../extensibility/source-control-plug-ins.md)
