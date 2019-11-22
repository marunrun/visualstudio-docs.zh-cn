---
title: Install a UML profile | Microsoft Docs
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
ms.openlocfilehash: 14911cda4cfc2be5fece6005a879427c10529bbc
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74298914"
---
# <a name="install-a-uml-profile"></a>安装 UML 配置文件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以使用 UML 配置文件来扩展 Visual Studio。 使用配置文件可以向在 UML 模型中创建的元素添加构造型及其他属性。 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

 收到使用配置文件创建的 UML 模型时，除非你安装相同配置文件，否则将不会显示某些属性。

 在 Visual Studio 扩展内部分发配置文件。 扩展还可能包含其他功能，如菜单命令。 For more information, see [Managing Visual Studio Extensions](https://go.microsoft.com/fwlink/?LinkId=160728).

### <a name="to-install-a-uml-profile-on-your-computer"></a>在计算机上安装 UML 配置文件

1. 应以 Visual Studio 扩展 (`.vsix`) 文件的形式向你提供了该配置文件。 同一文件中可能有其他功能。

     将 `.vsix` 文件移到计算机上方便的位置。

2. 在 Windows 资源管理器（或文件资源管理器）中双击 `.vsix` 文件，或在 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 中打开它。

3. Click **Install** in the dialog box that appears.

4. To uninstall or temporarily disable the extension, open **Extension Manager** from the **Tools** menu.

### <a name="to-uninstall-or-disable-a-profile-extension"></a>卸载或禁用配置文件扩展

1. On the Visual Studio **Tools** menu, click **Extension Manager**.

2. Click the extension that you want to remove, and then click **Disable** or **Uninstall**.

## <a name="see-also"></a>请参阅
 [Customize your model with profiles and stereotypes](../modeling/customize-your-model-with-profiles-and-stereotypes.md) [Define a profile to extend UML](../modeling/define-a-profile-to-extend-uml.md)
