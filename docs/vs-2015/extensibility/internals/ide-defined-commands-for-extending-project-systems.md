---
title: IDE 定义的命令，用于扩展项目系统 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands, project systems
- project systems, environment-defined commands
ms.assetid: 0e33b8e9-16fa-4400-a941-e92d56120e7e
caps.latest.revision: 20
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3b5de061449844b87d60d7a700b1e1c22e1e1282
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68195037"
---
# <a name="ide-defined-commands-for-extending-project-systems"></a>用于扩展项目系统的 IDE 定义的命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

当你想要扩展项目系统时，可以使用命令和命令组提供的[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]IDE。  
  
 以下部分列出用于扩展项目系统特别有用的命令项。  
  
## <a name="command-menus"></a>命令菜单  
 下表显示了是有用的位置，为你要放入调用项目扩展程序的高级命令的命令菜单。  
  
|命令菜单|描述|  
|------------------|-----------------|  
|IDM_VS_MENU_PROJECT|**项目**顶级菜单。|  
|IDM_VS_TOOL_PROJWIN|**解决方案资源管理器**工具栏。|  
  
## <a name="shortcut-menus"></a>快捷菜单  
 下表显示了应用中选择单个节点时的快捷菜单**解决方案资源管理器**，或在多个同构选择时**解决方案资源管理器**，即当所有所选的节点都属于同一类型。  
  
|快捷菜单|描述|  
|-------------------|-----------------|  
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_PROJNODE>|适用时选择的项目节点。|  
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_ITEMNODE>|适用时选择一个文件。|  
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_FOLDERNODE>|选择文件夹时适用。|  
|IDM_VS_CTXT_WEBREFFOLDER|适用时选择的 Web 引用文件夹。|  
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_REFERENCEROOT>|适用时选择名为"引用"的引用根节点。|  
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_REFERENCE>|适用时引用节点处于选中状态;其中包括程序集、 COM 和项目的引用。 不包括 Web 引用。|  
  
 下表显示了时应用的快捷菜单中的选定**解决方案资源管理器**跨越多个层次结构  
  
|快捷菜单|描述|  
|-------------------|-----------------|  
|IDM_VS_CTXT_XPROJ_SLNPROJ|适用于当前选定内容中包含的解决方案节点和根项目节点。|  
|IDM_VS_CTXT_XPROJ_SLNITEM|适用于当前选定内容中包含的解决方案节点和项目项。|  
|IDM_VS_CTXT_XPROJ_MULTIPROJ|适用于当前所选内容包含仅多个根项目节点。|  
|IDM_VS_CTXT_XPROJ_PROJITEM|适用于当前所选内容包含多个根项目节点和项目项。 此外，所选内容可能包含解决方案节点。|  
|IDM_VS_CTXT_XPROJ_MULTIITEM|适用时当前所选内容包含多个项目在解决方案中，从项目项或同一项目中选择的不同类型的项。|  
  
## <a name="command-groups"></a>命令组  
 下表显示了可用来在扩展项目，并可以通过访问的命令组<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_PROJNODE>快捷菜单。  
  
|命令组|描述|  
|-------------------|-----------------|  
|IDG_VS_CTXT_PROJECT_BUILD|用于生成、 重新生成和部署项目的命令。|  
|IDG_VS_CTXT_COMPILELINK|用于编译和链接项目的命令。|  
|IDG_VS_CTXT_PROJECT_CONFIG|将项目配置设置和生成顺序的命令。|  
|IDG_VS_CTXT_PROJECT_ADD|将项添加到项目的命令。|  
|IDG_VS_CTXT_PROJECT_START|设置启动项目与 F5 键相关联的命令。|  
|IDG_VS_CTXT_PROJECT_SAVE|用于保存项目项的命令。|  
|IDG_VS_CTXT_PROJECT_DEBUG|用于调试的命令。|  
|IDG_VS_CTXT_PROJECT_SCC|源代码管理命令。|  
|IDG_VS_CTXT_PROJECT_TRANSFER|命令进行剪切、 复制和粘贴操作。|  
|IDG_VS_CTXT_PROJECT_PROPERTIES|提供访问权限的命令**项目属性**对话框。|  
  
## <a name="see-also"></a>请参阅  
 [Vspackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [MenuCommands 与OleMenuCommands](../../misc/menucommands-vs-olemenucommands.md)   
 [创建可重复使用的按钮组](../../extensibility/creating-reusable-groups-of-buttons.md)
