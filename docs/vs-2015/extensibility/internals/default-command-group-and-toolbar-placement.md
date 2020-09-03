---
title: 默认命令、组和工具栏位置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands [Visual Studio], default groups
- toolbars [Visual Studio], default
- commands [Visual Studio], default editor
- command groups
- commands [Visual Studio], default IDE
- commands [Visual Studio], default product
ms.assetid: 35342110-d639-4577-8367-00b21dcc6f07
caps.latest.revision: 31
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a7fc877332f7db7b27c4a30c23f1ac395a4fc22e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196893"
---
# <a name="default-command-group-and-toolbar-placement"></a>默认命令、组和工具栏位置
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

对于产品一致性和稳定性，UI 默认显示特定的命令组，并 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 提供命令和命令组的定义。 Vspackage 还可以使用标准命令和命令组。  
  
 默认命令组分为三个类别： IDE 命令、产品命令和编辑器命令。  
  
## <a name="default-ide-commands"></a>默认 IDE 命令  
 默认 IDE 工具栏包括中包含的所有产品共享的命令 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 其中包括与常规项目操作相关的命令，如 " **保存** " 命令和 " **添加项** " 命令。 Vspackage 不应在此工具栏中增加或减少，但有一个例外：如果产品或 VSPackage 添加新的工具窗口，则应将该窗口添加到 " **视图** " 菜单上的可用工具窗口列表中。 新产品或 Vspackage 可以添加其工具栏。  
  
## <a name="default-product-commands"></a>默认产品命令  
 每个产品都可以为 IDE 提供其自己的默认工具栏，其中包含重要的常用命令。 不过，最好尽可能使用现有的菜单和工具栏，并根据需要使用其他特定于任务的工具栏对其进行补充。  
  
 工具栏的 "优先级" 字段决定其行位置。 如果为零，则在第3行 (第3行) ，菜单栏 (行 1) ， **标准** 工具栏 (第2行) 。 因此，其他工具栏出现在 " (优先级 + 3") 行。 如果有空间，后续工具栏会置于同一行;否则，它们会自动移动到下一行。  
  
## <a name="default-editor-commands"></a>默认编辑器命令  
 提供自定义编辑器的 VSPackage 应提供一个默认工具栏，其中包含该编辑器中最重要和最常用的命令。 编辑器处于活动状态时应显示编辑器工具栏，当编辑器处于非活动状态时应隐藏编辑器工具栏。 此可见性是在 .vsct 文件的中控制的 `VisibilityConstraints Element` 。  
  
 编辑器工具栏应放置在 IDE 和 product 工具栏下方。  
  
## <a name="see-also"></a>另请参阅  
 [IDE 定义的命令、菜单和组](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)   
 [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
