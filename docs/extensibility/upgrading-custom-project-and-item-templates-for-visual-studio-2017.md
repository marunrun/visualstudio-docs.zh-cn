---
title: 升级 Visual Studio 2017 的自定义项目和项模板
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: ad02477b-e101-4f32-aeb7-292bf95d5c2f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 5f807e142b376d05e5a44600e8f6b24ddb3593be
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80698850"
---
# <a name="upgrade-custom-project-and-item-templates-for-visual-studio-2017"></a>升级自定义 Visual Studio 项目和项模板2017

从 Visual Studio 2017 开始，Visual Studio 会发现以不同方式通过其他方式安装到 Visual Studio 的项目和项模板。 如果你拥有使用自定义项目或项模板的扩展，则需要更新你的扩展。 本文介绍你必须执行的操作。

此更改仅影响 Visual Studio 2017。 它不会影响以前版本的 Visual Studio。

如果要创建项目或项模板作为 VSIX 扩展的一部分，请参阅 [创建自定义项目和项模板](../extensibility/creating-custom-project-and-item-templates.md)。

## <a name="template-scanning"></a>模板扫描

在以前版本的 Visual Studio 中， **devenv/setup** 或 **devenv/installvstemplates** 扫描了本地磁盘以查找项目和项模板。 从 Visual Studio 2017 开始，仅对用户级位置执行扫描。 默认用户级位置是 **%USERPROFILE%\Documents \\<Visual Studio version \> \Templates \\ **。 **Project**  >  如果在向导中选择 "**自动将模板导入 Visual Studio** " 选项，则此位置用于 "项目**导出模板 ...** " 命令生成的模板。

对于其他 (非用户) 位置，必须包括一个清单 ( vstman) 文件，该文件指定模板的位置和其他特性。 Vstman 文件随用于模板的 .vstemplate 文件一起生成。 如果使用 .vsix 安装扩展，则可以通过在 Visual Studio 2017 中重新编译扩展来实现此目的。 但如果使用 .msi，则需要手动进行更改。 有关进行这些更改所需执行的操作的列表，请参阅  **使用安装的扩展的升级。MSI** 。

## <a name="how-to-update-a-vsix-extension-with-project-or-item-templates"></a>如何使用项目或项模板更新 VSIX 扩展

1. 在 Visual Studio 2017 中打开解决方案。 系统会要求升级代码。 单击“确定”。

2. 升级完成后，可能需要更改安装目标的版本。 在 VSIX 项目中，打开 source.extension.vsixmanifest 文件，然后选择 " **安装目标** " 选项卡。如果 **版本范围** 字段为 **[14.0]**，请单击 " **编辑** " 并将其更改为包括 Visual Studio 2017。 例如，可以将其设置为 **[14.0，15.0]** ，将扩展安装到 visual studio 2015 或 visual studio 2017，或设置为 **[15.0]** ，以仅将其安装到 visual studio 2017。

3. 重新编译代码。

4. 关闭 Visual Studio。

5. 安装 VSIX。

6. 可以通过执行以下操作来测试更新：

    1. 文件扫描更改由以下注册表项激活：

         **reg add hklm\software\microsoft\visualstudio\15.0\VSTemplate/v DisableTemplateScanning/t REG_DWORD/d 1/reg：32**

    2. 添加密钥后，运行 **devenv/installvstemplates**。

    3. 重新打开 Visual Studio。 你应在预期位置找到你的模板。

    > [!NOTE]
    > 存在注册表项时，Visual Studio 扩展性项目模板不可用。 必须删除注册表项 (并重新运行 **devenv/installvstemplates**) 才能使用它们。

## <a name="other-recommendations-for-deploying-project-and-item-templates"></a>部署项目模板和项模板的其他建议

- 避免使用压缩的模板文件。 压缩的模板文件需要解压缩才能检索资源和内容，因此它们将越大使用。 相反，你应该将项目和项模板作为单独的文件部署在其自己的目录下以加速模板初始化。 对于 VSIX 扩展，SDK 生成任务将在创建 VSIX 文件时自动解压缩任何压缩的模板。

- 避免使用 "模板名称"、"说明"、"图标" 或 "预览" 的 "包/资源 ID" 条目，以避免在模板发现期间不必要地加载资源程序集。 相反，你可以使用本地化清单为每个区域设置（使用本地化名称或属性）创建模板条目。

- 如果将模板作为文件项包括在内，则清单生成可能不会给出预期的结果。 在这种情况下，必须将手动生成的清单添加到 VSIX 项目中。

## <a name="file-changes-in-project-and-item-templates"></a>项目和项模板中的文件更改
我们会显示模板文件的 Visual Studio 2015 和 Visual Studio 2017 版本之间的差异点，以便你可以正确地创建新文件。

 下面是 Visual Studio 2015 创建的默认项目 .vstemplate 文件：

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

 下面是 vstman 文件 (你可以在 VSIX 项目的清单目录) 中找到该文件，该目录是通过重新生成 VSIX 项目生成的：

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

 [TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)元素提供的信息保持不变。 **\<VSTemplateContainer>** 元素指向关联模板的 .vstemplate 文件。

 下面是 Visual Studio 2015 创建的默认项 .vstemplate 文件：

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

 下面是 vstman 文件 (你可以在 VSIX 项目的清单目录) 中找到该文件，该目录是通过重新生成 VSIX 项目生成的：

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

 元素提供的信息 **\<TemplateData>** 保持不变。 **\<VSTemplateContainer>** 元素指向关联模板的 .vstemplate 文件

 有关 vstman 文件的不同元素的详细信息，请参阅 [Visual Studio 模板清单架构参考](../extensibility/visual-studio-template-manifest-schema-reference.md)。

## <a name="upgrades-for-extensions-installed-with-an-msi"></a>升级使用安装的扩展。MSI

某些基于 MSI 的扩展将模板部署到常见模板位置，如以下目录：

- **\<Visual Studio installation directory>\Common7\IDE \\<ProjectTemplates/ItemTemplates\>**

- **\<Visual Studio installation directory>\Common7\IDE\Extensions \\<ExtensionName \> \\<项目/ItemTemplates\>**

如果扩展执行基于 MSI 的部署，则需要手动生成模板清单，并确保其包含在扩展设置中。 比较上面列出的 vstman 示例和 [Visual Studio 模板清单架构参考](../extensibility/visual-studio-template-manifest-schema-reference.md)。

为项目和项模板创建单独的清单，并应指向上面指定的根模板目录。 为每个扩展和区域设置创建一个清单。

## <a name="see-also"></a>另请参阅

- [模板发现疑难解答](troubleshooting-template-discovery.md)
- [创建自定义项目和项模板](creating-custom-project-and-item-templates.md)
