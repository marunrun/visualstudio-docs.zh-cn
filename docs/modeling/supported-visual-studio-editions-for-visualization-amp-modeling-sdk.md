---
title: 支持可视化和建模 SDK 的 Visual Studio 版本
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools, supported Visual Studio editions
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: efe452f059d7184e1f7c87fddd6bdc6c213ece8a
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72983732"
---
# <a name="supported-visual-studio-editions-for-visualization--modeling-sdk"></a>可视化和建模 SDK 支持的 Visual Studio 版本

以下是在创作和部署环境中 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 支持的 Visual Studio 版本的列表。 有关这些版本的详细信息，请参阅 Microsoft Visual Studio[开发人员中心](https://visualstudio.microsoft.com/)。

## <a name="authoring-edition"></a>创作版

若要定义 DSL，必须安装以下组件：

|||
|-|-|
|Visual Studio|[http://go.microsoft.com/fwlink/?LinkId=185579](https://visualstudio.microsoft.com/)|
|Visual Studio SDK|[http://go.microsoft.com/fwlink/?LinkId=185580](/azure/devops/integrate/index?view=azure-devops&viewFallbackFrom=vsts)|
|Visual Studio 可视化和建模 SDK|[http://go.microsoft.com/fwlink/?LinkID=186128](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db)|

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="deployment-editions"></a>部署版

[!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 支持以下用于部署生成的域特定语言的配置：

- Visual Studio Enterprise

- Visual Studio Professional

- Visual Studio Shell （集成模式）可再发行组件包

- Visual Studio Shell（独立模式）可再发行组件包

> [!NOTE]
> 若要使 DSL 能够在 Shell 产品上运行，必须在扩展清单中设置**支持的 VS Edition**字段。 有关详细信息，请参阅[部署域特定语言解决方案](msi-and-vsix-deployment-of-a-dsl.md)。

## <a name="see-also"></a>请参阅

- [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)