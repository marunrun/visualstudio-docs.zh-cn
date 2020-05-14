---
title: 用于扩展项目系统的 IDE 定义命令 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, project systems
- project systems, environment-defined commands
ms.assetid: 0e33b8e9-16fa-4400-a941-e92d56120e7e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 61c0b2924548f50ad650389e3ad81759be1986a4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707736"
---
# <a name="ide-defined-commands-for-extending-project-systems"></a>用于扩展项目系统的 IDE 定义的命令
如果要扩展项目系统，可以使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE 提供的命令和命令组。

 以下各节列出了对扩展项目系统特别有用的命令项。

## <a name="command-menus"></a>命令菜单
 下表显示了用于放置调用项目扩展器的高级命令的有用位置的命令菜单。

|命令菜单|描述|
|------------------|-----------------|
|IDM_VS_MENU_PROJECT|**项目**顶级菜单。|
|IDM_VS_TOOL_PROJWIN|**解决方案资源管理器**工具栏。|

## <a name="shortcut-menus"></a>快捷菜单
 下表显示了**在解决方案资源管理器**中选择单个节点时应用的快捷菜单，或者**解决方案资源管理器**中有多个同质选择时应用的快捷菜单，即所有选定节点的类型相同时。

|快捷菜单|描述|
|-------------------|-----------------|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_PROJNODE>|在选择项目节点时应用。|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_ITEMNODE>|在选择文件时应用。|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_FOLDERNODE>|在选择文件夹时应用。|
|IDM_VS_CTXT_WEBREFFOLDER|选择 Web 参考文件夹时应用。|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_REFERENCEROOT>|当选择名为"引用"的引用根节点时应用。|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_REFERENCE>|在选择引用节点时应用;这些仅包括程序集、COM 和项目引用。 不包括 Web 引用。|

 下表显示了**解决方案资源管理器**中选区跨越多个层次结构时应用的快捷菜单，

|快捷菜单|描述|
|-------------------|-----------------|
|IDM_VS_CTXT_XPROJ_SLNPROJ|当当前选择包含解决方案节点和根项目节点时应用。|
|IDM_VS_CTXT_XPROJ_SLNITEM|当当前选择包含解决方案节点和项目项时应用。|
|IDM_VS_CTXT_XPROJ_MULTIPROJ|当当前选择仅由多个根项目节点组成时应用。|
|IDM_VS_CTXT_XPROJ_PROJITEM|当当前选择包含根项目节点和项目项的组合时，将应用。 此外，所选内容可能包含解决方案节点。|
|IDM_VS_CTXT_XPROJ_MULTIITEM|当当前选择包含解决方案中多个项目中的项目项，或者在同一项目中选择不同类型的项时，应用。|

## <a name="command-groups"></a>命令组
 下表显示了在扩展项目时可以使用的命令组，并且可以通过<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_PROJNODE>快捷菜单访问。

|命令组|描述|
|-------------------|-----------------|
|IDG_VS_CTXT_PROJECT_BUILD|用于生成、重建和部署项目的命令。|
|IDG_VS_CTXT_COMPILELINK|用于编译和链接项目的命令。|
|IDG_VS_CTXT_PROJECT_CONFIG|设置项目配置和生成顺序的命令。|
|IDG_VS_CTXT_PROJECT_ADD|向项目添加项的命令。|
|IDG_VS_CTXT_PROJECT_START|设置与 F5 密钥关联的启动项目的命令。|
|IDG_VS_CTXT_PROJECT_SAVE|用于保存项目项的命令。|
|IDG_VS_CTXT_PROJECT_DEBUG|用于调试的命令。|
|IDG_VS_CTXT_PROJECT_SCC|源控制的命令。|
|IDG_VS_CTXT_PROJECT_TRANSFER|剪切、复制和粘贴操作的命令。|
|IDG_VS_CTXT_PROJECT_PROPERTIES|提供对"**项目属性**"对话框的访问的命令。|

## <a name="see-also"></a>请参阅

- [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [创建可重复使用的按钮组](../../extensibility/creating-reusable-groups-of-buttons.md)
