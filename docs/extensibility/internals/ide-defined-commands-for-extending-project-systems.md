---
title: IDE 定义的用于扩展项目系统的命令 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, project systems
- project systems, environment-defined commands
ms.assetid: 0e33b8e9-16fa-4400-a941-e92d56120e7e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1c8be1cff099a713413957cfa5f8b3f383ca4bae
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73186333"
---
# <a name="ide-defined-commands-for-extending-project-systems"></a>用于扩展项目系统的 IDE 定义的命令
要扩展项目系统时，可以使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 提供的命令和命令组。

 以下部分列出了对扩展项目系统特别有用的命令项。

## <a name="command-menus"></a>命令菜单
 下表显示了可用于放置调用项目扩展程序的高级命令的有用位置的命令菜单。

|命令菜单|描述|
|------------------|-----------------|
|IDM_VS_MENU_PROJECT|**项目**顶级菜单。|
|IDM_VS_TOOL_PROJWIN|**解决方案资源管理器**工具栏。|

## <a name="shortcut-menus"></a>快捷菜单
 下表显示了在**解决方案资源管理器**中选择单个节点时或**解决方案资源管理器**中存在多个同源选项时应用的快捷菜单，这是所有选定节点的类型相同。

|快捷菜单|描述|
|-------------------|-----------------|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_PROJNODE>|在选择项目节点时应用。|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_ITEMNODE>|在选定文件时应用。|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_FOLDERNODE>|选择文件夹时应用。|
|IDM_VS_CTXT_WEBREFFOLDER|当选中 "Web 引用" 文件夹时应用。|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_REFERENCEROOT>|当选择了引用名为 "引用" 的根节点时应用。|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_REFERENCE>|当引用节点处于选定状态时应用;它们仅包括程序集、COM 和项目引用。 不包含 Web 引用。|

 下表显示了在**解决方案资源管理器**中的选定内容跨越多个层次结构时适用的快捷菜单。

|快捷菜单|描述|
|-------------------|-----------------|
|IDM_VS_CTXT_XPROJ_SLNPROJ|当当前所选内容包含 "解决方案" 节点和 "根项目" 节点时应用。|
|IDM_VS_CTXT_XPROJ_SLNITEM|在当前所选内容包含解决方案节点和项目项时应用。|
|IDM_VS_CTXT_XPROJ_MULTIPROJ|当当前选择仅包含多个根项目节点时应用。|
|IDM_VS_CTXT_XPROJ_PROJITEM|当当前选定内容包含混合的根项目节点和项目项时应用。 此外，选择可能包含 "解决方案" 节点。|
|IDM_VS_CTXT_XPROJ_MULTIITEM|当当前所选内容包含解决方案中多个项目的项目项时，或在同一项目中选择了不同类型的项时，应用。|

## <a name="command-groups"></a>命令组
 下表显示了可以在扩展项目时使用的命令组，以及可通过 <xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_PROJNODE> 快捷菜单访问的命令组。

|命令组|描述|
|-------------------|-----------------|
|IDG_VS_CTXT_PROJECT_BUILD|用于生成、重新生成和部署项目的命令。|
|IDG_VS_CTXT_COMPILELINK|用于编译和链接项目的命令。|
|IDG_VS_CTXT_PROJECT_CONFIG|用于设置项目配置和生成顺序的命令。|
|IDG_VS_CTXT_PROJECT_ADD|向项目添加项的命令。|
|IDG_VS_CTXT_PROJECT_START|用于设置与 F5 键关联的启动项目的命令。|
|IDG_VS_CTXT_PROJECT_SAVE|用于保存项目项的命令。|
|IDG_VS_CTXT_PROJECT_DEBUG|用于调试的命令。|
|IDG_VS_CTXT_PROJECT_SCC|源代码管理命令。|
|IDG_VS_CTXT_PROJECT_TRANSFER|用于剪切、复制和粘贴操作的命令。|
|IDG_VS_CTXT_PROJECT_PROPERTIES|提供对 "**项目属性**" 对话框的访问的命令。|

## <a name="see-also"></a>请参阅

- [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [创建可重复使用的按钮组](../../extensibility/creating-reusable-groups-of-buttons.md)