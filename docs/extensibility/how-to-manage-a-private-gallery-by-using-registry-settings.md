---
title: 如何：通过使用注册表设置管理专用库 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSIX private galleries, managing
- managing VSIX private galleries
ms.assetid: 86b86442-4293-4cad-9fe2-876eef65f426
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3b4f33f7ecf974fe527f814b9febdc861101f1ec
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66318498"
---
# <a name="how-to-manage-a-private-gallery-by-using-registry-settings"></a>如何：使用注册表设置管理专用库
如果你是管理员或独立 Shell 扩展开发人员，您可以控制对控件、 模板和工具在 Visual Studio 库、 示例库或专用库的访问。 若要使库可用或不可用，请创建 *.pkgdef*文件，用于描述已修改的注册表项和其值。

## <a name="manage-private-galleries"></a>管理专用库
 您可以创建 *.pkgdef*文件以控制对多台计算机上的库的访问。 此文件必须具有以下格式。

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

 `Repositories`键是指要启用或禁用库。 Visual Studio 库和示例库使用以下存储库的 Guid:

- Visual Studio 库：0F45E408-7995-4375-9485-86B8DB553DC9

- 示例库：AEB9CB40-D8E6-4615-B52C-27E307F8506C

  `Disabled`值是可选的。 默认情况下，启用了库。

  `Priority`值确定在其中对库中列出的顺序**选项**对话框。 Visual Studio 库具有优先级为 10，示例库具有优先级 20。 专用库开始按 100 的优先级。 如果多个库具有相同的优先级值，其本地化的值确定它们的显示的顺序`DisplayName`属性。

  `Protocol`值是必需的基于 Atom 的或基于 SharePoint 的库。

  要么`DisplayName`，和 / 或`DisplayNameResourceID`和`DisplayNamePackageGuid`，必须指定。 如果已指定所有，则`DisplayNameResourceID`和`DisplayNamePackageGuid`对使用。

## <a name="disable-the-visual-studio-gallery-using-a-pkgdef-file"></a>禁用 Visual Studio 库使用.pkgdef 文件
 您可以禁用库中的 *.pkgdef*文件。 以下条目可以禁用 Visual Studio 库：

```
[$RootKey$\ExtensionManager\Repositories\{0F45E408-7995-4375-9485-86B8DB553DC9}]
"Disabled"=dword:00000001

```

 以下条目可以禁用示例库：

```
[$RootKey$\ExtensionManager\Repositories\{AEB9CB40-D8E6-4615-B52C-27E307F8506C}]
"Disabled"=dword:00000001

```

## <a name="see-also"></a>请参阅
- [专用库](../extensibility/private-galleries.md)