---
title: 如何：使用注册表设置管理专用库 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSIX private galleries, managing
- managing VSIX private galleries
ms.assetid: 86b86442-4293-4cad-9fe2-876eef65f426
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a2630fc71bea40a4d05e616ae336759ba62431a0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710937"
---
# <a name="how-to-manage-a-private-gallery-by-using-registry-settings"></a>如何：使用注册表设置管理专用库
如果您是独立命令程序扩展的管理员或开发人员，则可以控制对可视化工作室库、示例库或专用库中的控件、模板和工具的访问。 要使库可用或不可用，请创建一个 *.pkgdef*文件，用于描述修改后的注册表项及其值。

## <a name="manage-private-galleries"></a>管理私人画廊
 您可以创建 *.pkgdef*文件来控制对多台计算机上的库的访问。 此文件必须具有以下格式。

```
[$RootKey$\ExtensionManager\Repositories\{UniqueGUID}]
@={URI}  (REG_SZ)
Disabled=0 | 1 (DWORD)
Priority=0 (highest priority) ... MaxInt (lowest priority) (DWORD) (uint)
Protocol=Atom Feed|Sharepoint (REG_SZ)
DisplayName={DisplayName} (REG_SZ)
DisplayNameResourceID={ID} (REG_SZ)
DisplayNamePackageGuid={GUID} (REG_SZ)

```

 该`Repositories`键是指要启用或禁用的库。 可视化工作室库和示例库使用以下存储库 GUID：

- 视觉工作室画廊 ： 0F45E408-7995-4375-9485-86B8DB553DC9

- 样品库 ： AEB9CB40-D8E6-4615-B52C-27E307F8506C

  该`Disabled`值是可选的。 默认情况下，启用了库。

  该`Priority`值确定"**选项**"对话框中列出库的顺序。 可视化工作室库具有优先级 10，示例库具有优先级 20。 私人画廊从优先级 100 开始。 如果多个库具有相同的优先级值，则它们显示的顺序由其本地化`DisplayName`属性的值决定。

  基于`Protocol`Atom 或基于 SharePoint 的图库需要该值。

  必须`DisplayName`指定 或`DisplayNameResourceID``DisplayNamePackageGuid`两者 以及 和 。 如果全部指定，则使用`DisplayNameResourceID`和`DisplayNamePackageGuid`对。

## <a name="disable-the-visual-studio-gallery-using-a-pkgdef-file"></a>使用 .pkgdef 文件禁用可视化工作室库
 您可以禁用 *.pkgdef*文件中的库。 以下条目禁用视觉工作室库：

```
[$RootKey$\ExtensionManager\Repositories\{0F45E408-7995-4375-9485-86B8DB553DC9}]
"Disabled"=dword:00000001

```

 以下条目禁用示例库：

```
[$RootKey$\ExtensionManager\Repositories\{AEB9CB40-D8E6-4615-B52C-27E307F8506C}]
"Disabled"=dword:00000001

```

## <a name="see-also"></a>请参阅
- [私人画廊](../extensibility/private-galleries.md)
