---
title: 测试的源代码管理插件的指南 |Microsoft Docs
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
ms.openlocfilehash: 098aa9499dd4c1073377ed6aa5e8fa2a6fb37ca8
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67823876"
---
# <a name="test-guide-for-source-control-plug-ins"></a>源代码管理插件的测试指南
本部分提供用于测试你的源代码管理插件与指导[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 提供的最常见的测试区域，以及一些可能会出现问题的更多复杂区域的广泛概述。 本概述不应为测试用例的详尽列表。

> [!NOTE]
> 某些 bug 修复和改进到最新[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE 可能会发现与现有源控件的管理单元以前未使用的早期版本时遇到的问题[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 强烈建议测试你现有的源代码管理插件在此部分中，枚举的区域，即使以来的以前版本的插件进行任何更改[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

## <a name="common-preparation"></a>常见的准备工作
 具有计算机[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]和安装，是必需的目标源代码管理插件。 与此类似配置的第二个计算机可用于某些打开从源代码管理的测试。

## <a name="definition-of-terms"></a>术语的定义
 在本测试指南，请使用以下术语定义：

 客户端项目中可用的任何项目类型[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]支持源代码管理集成 (例如， [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]， [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]，或[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)])。

 Web 项目有以下四种类型的 Web 项目：文件系统、 本地 IIS、 远程站点和 FTP。

- 在本地路径上创建文件系统项目，但它们不需要 Internet 信息服务 (IIS)，因为它们通过 UNC 路径，在内部访问，可以将放置在从 IDE，类似于客户端项目内部的源代码管理下安装。

- 本地 IIS 项目与 IIS 配合使用的同一台计算机上安装和访问与指向本地计算机的 URL。

- 远程站点项目还会创建下一项 IIS 服务，但在 IIS 服务器计算机上而不是从源代码管理下放入内部[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE。

- FTP 项目通过远程 FTP 服务器进行访问，但不能将它们放在源代码管理下。

  登记另一种说法的解决方案或项目受源代码控制。

  版本存储区正在通过源控件插件 API 访问源代码管理数据库。

## <a name="test-areas-covered-in-this-section"></a>在本部分中介绍的测试环节

- [测试区域 1：添加到源代码管理/从源代码管理打开](../../extensibility/internals/test-area-1-add-to-open-from-source-control.md)

  - Case 1a:将解决方案添加到源代码管理

  - Case 1b:从源代码管理打开解决方案

  - 案例 1 c:从源代码管理添加解决方案

- [测试区域 2：从源代码管理获取](../../extensibility/internals/test-area-2-get-from-source-control.md)

- [测试区域 3：签出/撤消签出](../../extensibility/internals/test-area-3-check-out-undo-checkout.md)

  - 案例 3:签出/撤销签出

  - Case 3a:签出

  - Case 3b:断开连接签出

  - 案例 3 c:查询编辑/查询保存 (QEQS)

  - 本例中 3d:无提示签出

  - Case 3e:撤消签出

- [测试区域 4：签入](../../extensibility/internals/test-area-4-check-in.md)

  - Case 4a:修改的项目

  - Case 4b:添加文件

  - 用例 4 c:添加项目

- [测试区域 5：更改源代码管理](../../extensibility/internals/test-area-5-change-source-control.md)

  - Case 5a:将绑定

  - Case 5b:取消绑定

  - 用例 5 c:重新绑定

- [测试区域 6：删除](../../extensibility/internals/test-area-6-delete.md)

- [测试区域 7：共享](../../extensibility/internals/test-area-7-share.md)

- [测试区域 8：插件切换](../../extensibility/internals/test-area-8-plug-in-switching.md)

  - Case 8a:自动更改

  - Case 8b:基于解决方案的更改

## <a name="see-also"></a>请参阅
- [源代码管理插件](../../extensibility/source-control-plug-ins.md)
