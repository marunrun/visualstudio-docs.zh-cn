---
title: 疑难解答：如何发布现有扩展的新版本？
description: 有关通过发布工作流更新现有扩展的指南。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 12/14/2020
ms.technology: vs-ide-general
ms.assetid: 5DA76197-7859-421f-AC45-401F22F5D794
ms.topic: troubleshooting
ms.openlocfilehash: 862ae404571da44d9ca28db2c94d2ebeb39ce79f
ms.sourcegitcommit: 19061b61759ce8e3b083a0e01a858e5435580b3e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97488540"
---
# <a name="troubleshooting-how-do-i-release-a-new-version-of-my-existing-extension"></a>疑难解答：如何发布现有扩展的新版本？

> [!IMPORTANT]
> 目前，Visual Studio 2019 for Mac 尚不支持创建新扩展。

Visual Studio for Mac 扩展存储库服务器将于 2021 年 1 月 15 日迁移。 此移动不会影响已下载扩展的用户，但会更改你在此日期之后发布新版本扩展的方式。

作为现有扩展的创建者，你需要遵循其他工作流以发布进一步的更新。 此过程包括以下步骤：
- 为每个扩展设置公共 GitHub 存储库
- 通过[扩展发布邮件列表](mailto:vsmextpub@microsoft.com)将存储库 URL 共享到 Visual Studio for Mac 团队
- 使用 GitHub 中的发布功能更新扩展


## <a name="initial-setup"></a>初始设置 

为了继续将更新发布到扩展，你需要创建一个公共 GitHub 存储库。 如果发布多个扩展，则需要为每个扩展提供单独的存储库，除非始终将它们一同进行版本控制和发布，在这种情况下，你可以使用单个存储库。

> [!NOTE]
> 虽然扩展的 GitHub 存储库需要是公共扩展库，但你无需将任何代码托管在此处。 这个过程并不要求你在 GitHub 中有任何代码。


## <a name="share-the-location-of-your-repository"></a>共享存储库的位置

设置存储库后，向[扩展发布邮件列表](mailto:vsmextpub@microsoft.com)发送包含 URL 的电子邮件。


## <a name="release-a-new-version"></a>发布新版本

你将使用存储库主页上的“创建新版本”链接来开始更新扩展的过程。 选择该链接后，请执行以下步骤：

1. 将信息添加到发布的“标记版本”，格式如下

    > v\<releaseVersion>\-vsm\<targetVersion>

    其中：
     - &lt;releaseVersion&gt; 是扩展版本号
     - &lt;targetVersion&gt; 是扩展所面向的 Visual Studio for Mac 的最低版本

2. （可选）“标题”和“说明”字段可填写所需的任何信息；此工作流不使用这些字段中的信息。

3. 确保取消勾选“预发行”复选框。 如果勾选，那么此发布过程将不会获得此版本。

4. 在“二进制文件”部分附加实现扩展的 .mpack 文件。 可以将多个 .mpack 文件附加到一个版本中。

Visual Studio for Mac 将显示与用于访问扩展存储库的 Visual Studio for Mac 安装兼容的最新版本扩展。

只要向 Visual Studio for Mac 团队注册 GitHub 存储库，Visual Studio for Mac 将在 24 小时内获得你的扩展版本。

## <a name="additional-information"></a>其他信息

- 不会发布不符合上述要求的版本。 
- 2021 年 1 月 15 日之后，扩展更新将只在 Visual Studio for Mac 8.0 或更高版本中显示。
- 现有扩展仍适用于 Visual Studio for Mac 用户，无需执行任何操作。 如果在 2021 年 1月 15 日之后发布新版本，则只需按照本指南中的说明进行操作。
