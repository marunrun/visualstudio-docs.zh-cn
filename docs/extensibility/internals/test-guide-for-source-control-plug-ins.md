---
title: 源代码管理插件的测试指南 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- plug-ins, source control
- source control [Visual Studio SDK], testing plug-ins
- tests, source control plug-ins
- testing, source control plug-ins
- source control plug-ins, test guide
ms.assetid: 13b74765-0b7c-418e-8cd9-5f2e8db51ae5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 51595708bf30472fd001bde394c7d8c80e39ad45
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72722398"
---
# <a name="test-guide-for-source-control-plug-ins"></a>源代码管理插件的测试指南
本部分提供了用于测试 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的源代码管理插件的指南。 提供了最常见测试领域的全面概述，以及可能存在问题的一些更复杂的区域。 此概述并不是测试用例的详尽列表。

> [!NOTE]
> 某些 bug 修复和改进对于最新的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 可能会发现以前使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 之前未遇到的现有源代码管理插件的问题。 强烈建议您为此部分中枚举的区域测试您的现有源代码管理插件，即使自上一版本的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 以来没有对插件进行过更改。

## <a name="common-preparation"></a>常见准备
 需要安装 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 和目标源代码管理插件的计算机。 另一台配置类似的计算机可用于某些从源代码管理测试中打开的。

## <a name="definition-of-terms"></a>术语定义
 出于本测试指南的目的，请使用以下术语定义：

 客户端项目在支持源代码管理集成的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中提供的任何项目类型（例如，[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]、[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 或 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]）。

 Web 项目有四种类型的 Web 项目：文件系统、本地 IIS、远程站点和 FTP。

- 文件系统项目在本地路径上创建，但它们不需要安装 Internet Information Services （IIS），因为它们是通过 UNC 路径在内部进行访问的，并且可从 IDE 内部的源代码管理下进行管理，这与客户端项目非常类似。

- 本地 IIS 项目与安装在同一台计算机上的 IIS 一起使用，并且通过指向本地计算机的 URL 进行访问。

- 远程站点项目也在 IIS 服务下创建，但它们位于 IIS 服务器计算机上的源代码管理下，而不是位于 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 中。

- FTP 项目是通过远程 FTP 服务器访问的，但不能置于源代码管理下。

  为源代码管理下的解决方案或项目登记另一项。

  版本存储通过源代码管理插件 API 访问的源代码管理数据库。

## <a name="test-areas-covered-in-this-section"></a>本部分介绍的测试区域

- [测试区域 1：添加到源代码管理或从源代码管理打开](../../extensibility/internals/test-area-1-add-to-open-from-source-control.md)

  - 情况1a：将解决方案添加到源代码管理

  - 案例1b：从源代码管理打开解决方案

  - Case 1c：从源控件添加解决方案

- [测试区域 2：从源代码管理获取](../../extensibility/internals/test-area-2-get-from-source-control.md)

- [测试区域 3：签出/撤销签出](../../extensibility/internals/test-area-3-check-out-undo-checkout.md)

  - 案例3：签出/撤消签出

  - Case 3a：检查

  - Case 3b：断开连接签出

  - Case 3c：查询编辑/查询保存（QEQS）

  - Case 3d：缄默结帐

  - Case 3e： Undo Checkout

- [测试区域 4：签入](../../extensibility/internals/test-area-4-check-in.md)

  - Case 4a：已修改项

  - Case 4b：添加文件

  - Case 4c：添加项目

- [测试区域 5：更改源代码管理](../../extensibility/internals/test-area-5-change-source-control.md)

  - 案例5a： Bind

  - Case 5b：拆散

  - 案例5c：重新绑定

- [测试区域 6：删除](../../extensibility/internals/test-area-6-delete.md)

- [测试区域 7：共享](../../extensibility/internals/test-area-7-share.md)

- [测试区域 8：插件切换](../../extensibility/internals/test-area-8-plug-in-switching.md)

  - Case 8a：自动更改

  - Case 8b：基于解决方案的更改

## <a name="see-also"></a>请参阅
- [源代码管理插件](../../extensibility/source-control-plug-ins.md)
