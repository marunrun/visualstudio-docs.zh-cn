---
title: 部署自定义起始页 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- package start page
- deploy start page
ms.assetid: 4a7eb360-de83-41d5-be53-3cfb160d19f9
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 5a84ba2ff92463ebea177fc5c3b04810de7ae817
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66348218"
---
# <a name="deploy-custom-start-pages"></a>部署自定义起始页

使用 VSIX 部署或将文件复制到目标计算机上的正确位置，你可以部署自定义起始页。

## <a name="vsix-deployment-by-using-the-start-page-project-template"></a>使用起始页项目模板的 VSIX 部署

当使用起始页项目模板，创建一个起始页，然后生成项目时，Visual Studio 将创建 *.vsix*可以分发的文件。 打包中的启动页 *.vsix*文件为您提供了部署，具体取决于您的目标受众的以下选项：

- 可以将放 *.vsix*或公共网站上的网络共享文件。 在有人打开文件时，会自动安装启动页。

- 可以上传 *.vsix*的文件[Visual Studio Marketplace](https://marketplace.visualstudio.com/) Web 站点，以便用户可以使用来安装它**扩展管理器**。

起始页项目模板创建一份默认 Visual Studio 起始页，以便您可以修改副本，并保留原始。

你可以通过使用获取起始页项目模板**扩展管理器**或通过从 Web 站点下载它。

## <a name="vsix-deployment-without-using-the-start-page-project-template"></a>而无需使用起始页项目模板的 VSIX 部署
 成功的 VSIX 部署需要在 VSIX 注册过程和识别的文件夹中安装的扩展**扩展管理器**。 由于起始页项目模板已指定正确的文件夹中，我们建议要打包为 VSIX 部署扩展时使用它。 但是，如果你不能在其中使用该模板的用例，您可以创建 VSIX 部署而无需使用它。

 若要创建 VSIX 部署而无需使用起始页项目模板，请先创建 *.vsix*这两种方式之一中的启动页的文件：

- 通过将自定义起始页文件添加到一个空的 VSIX 项目。 有关详细信息，请参阅[VSIX 项目模板](../extensibility/vsix-project-template.md)。

- 通过手动创建 *.vsix*文件。 若要创建 *.vsix*手动文件：

   1. 创建*extension.vsixmanifest*文件并 *[Content_Types].xml*的新文件夹中的文件。 有关详细信息，请参阅[VSIX 包的剖析](../extensibility/anatomy-of-a-vsix-package.md)。

   2. 在 Windows 资源管理器，右键单击包含两个 XML 文件的文件夹，单击**发送到**，然后单击压缩 (zipped) 文件夹。 重命名生成 *.zip*的文件*Filename.vsix*，其中 Filename 是用于安装包的可再发行文件的名称。

Visual studio 能够识别启动页上，`Content Element`必须包含的 VSIX 清单`CustomExtension Element`具有`Type`属性设置为`"StartPage"`。 使用 VSIX 部署安装起始页扩展将出现在**自定义起始页**上列出**启动**选项页中以 **[安装的扩展]** *扩展插件名称*。

如果起始页包中包含的程序集，必须添加绑定路径注册，以便它们可用于 Visual Studio 将启动。 若要执行此操作，请确保您的包，包括 *.pkgdef*包含以下信息的文件。

```
[$RootKey$\BindingPaths\{Insert a new GUID here}]
"$PackageFolder$"=""
```

### <a name="vsix-deployment-for-all-users"></a>所有用户的的 VSIX 部署
 默认情况下，在 VSIX 包中部署的扩展插件安装仅为当前用户。 您可以通过创建的所有用户部署的目标计算机的所有用户都使起始页安装。

### <a name="to-create-an-all-users-deployment"></a>若要创建的所有用户部署

1. 打开*extension.vsixmanifest*在代码视图中的文件。

2. 在中`Identifier`vsix 清单中，元素添加`AllUsers`元素的值为`true`。

    ```
    <AllUsers>true</AllUsers>
    ```

     这将导致 vsix 安装程序提示输入管理员权限，然后安装到的文件 *\Common7\IDE\Extensions* 。

3. 打开 *.pkgdef*文件。

4. 修改 *.pkgdef*若要设置默认起始页在 HKLM 下的通过添加以下内容，其中*MyStartPage.xaml*的名称 *.xaml*文件，其中包含您开始页。

     [$RootKey$\StartPage\Default]

     "Uri"="$PackageFolder$\\*MyStartPage.xaml*"

     这将告知 Visual Studio 中新的起始页位置进行查找。

## <a name="file-copy-deployment"></a>文件复制部署
 不需要创建 *.vsix*文件以部署自定义起始页。 相反，您可以将复制标记和直接在用户的支持文件<em>\StartPages\*文件夹。**自定义起始页</em>* 上列出**启动**选项页面列出了每个 *.xaml*路径以及该文件夹中的文件 — 例如， *%USERPROFILE%\My Documents\Visual Studio {version} \StartPages\\{文件名}.xaml*。 如果你的起始页包含对专用程序集的引用，必须将它们复制并将其粘贴 * \PrivateAssemblies\*文件夹。

 分发而无需打包在创建起始页 *.vsix*文件中，我们建议使用基本的文件的复制策略，例如，批处理脚本，或任何其他部署技术，它允许您将这些文件置于所需的目录。

### <a name="to-manually-install-a-custom-start-page"></a>若要手动安装自定义起始页

1. 复制 *.xaml*文件，包含起始页标记，以及任何支持文件以外的程序集，并将其粘贴在用户的 * \StartPages\*文件夹。

2. 如果启动页要求程序集，将它们复制并将其粘贴 *...\\{Visual Studio 安装文件夹} \Common7\IDE\PrivateAssemblies\\* 。

3. 在中**自定义起始页**上列出**启动**选项页上，选择新的起始页。 有关详细信息，请参阅[自定义起始页](../ide/customizing-the-start-page-for-visual-studio.md)。

## <a name="see-also"></a>请参阅

- [自定义起始页](../ide/customizing-the-start-page-for-visual-studio.md)
- [将用户控件添加到启动页](../extensibility/adding-user-control-to-the-start-page.md)