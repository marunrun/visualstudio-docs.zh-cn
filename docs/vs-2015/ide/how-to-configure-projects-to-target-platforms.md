---
title: 如何：配置项目以面向目标平台 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- project settings [Visual Studio], targeting platforms
- platforms, targeting specific CPUs
- project properties [Visual Studio], targeting platforms
- projects [Visual Studio], targeting platforms
- 64-bit [Visual Studio]
- 64-bit programming [Visual Studio]
- CPUs, targeting specific
- 64-bit applications [Visual Studio]
ms.assetid: 845302fc-273d-4f81-820a-7296ce91bd76
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e6ba899fd1b17fa5a82c64d5c5e44e67f0d5eb97
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668193"
---
# <a name="how-to-configure-projects-to-target-platforms"></a>如何：配置项目以面向目标平台
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 将应用程序设置为面向不同平台（包括 64 位平台）。 若要深入了解 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中对 64 位平台的支持，请参阅 [64 位应用程序](https://msdn.microsoft.com/library/fd4026bc-2c3d-4b27-86dc-ec5e96018181)。

## <a name="targeting-platforms-with-the-configuration-manager"></a>使用配置管理器设定目标平台
 “配置管理器”  提供了一种快速添加面向项目的新平台的方法。 如果选择 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 附带的平台之一，则将修改项目属性，以便生成适用于所选平台的项目。

#### <a name="to-configure-a-project-to-target-a-64-bit-platform"></a>将项目配置为面向 64 位平台

1. 在菜单栏上，依次选择 **“生成”** 、 **“配置管理器”** 。

2. 在“活动解决方案平台”  列表中，选择一个 64 位平台作为解决方案目标，然后选择“关闭”  按钮。

   1. 如果所需平台未出现在“活动解决方案平台”  列表中，请选择“新建”  。

        将显示“新建解决方案平台”  对话框。

   2. 在“键入或选择新平台”  列表中，选择“x64”  。

       > [!NOTE]
       > 如果对配置进行了重命名，则可能需要修改“项目设计器”  中的设置，以面向正确的平台。

   3. 如果要复制当前平台配置的设置，请选择它，然后选择“确定”  按钮。

   面向 64 位平台的所有项目的属性均已更新，并将为 64 位平台优化项目的下一个生成。

## <a name="targeting-platforms-in-the-project-designer"></a>在项目设计器中设定平台目标
 项目设计器还提供使项目面向不同平台的方法。 如果在“新建解决方案平台”  对话框的列表中选择的平台之一不适合自己的解决方案，则可以创建自定义配置名称并修改“项目设计器”  中的配置以面向正确的平台。

 此任务的执行根据所用编程语言而有所不同。 有关详细信息，请参阅以下链接：

- 对于 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 项目，请参阅 [/platform (Visual Basic)](https://msdn.microsoft.com/library/f9bc61e6-e854-4ae1-87b9-d6244de23fd1)。

- 对于 [!INCLUDE[csprcs](../includes/csprcs-md.md)] 项目，请参阅[“项目设计器”->“生成”页 (C#)](../ide/reference/build-page-project-designer-csharp.md)。

- 对于 [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] 项目，请参阅 [/clr（公共语言运行时编译）](https://msdn.microsoft.com/library/fec5a8c0-40ec-484c-a213-8dec918c1d6c)。

## <a name="see-also"></a>另请参阅
 [了解生成平台](../ide/understanding-build-platforms.md) [/Platform （C#编译器选项）](https://msdn.microsoft.com/library/c290ff5e-47f4-4a85-9bb3-9c2525b0be04) [64 位应用程序](https://msdn.microsoft.com/library/fd4026bc-2c3d-4b27-86dc-ec5e96018181) [Visual Studio IDE 64-位支持](../ide/visual-studio-ide-64-bit-support.md)
