---
title: 私人画廊 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSIX galleries, private
- private galleries, VSIX
ms.assetid: b6b3dee7-91c5-4556-9f69-0d56b675e83b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4056e4dedf06ffe86755bf946c77032d6f6782dd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702043"
---
# <a name="private-galleries"></a>私人画廊
通过将控件、模板和工具发布到组织 Intranet 上的*专用库*，可以共享这些控件、模板和工具，如下所示：

- 创建 Atom （RSS） 源，以连接到 Intranet 上配置适当的中央位置（存储库）。 有关详细信息，请参阅[如何：为专用库创建 Atom 源](../extensibility/how-to-create-an-atom-feed-for-a-private-gallery.md)。

- 分发描述私有库的 *.pkgdef*文件。 我们建议对希望同时将专用库连接到多台计算机的管理员进行此配置。

## <a name="add-a-private-gallery-to-extensions-and-updates-in-visual-studio"></a>将专用库添加到可视化工作室中的扩展和更新
 当专用库可用时，您可以将其添加到 Visual Studio 中的**扩展和更新**。

 ![“扩展管理器添加”对话框](../extensibility/media/em_adddialog.png "EM_AddDialog")

### <a name="to-add-a-private-gallery-to-extensions-and-updates"></a>将专用库添加到扩展和更新

1. 在菜单栏上，选择 **"工具** > **选项**"。

2. 在 **"环境"** 节点中，选择 **"扩展"和"更新**"。

3. 选择 **“添加”** 按钮。

4. 在 **"名称"** 字段中，输入专用库的名称，例如。 `My Gallery`

5. 在**URL**字段中，输入托管专用库的 Atom 源或 SharePoint 站点的 URL。

    1. 如果主机是连接到专用库的 Atom 源，则 URL 将类似于此 URL： http://www.mywebsite/mygallery/atom.xml。  此 URL 可以引用文件或网络路径。

    2. 如果主机是 SharePoint 站点，则 URL 将类似于此http://mysharepoint/sites/mygallery/forms/AllItems.aspx站点： 。

### <a name="manage-private-galleries"></a>管理私人画廊
 管理员可以通过修改每台计算机上的系统注册表，同时使专用库可供多台计算机使用。 为此，请创建一个 *.pkgdef*文件，描述新的注册表项及其值。  此文件的格式如下。

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

 有关详细信息，请参阅[操作方式：使用注册表设置管理专用库](../extensibility/how-to-manage-a-private-gallery-by-using-registry-settings.md)。

## <a name="install-extensions-from-a-private-gallery"></a>从专用库安装扩展
 您可以在**扩展和更新**中从专用库搜索和安装 Visual Studio 扩展。 以下步骤使用名为 的`My Gallery`私有库。

 ![安装专用库的扩展管理器](../extensibility/media/em_.png "EM_")

### <a name="to-search-for-and-install-extensions-from-a-private-gallery"></a>从专用库搜索和安装扩展

1. 在菜单栏上，选择 **"工具** > **扩展"和"更新**"。

2. 在左侧窗格中，选择 **"联机扩展**"，然后选择 **"我的库**"。

3. 在右侧窗格中，选择扩展名，然后选择"**下载**"按钮。

## <a name="update-extensions-from-a-private-gallery"></a>从专用库更新扩展
 当 Visual Studio 扩展的新版本发布到专用库中时，您可以更新已安装的扩展。 以下步骤使用名为 的`My Repository`私有库。

 ![扩展管理器专用库更新](../extensibility/media/em_update.png "EM_Update")

### <a name="to-update-an-installed-extension-from-a-private-gallery"></a>从专用库更新已安装的扩展

1. 在菜单栏上，选择 **"工具** > **扩展"和"更新**"。

2. 在左侧窗格中，选择 **"更新**"，然后选择 **"我的存储库**"。

3. 在右侧窗格中，选择扩展名，然后选择 **"更新**"按钮。

## <a name="see-also"></a>请参阅
- [查找和使用可视化工作室扩展](../ide/finding-and-using-visual-studio-extensions.md)
- [船舶视觉工作室扩展](../extensibility/shipping-visual-studio-extensions.md)
