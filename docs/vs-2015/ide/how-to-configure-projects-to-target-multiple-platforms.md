---
title: 如何：将项目配置为面向多个平台 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio], targeting platforms
- platforms, changing target platforms
ms.assetid: affa2392-7aed-45ac-9ffa-1d8e0496d590
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: bb759faff99b641f24df87f73bc1d3d52b6635cc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72663560"
---
# <a name="how-to-configure-projects-to-target-multiple-platforms"></a>如何：将项目配置为面向多个平台
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 提供了一种能够同时面向多个不同的 CPU 体系结构或平台的解决方案。 可通过“配置管理器”对话框访问设置这些功能的属性。

## <a name="targeting-a-platform"></a>面向平台
 可通过“配置管理器”对话框创建和设置解决方案级别和项目级别的配置和平台。 每个解决方案级别的配置和目标的组合都具有唯一的一组与之相关的属性，通过这些属性可以轻松地在面向 [!INCLUDE[vcprx64](../includes/vcprx64-md.md)] 平台的发布配置、面向 x86 平台的发布配置以及面向 x86 平台的调试配置等之间进行切换。

#### <a name="to-set-your-configuration-to-target-a-different-platform"></a>将配置设置为面向不同平台

1. 在“生成”菜单上，单击“配置管理器” 。

2. 在“活动解决方案平台”框中，选择希望解决方案面向的平台，或者选择 \<New> 创建一个新平台。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 会编译应用程序，以面向在“配置管理器”对话框中被设置为活动平台的平台****。

## <a name="removing-a-platform"></a>删除平台
 如果发现不再需要某个平台，可以使用“配置管理器”对话框将其删除。 此操作会删除你为配置和目标的这个组合所配置的所有解决方案和项目设置。

#### <a name="to-remove-a-platform"></a>删除平台

1. 在“生成”菜单上，单击“配置管理器” 。

2. 在“活动解决方案平台”框中，选择 \<Edit>。 “编辑解决方案平台”对话框随即打开。

3. 单击想要删除的平台，然后单击“删除”。

## <a name="targeting-multiple-platforms-with-one-solution"></a>通过一个解决方案面向多个平台
 由于可以基于配置和平台设置的组合更改设置，因此可以设置一个面向多个平台的解决方案。

#### <a name="to-target-multiple-platforms"></a>面向多个平台

1. 使用“配置资源管理器”为解决方案添加至少两个目标平台。

2. 从“活动解决方案平台”列表中选择想要面向的平台。

3. 生成解决方案。

#### <a name="to-build-multiple-solution-configurations-at-once"></a>一次生成多个解决方案配置

1. 使用“配置资源管理器”为解决方案添加至少两个目标平台。

2. 使用“批量生成”窗口可以同时生成多个解决方案配置。

   例如，可以将解决方案级别的平台设置为 [!INCLUDE[vcprx64](../includes/vcprx64-md.md)]，并使该解决方案中项目都不面向该平台。 解决方案中可以存在多个项目，并且每个项目面向不同的平台。 如果具有此类解决方案，建议创建一个新的配置并使用描述性名称命名，以免混淆。

## <a name="see-also"></a>另请参阅
 [如何：创建和编辑配置](../ide/how-to-create-and-edit-configurations.md)[了解生成配置](../ide/understanding-build-configurations.md)[在 Visual Studio 中生成和清理项目和解决方案](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)
