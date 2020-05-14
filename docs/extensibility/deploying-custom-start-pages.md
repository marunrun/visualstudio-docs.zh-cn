---
title: 部署自定义起始页 |微软文档
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
ms.openlocfilehash: 210b4589c0e2165af537c3fa9129affb06197e9b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712230"
---
# <a name="deploy-custom-start-pages"></a>部署自定义起始页

您可以通过使用 VSIX 部署或将文件复制到目标计算机上的正确位置来部署自定义起始页。

## <a name="vsix-deployment-by-using-the-start-page-project-template"></a>使用"开始页"项目模板进行 VSIX 部署

当您使用"开始页"项目模板创建"开始页"，然后生成项目时，Visual Studio 将创建一个可以分发的 *.vsix*文件。 在 *.vsix*文件中打包起始页可为您提供以下部署选项，具体取决于您的目标受众：

- 您可以将 *.vsix*文件放在网络共享上或公共网站上。 当有人打开该文件时，将自动安装"开始页"。

- 您可以将 *.vsix*文件上载到[可视化工作室应用商店](https://marketplace.visualstudio.com/)网站，以便用户可以使用**扩展管理器**安装该文件。

"开始页"项目模板创建默认可视化工作室起始页的副本，以便您可以修改副本并保留原始副本。

您可以使用**扩展管理器**或从网站下载"开始页"项目模板。

## <a name="vsix-deployment-without-using-the-start-page-project-template"></a>不使用"开始页"项目模板进行 VSIX 部署
 成功的 VSIX 部署需要将扩展安装在 VSIX 注册过程和**扩展管理器**识别的文件夹中。 由于"开始页"项目模板已指定正确的文件夹，因此我们建议您在要打包 VSIX 部署扩展时使用它。 但是，如果您有无法使用模板的情况，则可以创建 VSIX 部署而不使用它。

 要创建 VSIX 部署而不使用"开始页"项目模板，请首先通过以下两种方式为起始页创建 *.vsix*文件：

- 通过将自定义"开始页"文件添加到空的 VSIX 项目中。 有关详细信息，请参阅[VSIX 项目模板](../extensibility/vsix-project-template.md)。

- 通过手动创建 *.vsix*文件。 要手动创建 *.v6*文件，请执行操作：

   1. 在新文件夹中创建*扩展.vsixmanifest*文件和 *[Content_Types]xml*文件。 有关详细信息，请参阅[VSIX 包的剖析](../extensibility/anatomy-of-a-vsix-package.md)。

   2. 在 Windows 资源管理器中，右键单击包含两个 XML 文件的文件夹，单击"**发送到**"，然后单击"压缩（压缩）文件夹"。 将生成的 *.zip*文件重命名为*Filename.vsix，* 其中 Filename 是安装包的可再分发文件的名称。

Visual Studio 要识别`Content Element`起始页，VSIX 清单必须包含的属性`CustomExtension Element``Type`设置为`"StartPage"`的 。 通过使用 VSIX 部署安装的起始页扩展页将显示在 **"启动**"选项**页上的"自定义起始页**"列表中，作为 **[已安装扩展名]** *扩展名*。

如果"开始页"包包含程序集，则必须添加绑定路径注册，以便在 Visual Studio 启动时它们可用。 为此，请确保您的包包含包含以下信息的 *.pkgdef*文件。

```
[$RootKey$\BindingPaths\{Insert a new GUID here}]
"$PackageFolder$"=""
```

### <a name="vsix-deployment-for-all-users"></a>所有用户的 VSIX 部署
 默认情况下，在 VSIX 包中部署的扩展仅针对当前用户安装。 您可以通过创建所有用户部署，为目标计算机的所有用户安装"开始页"。

### <a name="to-create-an-all-users-deployment"></a>创建所有用户部署

1. 在代码视图中打开*扩展名.vsixmanifest*文件。

2. 在`Identifier`vsix 清单的元素中，添加`AllUsers`值 为 的元素。 `true`

    ```
    <AllUsers>true</AllUsers>
    ```

     这将导致 vsix 安装程序提示管理员权限，然后将文件安装到 *[Common7_IDE]扩展*。

3. 打开 *.pkgdef*文件。

4. 通过添加以下内容，修改 *.pkgdef*以设置 HKLM 下的默认起始页，其中*MyStartPage.xaml*是包含"开始页"的 *.xaml*文件的名称。

     [$RootKey$_开始页\默认]

     "Uri"="$PackageFolder$\\*MyStartPage.xaml"*

     这告诉 Visual Studio 在新的"开始页"位置查看。

## <a name="file-copy-deployment"></a>文件副本部署
 您不必创建 *.vsix*文件来部署自定义"开始页"。 相反，您可以将标记和支持文件直接复制到用户的<em>@StartPages\*文件夹中。"启动"选项页上的 >*自定义起始页</em>* 列表列出该文件夹中的每个 *.xaml*文件以及路径 — 例如 *，%USERPROFILE%%\我的文档_Visual Studio [版本][起始页\\]文件名称\.xaml*。 **Startup** 如果"开始页"包含对专用程序集的引用，则必须复制它们并将其粘贴到 _PrivateAssemblies\*文件夹中。

 要分发创建"开始页"而不将其打包到 *.vsix*文件中，我们建议您使用基本文件复制策略，例如批处理脚本或任何其他部署技术，以便将文件放入所需的目录中。

### <a name="to-manually-install-a-custom-start-page"></a>手动安装自定义起始页

1. 复制包含"开始页"标记的 *.xaml*文件以及程序集以外的任何支持文件，并将其粘贴到用户的 @StartPages\*文件夹中。

2. 如果"开始页"需要程序集，请复制它们并将其粘贴到*中。{可视化工作室安装文件夹}公共7_IDE_私有程序集\\ \\*

3. 在 **"启动**选项"页上的 **"自定义起始页**"列表中，选择新的"开始页"。 有关详细信息，请参阅[自定义起始页](../ide/customizing-the-start-page-for-visual-studio.md)。

## <a name="see-also"></a>请参阅

- [自定义"开始"页](../ide/customizing-the-start-page-for-visual-studio.md)
- [将用户控件添加到"开始页面"](../extensibility/adding-user-control-to-the-start-page.md)
