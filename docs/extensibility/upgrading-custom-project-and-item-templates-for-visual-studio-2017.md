---
title: 升级 Visual Studio 2017 的自定义项目和项模板
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: ad02477b-e101-4f32-aeb7-292bf95d5c2f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: d375dfc4a53015f57546f7cbfcc8b940fa81bd0b
ms.sourcegitcommit: 74c5360186731de07828764eb32ea1033a8c2275
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2019
ms.locfileid: "67559757"
---
# <a name="upgrade-custom-project-and-item-templates-for-visual-studio-2017"></a>升级自定义项目和项模板的 Visual Studio 2017

从 Visual Studio 2017 开始，Visual Studio 发现由.vsix 或.msi 安装在不同的方式与以前版本的 Visual Studio 中的项目和项模板。 如果你拥有使用自定义项目或项模板的扩展，您需要更新你的扩展。 本文介绍了必须执行的操作。

此更改会影响 Visual Studio 2017。 它不会影响 Visual Studio 的早期版本。

如果你想要创建项目或项模板作为 VSIX 扩展的一部分，请参阅[创建自定义项目和项模板](../extensibility/creating-custom-project-and-item-templates.md)。

## <a name="template-scanning"></a>扫描的模板

在以前版本的 Visual Studio 中， **devenv /setup**或**devenv /installvstemplates**扫描以查找项目和项模板的本地磁盘。 从 Visual Studio 2017 中，扫描仅对于用户级别位置的执行。 默认用户级位置是 **%USERPROFILE%\Documents\\< Visual Studio 版本\>\Templates\\** 。 此位置用于生成的模板**项目** > **导出模板...** 命令时，如果**会自动将模板导入 Visual Studio**在向导中选择选项。

对于其他 （非用户） 的位置，您必须包含指定的位置和模板的其他特征的 manifest(.vstman) 文件。 适用于模板的.vstemplate 文件以及生成.vstman 文件。 如果您安装使用.vsix 扩展，可以通过重新编译 Visual Studio 2017 中的扩展来实现此目的。 但如果您使用一个.msi，则需要手动进行的更改。 您需要执行的操作进行这些更改的列表，请参阅**对扩展安装与升级。MSI**稍后在此页。

## <a name="how-to-update-a-vsix-extension-with-project-or-item-templates"></a>如何使用项目或项模板更新 VSIX 扩展

1. 在 Visual Studio 2017 中打开的解决方案。 你将需要升级的代码。 单击 **“确定”** 。

2. 在升级完成后，你可能需要更改安装目标版本。 在 VSIX 项目中，打开 source.extension.vsixmanifest 文件，然后选择**安装目标**选项卡。如果**版本范围**字段是 **[14.0]** ，单击**编辑**并将其更改为包括 Visual Studio 2017。 例如，您可以将其设置为 **[14.0,15.0]** 到 Visual Studio 2015 或 Visual Studio 2017，或安装扩展 **[15.0]** 以将其安装到只需使用 Visual Studio 2017。

3. 重新编译代码。

4. 关闭 Visual Studio。

5. 安装 VSIX。

6. 可以通过执行以下操作来测试更新：

    1. 扫描更改的文件被激活由以下注册表项：

         **reg 添加 hklm\software\microsoft\visualstudio\15.0\VSTemplate /v DisableTemplateScanning /t REG_DWORD /d 1 /reg:32**

    2. 添加密钥后，运行**devenv /installvstemplates**。

    3. 重新打开 Visual Studio。 应该在预期位置中找到你的模板。

    > [!NOTE]
    > 存在注册表项时，Visual Studio 扩展性项目模板不可用。 必须删除注册表项 (和重新运行**devenv /installvstemplates**) 来使用它们。

## <a name="other-recommendations-for-deploying-project-and-item-templates"></a>部署项目和项模板的其他建议

- 避免使用压缩的模板文件。 压缩需要不会进行压缩以便检索资源和内容文件的模板，因此它们将考虑使用。 相反，应将项目和项模板部署为单个文件，以加快模板初始化其自身目录下。 VSIX 扩展的 SDK 生成任务会自动将任何压缩的模板解压缩创建 VSIX 文件时。

- 避免使用包/资源 ID 条目的模板名称、 说明、 图标，或为模板在发现期间避免不必要的资源程序集加载预览。 相反，本地化的清单可用于创建每个区域设置，它使用本地化的名称或属性的模板条目。

- 如果要包含为文件项模板，清单生成可能无法让你预期的结果。 在这种情况下，必须向 VSIX 项目添加一个手动生成的清单。

## <a name="file-changes-in-project-and-item-templates"></a>项目和项模板中的文件更改
我们显示 Visual Studio 2015 和 Visual Studio 2017 版本的模板文件之间差异的点，以便可以正确地创建新文件。

 下面是 Visual Studio 2015 创建的默认项目.vstemplate 文件：

