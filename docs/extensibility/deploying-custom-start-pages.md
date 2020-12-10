---
title: 部署自定义起始页 |Microsoft Docs
description: 了解如何使用 VSIX 部署或通过将文件复制到目标计算机上的正确位置来部署自定义起始页。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- package start page
- deploy start page
ms.assetid: 4a7eb360-de83-41d5-be53-3cfb160d19f9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 76c2fc23a2b76b48152a4d3d44d687f165abf106
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "96993882"
---
# <a name="deploy-custom-start-pages"></a>部署自定义起始页

您可以通过使用 VSIX 部署或通过将文件复制到目标计算机上的正确位置来部署自定义起始页。

## <a name="vsix-deployment-by-using-the-start-page-project-template"></a>使用起始页项目模板的 VSIX 部署

使用 "起始页" 项目模板创建 "起始页"，然后生成项目时，Visual Studio 将创建一个可分发的 *.vsix* 文件。 打包 *.vsix* 文件中的起始页可以根据你的目标受众，为你提供以下部署选项：

- 可以将 *.vsix* 文件放在网络共享或公共网站上。 当某个用户打开该文件时，将自动安装起始页。

- 您可以将 *.vsix* 文件上载到 [Visual Studio Marketplace](https://marketplace.visualstudio.com/) 网站，以便用户可以使用 **扩展管理器** 进行安装。

"起始页" 项目模板创建默认 Visual Studio 起始页的副本，以便您可以修改副本并保留原始页。

您可以使用 **扩展管理器** 或从网站下载 "起始页" 项目模板。

## <a name="vsix-deployment-without-using-the-start-page-project-template"></a>不使用起始页项目模板的 VSIX 部署
 成功的 VSIX 部署需要在由 VSIX 注册过程和 **扩展管理器** 识别的文件夹中安装一个扩展。 由于起始页项目模板已经指定了正确的文件夹，因此，我们建议你在每次需要为 VSIX 部署打包扩展时使用它。 但是，如果你不能使用模板，则可以在不使用模板的情况下创建它。

 若要在不使用起始页项目模板的情况下创建 VSIX 部署，请先使用以下两种方法之一创建起始页的 *.vsix* 文件：

- 通过将自定义起始页文件添加到空 VSIX 项目中。 有关详细信息，请参阅 [VSIX 项目模板](../extensibility/vsix-project-template.md)。

- 通过手动创建 *.vsix* 文件。 若要手动创建 *.vsix* 文件：

   1. 在新文件夹中创建 *source.extension.vsixmanifest* 文件和 *[Content_Types] .xml* 文件。 有关详细信息，请参阅 [VSIX 包的解析](../extensibility/anatomy-of-a-vsix-package.md)。

   2. 在 Windows 资源管理器中，右键单击包含两个 XML 文件的文件夹，单击 " **发送到**"，然后单击 "压缩 (Zipped) 文件夹。 将生成的 *.zip* 文件重命名为 *Filename .Vsix*，其中 filename 是用于安装包的可再发行文件的名称。

为了使 Visual Studio 能够识别起始页， `Content Element` VSIX 清单的必须包含一个 `CustomExtension Element` `Type` 将属性设置为的 `"StartPage"` 。 **"启动选项"** 页上的 "**自定义起始页**" 列表中显示了已使用 VSIX 部署安装的起始页 **扩展。** 

如果起始页包包含程序集，则必须添加绑定路径注册，使其在 Visual Studio 启动时可用。 为此，请确保你的包包含 *.pkgdef* 文件，其中包含以下信息。

```
[$RootKey$\BindingPaths\{Insert a new GUID here}]
"$PackageFolder$"=""
```

### <a name="vsix-deployment-for-all-users"></a>所有用户的 VSIX 部署
 默认情况下，仅为当前用户安装 VSIX 包中部署的扩展。 可以通过创建 All-Users 部署，为目标计算机的所有用户设置开始页面。

### <a name="to-create-an-all-users-deployment"></a>创建 All-Users 部署

1. 在代码视图中打开 *source.extension.vsixmanifest* 文件。

2. 在 `Identifier` vsix 清单的元素中，添加一个 `AllUsers` 值为的元素 `true` 。

    ```
    <AllUsers>true</AllUsers>
    ```

     这将导致 vsix 安装程序提示管理员权限，然后将这些文件安装到 *\Common7\IDE\Extensions*。

3. 打开 *.pkgdef* 文件。

4. 通过添加以下项来修改 *.pkgdef* 以设置 HKLM 下的默认起始页，其中 *MyStartPage* 是包含起始页的 *.xaml* 文件的名称。

     [$RootKey $ \StartPage\Default]

     "Uri" = "$PackageFolder $ \\ *MyStartPage*"

     这会告知 Visual Studio 在新的起始页位置中查找。

## <a name="file-copy-deployment"></a>文件复制部署
 不必创建 *.vsix* 文件来部署自定义起始页。 相反，你可以将标记和支持文件直接复制到用户的 <em>\StartPages \* 文件夹中。"启动选项" 页上的 "*自定义起始页</em>* " 列表中列出了该文件夹中的每个 *.xaml* 文件以及路径，例如 *%USERPROFILE%\My Documents\Visual Studio {version} \StartPages \\ {file Name} .xaml*。  如果起始页包含对专用程序集的引用，则必须复制这些程序集，并将其粘贴到 * \PrivateAssemblies \* 文件夹中。

 若要分发已创建的起始页，而不将其打包到 *.vsix* 文件中，我们建议你使用基本的文件复制策略（例如，批处理脚本）或任何其他部署技术，使你能够将这些文件放入所需的目录。

### <a name="to-manually-install-a-custom-start-page"></a>手动安装自定义起始页

1. 复制包含起始页标记的 *.xaml* 文件和除程序集之外的任何支持文件，然后将其粘贴到用户的 * \StartPages \* 文件夹中。

2. 如果起始页需要程序集，请将其复制并粘贴到中 *。 \\{Visual Studio 安装文件夹} \Common7\IDE\PrivateAssemblies \\*。

3. 在 "**启动** 选项" 页面上的 "**自定义起始页**" 列表中，选择新的起始页。 有关详细信息，请参阅 [自定义起始页](../ide/customizing-the-start-page-for-visual-studio.md)。

## <a name="see-also"></a>另请参阅

- [自定义起始页](../ide/customizing-the-start-page-for-visual-studio.md)
- [将用户控件添加到起始页](../extensibility/adding-user-control-to-the-start-page.md)
