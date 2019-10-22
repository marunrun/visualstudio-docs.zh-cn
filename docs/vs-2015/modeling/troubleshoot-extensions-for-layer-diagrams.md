---
title: 层关系图扩展疑难解答 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: troubleshooting
helpviewer_keywords:
- layer diagrams, extension errors
- layer diagrams, troubleshooting extensions
ms.assetid: 1fda4f8a-38b8-482b-87b8-eade1a4e5662
caps.latest.revision: 27
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: dd4560673259373b68b370e73a43de424fb7bdb7
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658472"
---
# <a name="troubleshoot-extensions-for-layer-diagrams"></a>层关系图扩展疑难解答
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题解决了你在创建层模型扩展时可能会遇到的一些问题。

#### <a name="when-i-press-f5-to-debug-my-extension-my-commands-gesture-handlers-validation-extensions-or-custom-properties-do-not-appear-on-layer-diagrams-in-the-experimental-instance-of-includevsprvsincludesvsprvs-mdmd"></a>在我按 F5 调试扩展时，我的命令、笔势处理程序、验证扩展或自定义属性没有出现在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 实验实例的层关系图上。

1. 在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的实验实例中打开扩展解决方案，然后在 "**生成**" 菜单上单击 "**重新生成解决方案**"。

2. 按**F5**或**CTRL + F5**启动 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的实验实例。 打开层关系图并测试你的扩展。

   如有必要，请继续下一个过程。

#### <a name="an-old-version-of-my-extension-runs"></a>将运行我的旧版本扩展。

1. 请确保没有 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 实验实例正在运行。

2. 删除以下文件夹：%LocalAppData%\Microsoft\VisualStudio \\ [version] \ComponentModelCache

   > [!NOTE]
   > % LocalAppData% 通常为*DriveName*： \Users \\*用户名*\appdata\local。

   如有必要，请继续下一个过程。

#### <a name="an-old-version-of-my-validation-results-appears-or-my-validation-method-is-not-called"></a>将出现旧版本的验证结果，或我的验证方法未被调用。

1. 在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的实验实例中，单击 "**生成**" 菜单上的 "**清理解决方案**"。 这将清除上一个验证分析缓存的结果。

2. 请确保你的模型中的层与代码元素关联，并且在模型中有至少一个依赖项链接。 如果不存在任何验证内容，则不会调用验证。

3. 常规断点可能在验证方法中不起作用，因为其运行于单独的进程中。 如果你想要逐步执行你的方法，就必须插入一个对 `System.Diagnostics.Debugger.Launch()` 的调用。

4. 在层验证项目的**source.extension.vsixmanifest**中，请确保已在 "**内容**" 下添加了**MEF 组件**项和**自定义扩展类型**项。

## <a name="see-also"></a>请参阅
 [扩展层关系图](../modeling/extend-layer-diagrams.md)
