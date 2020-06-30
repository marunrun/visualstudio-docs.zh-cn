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
ms.openlocfilehash: 3eebefeab6b78955b03d4546a60dd811f5e9ae4e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547649"
---
# <a name="supported-visual-studio-editions-for-visualization-amp-modeling-sdk"></a>支持的 Visual Studio 版本的可视化 &amp; 建模 SDK
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

以下是 [!INCLUDE[dsl](../includes/dsl-md.md)] 在创作和部署环境中支持的 Visual Studio 版本的列表。 有关这些版本的详细信息，请参阅 Microsoft [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] [开发人员中心](https://msdn.microsoft.com/vstudio/products/)。

## <a name="authoring-edition"></a>创作版
 若要定义 DSL，必须安装以下组件：

|Products|下载链接|
|-|-|
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]|[https://www.visualstudio.com/](https://www.visualstudio.com/)|
|[!INCLUDE[vssdk_current_short](../includes/vssdk-current-short-md.md)]|[Visual Studio SDK](../extensibility/visual-studio-sdk.md)|
|Visual Studio 可视化和建模 SDK|[建模 SDK 下载](https://www.microsoft.com/download/details.aspx?id=48148)|
## <a name="deployment-editions"></a>部署版
 [!INCLUDE[dsl](../includes/dsl-md.md)]支持以下配置以部署生成的域特定语言：

- Visual Studio Enterprise

- Visual Studio Professional

- Visual Studio Shell（集成模式）可再发行组件包

- Visual Studio Shell（独立模式）可再发行组件包

> [!NOTE]
> 若要使 DSL 能够在 Shell 产品上运行，必须在扩展清单中设置**支持的 VS Edition**字段。 有关详细信息，请参阅[部署域特定语言解决方案](../modeling/deploying-domain-specific-language-solutions.md)。

## <a name="see-also"></a>另请参阅
 [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
