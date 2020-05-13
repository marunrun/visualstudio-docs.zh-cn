---
title: 使用命令行发布扩展
ms.date: 07/12/2018
ms.topic: conceptual
helpviewer_keywords:
- publishing extensions
- extension, publishing
ms.assetid: 6ff9efc4-919d-4071-a80d-6dbdd2ceb2f8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 40be0252218f39b4ff98b58caedd7f9f20ce6d5d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697130"
---
# <a name="walkthrough-publishing-a-visual-studio-extension-via-command-line"></a>演练：通过命令行发布可视化工作室扩展

本演练演示如何使用命令行将可视化工作室扩展发布到可视化工作室市场。 将扩展添加到应用商店时，开发人员可以使用[**"扩展和更新**](../ide/finding-and-using-visual-studio-extensions.md)"对话框浏览其中的新扩展和更新的扩展。

VsixPublisher.exe 是用于将可视化工作室扩展发布到应用商店的命令行工具。 可以从 ${VSInstallDir}VSSDK\VisualStudio 集成\工具\Bin_VsixPublisher.exe 访问它。 此工具上可用的命令是：**发布**、**创建发布者**、**删除发布者**、**删除扩展**、**登录**、**注销**。

## <a name="commands"></a>命令

### <a name="publish"></a>发布

发布到应用商店的扩展。 扩展名可以是 vsix、exe/msi 文件或链接。 如果扩展已使用相同的版本存在，它将覆盖扩展。 如果扩展不存在，它将创建新扩展。

|命令选项 |描述 |
|---------|---------|
|有效负载（必需） | 要发布的有效负载的路径或用作"更多信息 URL"的链接。 |
|发布清单（必需） | 要使用的发布清单文件的路径。 |
|忽略警告 | 发布扩展时要忽略的警告列表。 发布扩展时，这些警告显示为命令行消息。 （例如，"VSIX 验证器警告 01，VSIX 验证器警告 02"）
|个人访问令牌 | 用于对发布者进行身份验证的个人访问令牌 （PAT）。 如果未提供，则从登录用户获取 PAT。 |

```
VsixPublisher.exe publish -payload "{path to vsix}" -publishManifest "{path to vs-publish.json}" -ignoreWarnings "VSIXValidatorWarning01,VSIXValidatorWarning02"
```

### <a name="createpublisher"></a>创建发布者

在应用商店中创建发布者。 还将发布者记录到计算机中以进行将来的操作（例如，删除/发布扩展）。

|命令选项 |描述 |
|---------|---------|
|显示名称（必需） | 显示发布者的名称。 |
|发布者名称（必需） | 发布者的名称（例如标识符）。 |
|个人访问令牌（必需） | 用于对发布者进行身份验证的个人访问令牌。 |
|shortDescription | 发布者的简短描述（不是文件）。 |
|长描述 | 发布者（不是文件）的长描述。 |

```
VsixPublisher.exe createPublisher -publisherName "{Publisher Name}" -displayName "{Publisher Display Name}" -personalAccessToken "{Personal Access Token}"
```

### <a name="deletepublisher"></a>删除发布者

删除应用商店上的发布者。

|命令选项 |描述 |
|---------|---------|
|发布者名称（必需） | 发布者的名称（例如标识符）。 |
|个人访问令牌（必需） | 用于对发布者进行身份验证的个人访问令牌。 |

```
VsixPublisher.exe deletePublisher -publisherName "{Publisher Name}" -personalAccessToken "{Personal Access Token}"
```

### <a name="deleteextension"></a>删除扩展

从应用商店中删除扩展。

|命令选项 |描述 |
|---------|---------|
|分名（必填） | 要删除的扩展的名称。 |
|发布者名称（必需） | 发布者的名称（例如标识符）。 |
|个人访问令牌 | 用于对发布者进行身份验证的个人访问令牌。 如果未提供，则从登录用户获取 pat。 |

```
VsixPublisher.exe deleteExtension -extensionName "{Extension Name}" -publisherName "{Publisher Name}"
```

### <a name="login"></a>login

将发布者记录到计算机中。

|命令选项 |描述 |
|---------|---------|
|个人访问令牌（必需 | 用于对发布者进行身份验证的个人访问令牌。 |
|发布者名称（必需） | 发布者的名称（例如标识符）。 |
|overwrite | 指定任何现有发布者都应使用新的个人访问令牌进行覆盖。 |

```
VsixPublisher.exe login -personalAccessToken "{Personal Access Token}" -publisherName "{Publisher Name}"
```

### <a name="logout"></a>logout

将发布者从计算机中注销。

|命令选项 |描述 |
|---------|---------|
|发布者名称（必需） | 发布者的名称（例如标识符）。 |
|忽略缺失的发布者 | 指定如果指定的发布者尚未登录，该工具不应出错。 |

```
VsixPublisher.exe logout -publisherName "{Publisher Name}"
```

## <a name="publishmanifest-file"></a>发布清单文件

**发布**命令使用 publishManifest 文件。 它表示有关应用商店需要知道的扩展的所有元数据。 如果上载的扩展来自 VSIX 扩展，"标识"属性必须仅设置"内部名称"。 这是因为可以从 vsixmanifest 文件生成"标识"属性的其余部分。 如果扩展是 msi/exe 或链接扩展，则用户必须在"标识"属性中提供所需的字段。 清单的其余部分包含特定于应用商店的信息（例如，类别、是否启用 Q&A 等）。

VSIX 扩展名发布清单文件示例：

```json
{
    "$schema": "http://json.schemastore.org/vsix-publish",
    "categories": [ "build", "coding" ],  // The categories of the extension. Between 1 and 3 categories are required.
    "identity": {
        "internalName": "MyVsixExtension" // If not specified, we try to generate the name from the display name of the extension in the vsixmanifest file.
                                            // Required if the display name is not the actual name of the extension.
    },
    "overview": "overview.md",            // Path to the "readme" file that gets uploaded to the Marketplace. Required.
    "priceCategory": "free",              // Either "free", "trial", or "paid". Defaults to "free".
    "publisher": "MyPublisherName",       // The name of the publisher. Required.
    "private": false,                     // Specifies whether or not the extension should be public when uploaded. Defaults to false.
    "qna": true,                          // Specifies whether or not the extension should have a Q&A section. Defaults to true.
    "repo": "https://github.com/MyPublisherName/MyVsixExtension" // Not required.
}
```

MSI/EXE 或 LINK 发布清单文件示例：

```json
{
    "$schema": "http://json.schemastore.org/vsix-publish",
    "categories": [ "build", "coding" ],
    "identity": {
        "description": "My extension.", // The description of the extension. Required for non-vsix extensions.
        "displayName": "My Extension",  // The display name of the extension. Required for non-vsix extensions.
        "icon": "\\path\\to\\icon.ico", // The path to an icon file (can be relative to the json file location). Required for non-vsix extensions.
        "installTargets": [             // The installation targets for the extension. Required for non-vsix extensions.
            {
                "sku": "Microsoft.VisualStudio.Community",
                "version": "[10.0, 16.0)"
            }
        ],
        "internalName": "MyExtension",
        "language": "en-US",            // The default language id of the extension. Can be in the "1033" or "en-US" format. Required for non-vsix extensions.
        "tags": [ "tag1", "tag2" ],     // The tags for the extension. Not required.
        "version": "3.7.0",             // The version of the extension. Required for non-vsix extensions.
        "vsixId": "MyExtension",        // The vsix id of the extension. Not required but useful for showing updates to installed extensions.
    },
    "overview": "overview.md",
    "priceCategory": "free",
    "publisher": "MyPublisherName",
    "private": false,
    "qna": true,
    "repo": "https://github.com/MyPublisherName/MyVsixExtension"
}
```

## <a name="asset-files"></a>资产文件

可以提供资产文件，用于在读读文件中嵌入图像等内容。 例如，如果扩展具有以下"概述"标记文档：

```markdown
TestExtension
...
This is test extension.
![Test logo](images/testlogo.png "Test logo")
```

为了解决前面的示例中的"图像/testlogo.png"，用户可以在其发布清单中提供"资产文件"，如下所示：

```json
{
    "assetFiles": [
        {
            "pathOnDisk": "\\path\\to\\logo.png",
            "targetPath": "images/logo.png"
        }
    ],
    // other required fields
}
```

## <a name="publishing-walkthrough"></a>发布演练

### <a name="prerequisites"></a>先决条件

要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

### <a name="create-a-visual-studio-extension"></a>创建可视化工作室扩展

在这种情况下，我们将使用默认的 VSPackage 扩展，但相同的步骤对于每种扩展都有效。

1. 在 C# 中创建一个 VSPackage，名为"TestPublish"，具有菜单命令。 有关详细信息，请参阅[创建您的第一个扩展：你好世界](../extensibility/extensibility-hello-world.md)。

### <a name="package-your-extension"></a>打包扩展

1. 使用有关产品名称、作者和版本的正确信息更新扩展 vsix 清单。

   ![更新扩展 vsixmanifest](media/update-extension-vsixmanifest.png)

2. 在**释放**模式下生成扩展。 现在，您的扩展将打包为 [bin_释放文件夹中的 VSIX》。

3. 您可以双击 VSIX 以验证安装。

### <a name="test-the-extension"></a>测试扩展

 在分发扩展之前，请生成并对其进行测试，以确保它在 Visual Studio 的实验实例中正确安装。

1. 在可视化工作室中，开始调试。 打开视觉工作室的实验实例。

2. 在实验实例中，转到 **"工具"** 菜单，然后单击 **"扩展和更新..."。** 测试发布扩展应显示在中心窗格中并启用。

3. 在 **"工具"** 菜单上，请确保看到测试命令。

### <a name="publish-the-extension-to-the-marketplace-via-command-line"></a>通过命令行将扩展发布到应用商店

1. 请确保您已构建扩展的发布版本，并且该版本是最新的。

2. 请确保您已创建 publishmanifest.json 和overview.md文件。

3. 打开命令行并导航到 $_VSInstallDir_VSSDK_VisualStudio 集成\工具\Bin_目录。

4. 要创建新发布服务器，请使用以下命令：

   ```
   VsixPublisher.exe createPublisher -publisherName "TestVSIXPublisher" -displayName "Test VSIX Publisher" -personalAccessToken "{Personal Access Token that is used to authenticate the publisher. If not provided, the pat is acquired from the logged-in users.}"
   ```

5. 成功创建发布者时，您将看到以下命令行消息：

   ```
   Added 'Test VSIX Publisher' as a publisher on the Marketplace.
   ```

6. 您可以通过导航到[可视化工作室市场](https://marketplace.visualstudio.com/manage/publishers)来验证您创建的新发布者

7. 要发布新扩展，请使用以下命令：

   ```
   VsixPublisher.exe publish -payload "{Path to vsix file}"  -publishManifest "{path to publishManifest file}"
   ```

8. 成功创建发布者时，您将看到以下命令行消息：

   ```
   Uploaded 'MyVsixExtension' to the Marketplace.
   ```

9. 您可以通过导航到[可视化工作室市场](https://marketplace.visualstudio.com/)来验证发布的新扩展

### <a name="install-the-extension-from-the-visual-studio-marketplace"></a>从可视化工作室市场安装扩展

现在，扩展已发布，请将其安装在 Visual Studio 中并在那里进行测试。

1. 在可视化工作室中，在 **"工具"** 菜单上，单击 **"扩展和更新..."。**

2. 单击 **"联机"，** 然后搜索测试发布。

3. 单击“下载”  。 然后，将计划安装扩展。

4. 要完成安装，关闭可视化工作室的所有实例。

## <a name="remove-the-extension"></a>删除扩展

可以从可视化工作室应用商店和计算机中删除扩展。

### <a name="to-remove-the-extension-from-the-marketplace-via-command-line"></a>通过命令行从应用商店中删除扩展

1. 如果要删除扩展，请使用以下命令：

   ```
   VsixPublisher.exe deleteExtension -publisherName "TestVSIXPublisher" -extensionName "MyVsixExtension"
   ```

2. 成功删除扩展后，您将看到以下命令行消息：

   ```
   Removed 'MyVsixExtension' from the Marketplace.
   ```

### <a name="to-remove-the-extension-from-your-computer"></a>从计算机中删除扩展名

1. 在可视化工作室中，在 **"工具"** 菜单上，单击 **"扩展和更新**"。

2. 选择"MyVsix 扩展"，然后单击 **"卸载**"。 然后，将安排卸载扩展。

3. 要完成卸载，关闭可视化工作室的所有实例。
