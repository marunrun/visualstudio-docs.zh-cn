---
title: 安装 UML 配置文件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML - extending, profiles
ms.assetid: 586f9ba5-4d01-4a1d-b001-32e2efaa4f24
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 89531fe0f2e912a6aabd962ab56ca7a24a7f3e20
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75850655"
---
# <a name="install-a-uml-profile"></a>安装 UML 配置文件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以使用 UML 配置文件来扩展 Visual Studio。 使用配置文件可以向在 UML 模型中创建的元素添加构造型及其他属性。 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

 收到使用配置文件创建的 UML 模型时，除非你安装相同配置文件，否则将不会显示某些属性。

 在 Visual Studio 扩展内部分发配置文件。 扩展还可能包含其他功能，如菜单命令。 有关详细信息，请参阅[管理 Visual Studio 扩展](https://msdn.microsoft.com/library/dd293638(VS.100).aspx)。

### <a name="to-install-a-uml-profile-on-your-computer"></a>在计算机上安装 UML 配置文件

1. 应以 Visual Studio 扩展 (`.vsix`) 文件的形式向你提供了该配置文件。 同一文件中可能有其他功能。

     将 `.vsix` 文件移到计算机上方便的位置。

2. 在 Windows 资源管理器（或文件资源管理器）中双击 `.vsix` 文件，或在 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 中打开它。

3. 在出现的对话框中单击 "**安装**"。

4. 若要卸载或临时禁用该扩展，请从 "**工具**" 菜单打开 "**扩展管理器**"。

### <a name="to-uninstall-or-disable-a-profile-extension"></a>卸载或禁用配置文件扩展

1. 在 Visual Studio "**工具**" 菜单上，单击 "**扩展管理器**"。

2. 单击要删除的扩展，然后单击 "**禁用**" 或 "**卸载**"。

## <a name="see-also"></a>请参阅
 [使用配置文件和构造型自定义模型](../modeling/customize-your-model-with-profiles-and-stereotypes.md)[定义用于扩展 UML 的配置文件](../modeling/define-a-profile-to-extend-uml.md)
