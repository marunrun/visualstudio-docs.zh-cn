---
title: 迁移旧版语言服务 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, migrating
ms.assetid: e0f666a0-92a7-4f9c-ba79-d05b13fb7f11
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1027d4b834f1ffdd2289ced2ee5523c20f9d2353
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72726695"
---
# <a name="migrating-a-legacy-language-service"></a>迁移旧版语言服务
你可以通过更新项目并将 source.extension.vsixmanifest 文件添加到项目中，将旧版语言服务迁移到更高版本的 Visual Studio。 语言服务本身将像以前一样继续工作，因为 Visual Studio 编辑器会改编它。

 旧版语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的更新方法是使用 MEF 扩展。 若要了解有关实现语言服务的新方法的详细信息，请参阅[编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)。

> [!NOTE]
> 建议你尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并使你能够利用新的编辑器功能。

## <a name="migrating-a-visual-studio-2008-language-service-solution-to-a-later-version"></a>将 Visual Studio 2008 语言服务解决方案迁移到更高版本
 以下步骤演示如何调整名为 RegExLanguageService 的 Visual Studio 2008 示例。 可在 visual studio 2008 SDK 安装的*Visual STUDIO SDK 安装路径*\VisualStudioIntegration\Samples\IDE\CSharp\Example.RegExLanguageService\ 文件夹中找到此示例。

> [!IMPORTANT]
> 如果语言服务未定义颜色，则必须在 VSPackage 上将 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute.RequestStockColors%2A> 显式设置为 `true`：

```
[Microsoft.VisualStudio.Shell.ProvideLanguageService(typeof(YourLanguageService), YourLanguageServiceName, 0, RequestStockColors = true)]
```

#### <a name="to-migrate-a-visual-studio-2008-language-service-to-a-later-version"></a>将 Visual Studio 2008 语言服务迁移到更高版本

1. 安装较新版本的 Visual Studio 和 Visual Studio SDK。 有关安装 SDK 的方法的详细信息，请参阅[安装 Visual STUDIO SDK](../../extensibility/installing-the-visual-studio-sdk.md)。

2. 编辑 RegExLangServ 文件（而不在 Visual Studio 中加载它。

     在引用 VsSDK 文件的 `Import` 节点中，将值替换为以下文本。

    ```
    $(MSBuildExtensionsPath)\Microsoft\VisualStudio\v14.0\VSSDK\Microsoft.VsSDK.targets
    ```

3. 保存该文件，然后将其关闭。

4. 打开 RegExLangServ 解决方案。

5. 此时将显示单向**升级**窗口。 单击“确定”。

6. 更新项目属性。 通过选择 "**解决方案资源管理器**中的项目节点，右键单击，然后选择"**属性**"，打开"**项目属性**"窗口。

    - 在 "**应用程序**" 选项卡上，将 "**目标框架**" 更改为**4.6.1**。

    - 在 "**调试**" 选项卡上的 "**启动外部程序**" 框中，键入 **\<Visual Studio 安装路径 > \Common7\IDE\devenv.exe.** 。

         在 "**命令行参数**" 框中，键入/**rootsuffix Exp**。

7. 更新以下引用：

    - 删除对 VisualStudio 的引用，然后添加对 VisualStudio 和 VisualStudio............. 的引用。

    - 删除对 VisualStudio 的引用，然后添加对 VisualStudio 的引用。 LanguageService....。

    - 添加一个对 VisualStudio 的引用。）。

8. 打开 VsPkg.cs 文件并将 `DefaultRegistryRoot` 特性的值更改为

    ```
    "Software\\Microsoft\\VisualStudio\\14.0Exp"
    ```

9. 原始示例不注册其语言服务，因此必须将以下属性添加到 VsPkg.cs。

    ```
    [ProvideLanguageService(typeof(RegularExpressionLanguageService), "RegularExpressionLanguage", 0, RequestStockColors=true)]
    ```

10. 必须添加 source.extension.vsixmanifest 文件。

    - 将此文件从现有扩展复制到项目目录。 （获取此文件的一种方法是创建一个 VSIX 项目（在 "**文件**" 下，单击 "**新建**"，然后单击 "**项目**"。 在 Visual Basic 或C#单击 "**扩展性**" 下，选择 " **VSIX 项目**"。）

    - 将文件添加到项目。

    - 在文件的**属性**中，将 "**生成操作**" 设置为 "**无**"。

    - 在**VSIX 清单编辑器**中打开文件。

    - 更改以下字段：

    - **ID**： RegExLangServ

    - **产品名称**： RegExLangServ

    - **说明**：正则表达式语言服务。

    - 在 **"资产**" 下，单击 "**新建**"，选择 " **VisualStudio. VsPackage**"**类型**，将 "**源**" 设置为 "**当前解决方案中的项目**"，然后将**项目**设置为 " **RegExLangServ**"。

    - 保存并关闭文件。

11. 生成解决方案。 生成的文件将部署到 **%USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0Exp\Extensions\MSIT\ RegExLangServ \\** 。

12. 开始调试。 已打开 Visual Studio 的第二个实例。

## <a name="see-also"></a>请参阅
- [旧版语言服务扩展性](../../extensibility/internals/legacy-language-service-extensibility.md)