---
title: 迁移传统语言服务 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, migrating
ms.assetid: e0f666a0-92a7-4f9c-ba79-d05b13fb7f11
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9e2eff3f3a27b7d8a276c8ed776c1e11d5ce332e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707112"
---
# <a name="migrating-a-legacy-language-service"></a>迁移旧版语言服务
您可以通过更新项目并将 source.扩展.vsixmanifest 文件添加到项目中，将旧语言服务迁移到更高版本的 Visual Studio。 语言服务本身将继续像以前那样运行，因为 Visual Studio 编辑器会适应它。

 旧语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的较新方法是使用 MEF 扩展。 要了解有关实现语言服务的新方法的详细信息，请参阅[编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)。

> [!NOTE]
> 我们建议您尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并允许您利用新的编辑器功能。

## <a name="migrating-a-visual-studio-2008-language-service-solution-to-a-later-version"></a>将可视化工作室 2008 语言服务解决方案迁移到更高版本
 以下步骤演示如何调整名为 RegEx语言服务的视觉工作室 2008 示例。 您可以在 Visual Studio 2008 SDK 安装中找到此示例，在*Visual Studio SDK 安装路径*[VisualStudio 集成]示例_IDE_CSharp_示例.RegEx语言服务]文件夹中找到此示例。

> [!IMPORTANT]
> 如果语言服务未定义颜色，则必须<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute.RequestStockColors%2A>`true`在 VSPackage 上显式设置为：

```
[Microsoft.VisualStudio.Shell.ProvideLanguageService(typeof(YourLanguageService), YourLanguageServiceName, 0, RequestStockColors = true)]
```

#### <a name="to-migrate-a-visual-studio-2008-language-service-to-a-later-version"></a>将 Visual Studio 2008 语言服务迁移到更高版本

1. 安装较新版本的可视化工作室和可视化工作室 SDK。 有关安装 SDK 的方法的详细信息，请参阅[安装可视化工作室 SDK](../../extensibility/installing-the-visual-studio-sdk.md)。

2. 编辑 RegExLangServ.csproj 文件（无需在视觉工作室中加载）。

     在`Import`引用 Microsoft.VsSDK.target 文件的节点中，将值替换为以下文本。

    ```
    $(MSBuildExtensionsPath)\Microsoft\VisualStudio\v14.0\VSSDK\Microsoft.VsSDK.targets
    ```

3. 保存文件，然后关闭它。

4. 打开 RegExLangServ.sln 解决方案。

5. 将显示**单向升级**窗口。 单击“确定”。

6. 更新项目属性。 通过在**解决方案资源管理器**中选择项目节点（右键单击和选择属性）打开 **"项目属性****"** 窗口。

    - 在 **"应用程序"** 选项卡上，将**目标框架**更改为**4.6.1**。

    - 在 **"调试"** 选项卡上，在 **"开始外部程序"** 框中，键入**\<可视化工作室安装路径>_Common7_IDE_devenv.exe.**

         在**命令行参数**框中，键入 /**根缀 Exp**。

7. 更新以下引用：

    - 删除对微软的引用.VisualStudio.shell.9.0.dll，然后添加对微软的引用。

    - 删除对 Microsoft.VisualStudio.Package.语言服务.9.0.dll 的引用，然后添加对 Microsoft.VisualStudio.Package.语言服务.14.0.dll 的引用。

    - 添加对 Microsoft.VisualStudio.shell.Interop.10.0.dll 的引用。

8. 打开VsPkg.cs文件并将`DefaultRegistryRoot`属性的值更改为

    ```
    "Software\\Microsoft\\VisualStudio\\14.0Exp"
    ```

9. 原始示例不注册其语言服务，因此您必须向VsPkg.cs添加以下属性。

    ```
    [ProvideLanguageService(typeof(RegularExpressionLanguageService), "RegularExpressionLanguage", 0, RequestStockColors=true)]
    ```

10. 您必须添加源.扩展.vsixmanifest 文件。

    - 将此文件从现有扩展名复制到项目目录。 （获取此文件的一种方法是创建一个 VSIX 项目（在 **"文件**"下，单击 **"新建**"，然后单击 **"项目**"。 在"视觉基本"或"C#"下单击 **"可扩展性**"，然后选择**VSIX 项目**。

    - 将此文件添加到项目。

    - 在文件**的属性**中，将**生成操作**设置为 **"无**"。

    - 使用**VSIX 清单编辑器**打开文件。

    - 更改以下字段：

    - **ID**： RegExLangServ

    - **产品名称**： RegExLangServ

    - **说明**：正则表达式语言服务。

    - 在 **"资产**"下，单击 **"新建**"，选择"**键入****到 Microsoft.VisualStudio.VsPackage"，** 将**源**设置为**当前解决方案中的项目**，然后将**项目**设置为**RegExLangServ**。

    - 保存并关闭该文件。

11. 生成解决方案。 生成的文件部署到 **%USERPROFILE%\AppData_本地\微软_VisualStudio_14.0Exp_扩展\MSIT_RegExLangServ\\**。

12. 开始调试。 打开了视觉工作室的第二个实例。

## <a name="see-also"></a>请参阅
- [旧版语言服务扩展性](../../extensibility/internals/legacy-language-service-extensibility.md)
