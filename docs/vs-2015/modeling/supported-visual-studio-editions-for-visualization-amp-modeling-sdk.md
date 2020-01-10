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
ms.openlocfilehash: 0692efefcc92e3316ccf725c586fc6566b09a6ef
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75850782"
---
# <a name="supported-visual-studio-editions-for-visualization-amp-modeling-sdk"></a>支持可视化 &amp; 建模 SDK 的 Visual Studio 版本
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

以下是支持与 Visual Studio 版本的列表[!INCLUDE[dsl](../includes/dsl-md.md)]中创作和部署环境。 有关这些版本的详细信息，请参阅 Microsoft [!INCLUDE[vsprvs](../includes/vsprvs-md.md)][开发人员中心](https://msdn.microsoft.com/vstudio/products/)。

## <a name="authoring-edition"></a>创作版
 若要定义 DSL，必须安装以下组件：

|||
|-|-|
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]|[http://go.microsoft.com/fwlink/?LinkId=185579](https://www.visualstudio.com/)|
|Visual Studio SDK|[http://go.microsoft.com/fwlink/?LinkId=185580](https://docs.microsoft.com/azure/devops/integrate/index?view=azure-devops&viewFallbackFrom=vsts)|
|Visual Studio 可视化和建模 SDK|[http://go.microsoft.com/fwlink/?LinkID=186128](https://docs.microsoft.com/samples/browse/?redirectedfrom=MSDN-samples)|

## <a name="deployment-editions"></a>部署版
 [!INCLUDE[dsl](../includes/dsl-md.md)] 支持以下用于部署生成的域特定语言的配置：

- Visual Studio Enterprise

- Visual Studio Professional

- Visual Studio Shell （集成模式） 可再发行组件包可再发行组件包

- Visual Studio Shell（独立模式）可再发行组件包

> [!NOTE]
> 若要使 DSL 能够在 Shell 产品上运行，必须设置**支持的 VS 版本**字段在扩展清单中。 有关详细信息，请参阅[部署域特定语言解决方案](../modeling/deploying-domain-specific-language-solutions.md)。

## <a name="see-also"></a>请参阅
 [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