```xml
<?xml version="1.0" encoding="utf-8"?>
<VSTemplate Version="3.0.0" Type="Project" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:sdk="http://schemas.microsoft.com/developer/vstemplate-sdkextension/2010">
  <TemplateData>
    <Name>ProjectTemplate1</Name>
    <Description>ProjectTemplate1</Description>
    <Icon>ProjectTemplate1.ico</Icon>
    <ProjectType>CSharp</ProjectType>
    <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
    <SortOrder>1000</SortOrder>
    <TemplateID>05b79cc9-2146-4716-a8e5-7e085cdd2221</TemplateID>
    <CreateNewFolder>true</CreateNewFolder>
    <DefaultName>ProjectTemplate1</DefaultName>
    <ProvideDefaultName>true</ProvideDefaultName>
  </TemplateData>
  <TemplateContent>
    <Project File="ProjectTemplate.csproj" ReplaceParameters="true">
      <ProjectItem ReplaceParameters="true" TargetFileName="Properties\AssemblyInfo.cs">AssemblyInfo.cs</ProjectItem>
      <ProjectItem ReplaceParameters="true" OpenInEditor="true">Class1.cs</ProjectItem>
    </Project>
  </TemplateContent>
</VSTemplate>

```

 下面是从重新生成的 VSIX 项目生成.vstman 文件 （可以在 VSIX 项目的清单目录中找到它）：

```xml
<VSTemplateManifest Version="1.0" Locale="1033" xmlns="http://schemas.microsoft.com/developer/vstemplatemanifest/2015">
  <VSTemplateContainer TemplateType="Project">
    <RelativePathOnDisk>CSharp\1033\ProjectTemplate1</RelativePathOnDisk>
    <TemplateFileName>ProjectTemplate1.vstemplate</TemplateFileName>
    <VSTemplateHeader>
      <TemplateData xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
        <Name>ProjectTemplate1</Name>
        <Description>ProjectTemplate1</Description>
        <Icon>ProjectTemplate1.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
        <SortOrder>1000</SortOrder>
        <TemplateID>05b79cc9-2146-4716-a8e5-7e085cdd2221</TemplateID>
        <CreateNewFolder>true</CreateNewFolder>
        <DefaultName>ProjectTemplate1</DefaultName>
        <ProvideDefaultName>true</ProvideDefaultName>
      </TemplateData>
    </VSTemplateHeader>
  </VSTemplateContainer>
</VSTemplateManifest>

```

 提供的信息[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)元素保持不变。 **\<VSTemplateContainer >** 元素指向关联的模板的.vstemplate 文件。

 下面是由 Visual Studio 2015 创建的默认项.vstemplate 文件：

```xml
<?xml version="1.0" encoding="utf-8"?>
<VSTemplate Version="3.0.0" Type="Item" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:sdk="http://schemas.microsoft.com/developer/vstemplate-sdkextension/2010">
  <TemplateData>
    <Name>ItemTemplate1</Name>
    <Description>ItemTemplate1</Description>
    <Icon>ItemTemplate1.ico</Icon>
    <TemplateID>bfeadf8e-a251-4109-b605-516b88e38c8d</TemplateID>
    <ProjectType>CSharp</ProjectType>
    <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
    <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
    <DefaultName>Class.cs</DefaultName>
  </TemplateData>
  <TemplateContent>
    <References>
      <Reference>
        <Assembly>System</Assembly>
      </Reference>
    </References>
    <ProjectItem ReplaceParameters="true">Class.cs</ProjectItem>
  </TemplateContent>
</VSTemplate>

```

 下面是从重新生成的 VSIX 项目生成.vstman 文件 （可以在 VSIX 项目的清单目录中找到它）：

```xml
<VSTemplateManifest Version="1.0" Locale="1033" xmlns="http://schemas.microsoft.com/developer/vstemplatemanifest/2015">
  <VSTemplateContainer TemplateType="Item">
    <RelativePathOnDisk>CSharp\1033\ItemTemplate1</RelativePathOnDisk>
    <TemplateFileName>ItemTemplate1.vstemplate</TemplateFileName>
    <VSTemplateHeader>
      <TemplateData xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
        <Name>ItemTemplate1</Name>
        <Description>ItemTemplate1</Description>
        <Icon>ItemTemplate1.ico</Icon>
        <TemplateID>bfeadf8e-a251-4109-b605-516b88e38c8d</TemplateID>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
        <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
        <DefaultName>Class.cs</DefaultName>
      </TemplateData>
    </VSTemplateHeader>
  </VSTemplateContainer>
</VSTemplateManifest>
```

 提供的信息 **\<TemplateData >** 元素保持不变。 **\<VSTemplateContainer >** 元素指向关联的模板的.vstemplate 文件

 有关.vstman 文件的不同元素的详细信息，请参阅[Visual Studio 模板清单架构参考](../extensibility/visual-studio-template-manifest-schema-reference.md)。

## <a name="upgrades-for-extensions-installed-with-an-msi"></a>与安装扩展的升级。MSI

某些基于 MSI 的扩展插件将模板部署到常见的模板位置，例如在以下目录：

- **\<Visual Studio 安装目录 > \Common7\IDE\\< ProjectTemplates/项模板\>**

- **\<Visual Studio 安装目录 > \Common7\IDE\Extensions\\< ExtensionName\>\\< 项目/项模板\>**

如果你的扩展执行的基于 MSI 的部署，需要手动生成模板清单，并确保它包含在扩展安装程序中。 比较上面列出的.vstman 示例和[Visual Studio 模板清单架构参考](../extensibility/visual-studio-template-manifest-schema-reference.md)。

创建单独的项目和项模板清单，它们应指向根模板目录指定更高版本。 创建一个清单，每个扩展和区域设置。

## <a name="see-also"></a>请参阅

- [模板发现疑难解答](troubleshooting-template-discovery.md)
- [创建自定义项目和项模板](creating-custom-project-and-item-templates.md)
