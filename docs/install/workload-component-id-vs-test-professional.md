---
title: Visual Studio Test Professional 工作负载和组件 ID
titleSuffix: ''
description: 使用 Visual Studio 工作负载和组件 ID 为技术全面的测试人员提供集成的测试工具
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.date: 03/16/2020
ms.topic: reference
helpviewer_keywords:
- workload ID, Visual Studio
- component ID, Visual Studio
- install Visual Studio, administrator guide
ms.assetid: 70c03438-8434-4921-ada0-c172519af431
ms.prod: visual-studio-windows
ms.technology: vs-installation
monikerRange: vs-2017
ms.openlocfilehash: ececc1815ebc578076d059b00ade1a5fde4552a4
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "79437334"
---
# <a name="visual-studio-test-professional-component-directory"></a>Visual Studio Test Professional 组件目录

本页的表中列出了可用于通过使用命令行安装 Visual Studio 或可指定为 VSIX 清单中的依赖项的 ID。 请注意，我们将在发布 Visual Studio 更新时添加其他组件。

另请注意以下有关本页的注意事项：

* 每个工作负载均有其自己的部分，后跟工作负载 ID 和适用于工作负载的组件表格。
* 默认情况下，安装工作负载时将安装**必需**组件。
* 如果愿意，还可以安装**推荐**和**可选**组件。
* 我们还添加了一个部分，此部分列出了不属于任何工作负载的其他组件。

在 VSIX 清单中设置依赖项时，必须仅指定组件 ID。 使用本页中的表格来确定最小组件依赖项。 在某些情况下，这可能意味着仅从工作负载指定一个组件。 在其他情况下，这可能意味着你从单个工作负载指定多个组件或从多个工作负载指定多个组件。 有关详细信息，请参阅[如何：将扩展性项目迁移到 Visual Studio 2017](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md) 页。

有关如何使用这些 ID 的详细信息，请参阅[使用命令行参数安装 Visual Studio 2017](use-command-line-parameters-to-install-visual-studio.md) 页。 另外，有关其他产品的工作负载和组件 ID 的列表，请参阅 [Visual Studio 2017 工作负载和组件 ID](workload-and-component-ids.md) 页。

## <a name="test-professional"></a>Test Professional

**ID：** Microsoft.VisualStudio.Workload.TestProfessional

**说明：** Test Professional 面向技术全面的测试人员提供集成的测试工具，这可帮助他们促进整个测试生存期的测试需求。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | 名称 | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.VisualStudio.Component.TestTools.FeedbackClient | Microsoft Feedback Client | 15.6.27406.0 | 必需
Microsoft.VisualStudio.Component.TestTools.MicrosoftTestManager | Microsoft 测试管理器 | 15.6.27406.0 | 必需

## <a name="unaffiliated-components"></a>独立组件

这些组件不随附于任何工作负载，但可选择作为单个组件。

组件 ID | 名称 | Version
--- | --- | ---
n/a | n/a | n/a

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>另请参阅

* [Visual Studio 工作负荷和组件 ID](workload-and-component-ids.md)
* [Visual Studio 管理员指南](visual-studio-administrator-guide.md)
* [使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
  * [命令行参数示例](command-line-parameter-examples.md)
* [创建 Visual Studio 的脱机安装](create-an-offline-installation-of-visual-studio.md)
