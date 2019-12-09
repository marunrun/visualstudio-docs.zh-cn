---
title: 支持可视化和建模 SDK 的 Visual Studio 版本 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools, supported Visual Studio editions
ms.assetid: 7c313ba0-031d-45b8-8220-eead61754747
caps.latest.revision: 29
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b81aaba14acc2c050a770e810c57e99ee43c2ab3
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74298151"
---
# <a name="supported-visual-studio-editions-for-visualization-amp-modeling-sdk"></a>支持可视化 &amp; 建模 SDK 的 Visual Studio 版本
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

以下是在创作和部署环境中 [!INCLUDE[dsl](../includes/dsl-md.md)] 支持的 Visual Studio 版本的列表。 有关这些版本的详细信息，请参阅 Microsoft [!INCLUDE[vsprvs](../includes/vsprvs-md.md)][开发人员中心](https://go.microsoft.com/fwlink/?LinkId=75628)。

## <a name="authoring-edition"></a>创作版
 若要定义 DSL，必须安装以下组件：

|||
|-|-|
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]|[http://go.microsoft.com/fwlink/?LinkId=185579](https://go.microsoft.com/fwlink/?LinkId=185579)|
|Visual Studio SDK|[http://go.microsoft.com/fwlink/?LinkId=185580](https://go.microsoft.com/fwlink/?LinkId=185580)|
|Visual Studio 可视化和建模 SDK|[http://go.microsoft.com/fwlink/?LinkID=186128](https://go.microsoft.com/fwlink/?LinkID=186128)|

## <a name="deployment-editions"></a>部署版
 [!INCLUDE[dsl](../includes/dsl-md.md)] 支持以下配置以部署生成的域特定语言：

- Visual Studio Enterprise

- Visual Studio Professional

- Visual Studio Shell （集成模式） 可再发行组件包可再发行组件包

- Visual Studio Shell（独立模式）可再发行组件包

> [!NOTE]
> 若要使 DSL 能够在 Shell 产品上运行，必须在扩展清单中设置**支持的 VS Edition**字段。 有关详细信息，请参阅[部署域特定语言解决方案](../modeling/deploying-domain-specific-language-solutions.md)。

## <a name="see-also"></a>请参阅
 [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
