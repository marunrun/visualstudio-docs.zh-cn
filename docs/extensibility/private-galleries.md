---
title: 专用库 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSIX galleries, private
- private galleries, VSIX
ms.assetid: b6b3dee7-91c5-4556-9f69-0d56b675e83b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 115fa08bea2716d4d16ba1bc04ac2fafa82154ec
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66336097"
---
# <a name="private-galleries"></a>专用库
你可以共享控件、 模板和发布到开发的工具*专用库*为你的组织，按如下所示在 intranet 上：

- 创建 Atom (RSS) 源到您的 intranet 上的适当配置中央位置 （存储库）。 有关详细信息，请参阅[如何：创建 Atom 馈送专用库](../extensibility/how-to-create-an-atom-feed-for-a-private-gallery.md)。

- 分发 *.pkgdef*介绍专用库的文件。 我们建议为想要在同一时间连接到多台计算机的专用库的管理员完成此配置。

## <a name="add-a-private-gallery-to-extensions-and-updates-in-visual-studio"></a>添加到扩展和更新 Visual Studio 中的专用库
 当专用库可用时，您可以将其添加到**扩展和更新**Visual Studio 中。

 ![扩展管理器添加对话框](../extensibility/media/em_adddialog.png "EM_AddDialog")

### <a name="to-add-a-private-gallery-to-extensions-and-updates"></a>若要将专用库添加到扩展和更新

1. 在菜单栏上，依次选择“工具” > “选项”   。

2. 在中**环境**节点中，选择**扩展和更新**。

3. 选择 **“添加”** 按钮。

4. 在中**名称**字段中，例如，输入一个名称为专用库， `My Gallery`。

5. 在中**URL**字段中，输入的 Atom 馈送或托管专用库的 SharePoint 站点的 URL。

    1. 如果主机是 Atom 馈送的连接至专用库时，URL 将类似于此： http://www.mywebsite/mygallery/atom.xml。  此 URL 可以指向文件或网络路径。

    2. 如果主机是 SharePoint 站点，该 URL 类似于此： http://mysharepoint/sites/mygallery/forms/AllItems.aspx。

### <a name="manage-private-galleries"></a>管理专用库
 管理员可以向专用库提供多台计算机在同一时间通过修改每个计算机上的系统注册表。 若要实现此目的，创建 *.pkgdef*文件，用于描述新的注册表项和它们的值。  此文件的格式如下所示。

```
[$RootKey$\ExtensionManager\Repositories\{UniqueGUID}]
@={URI}  (REG_SZ)
Disabled=0 | 1 (DWORD)
Priority=0 (highest priority) ... MaxInt (lowest priority) (DWORD) (uint)
Protocol=Atom|Sharepoint (REG_SZ)
DisplayName={DisplayName} (REG_SZ)
DisplayNameResourceID={ID} (REG_SZ)
DisplayNamePackageGuid={GUID} (REG_SZ)

```

 有关详细信息，请参阅[如何：使用注册表设置管理专用库](../extensibility/how-to-manage-a-private-gallery-by-using-registry-settings.md)。

## <a name="install-extensions-from-a-private-gallery"></a>从专用库安装扩展
 可以搜索并从专用库，在安装 Visual Studio 扩展**扩展和更新**。 以下步骤使用名为专用库`My Gallery`。

 ![扩展管理器安装专用库](../extensibility/media/em_.png "EM_")

### <a name="to-search-for-and-install-extensions-from-a-private-gallery"></a>若要搜索并安装扩展从专用库

1. 在菜单栏上依次选择**工具** > **扩展和更新**。

2. 在左窗格中，选择**联机扩展**，然后选择**我的库**。

3. 在右窗格中，选择扩展，然后选择**下载**按钮。

## <a name="update-extensions-from-a-private-gallery"></a>从专用库自动更新扩展
 在专用库中发布新版本的 Visual Studio 扩展，您可以更新已安装的扩展。 以下步骤使用名为专用库`My Repository`。

 ![扩展管理器专用库更新](../extensibility/media/em_update.png "EM_Update")

### <a name="to-update-an-installed-extension-from-a-private-gallery"></a>若要更新已安装的扩展从专用库

1. 在菜单栏上依次选择**工具** > **扩展和更新**。

2. 在左窗格中，选择**更新**，然后选择**我的存储库**。

3. 在右窗格中，选择扩展，然后选择**更新**按钮。

## <a name="see-also"></a>请参阅
- [查找和使用 Visual Studio 扩展](../ide/finding-and-using-visual-studio-extensions.md)
- [提供 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)