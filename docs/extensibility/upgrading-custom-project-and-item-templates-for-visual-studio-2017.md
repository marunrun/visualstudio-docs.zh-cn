---
title: 升级 Visual Studio 2017 的自定义项目和项目模板
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698850"
---
# <a name="upgrade-custom-project-and-item-templates-for-visual-studio-2017"></a>升级可视化工作室 2017 的自定义项目和项目模板

从 Visual Studio 2017 开始，Visual Studio 会发现由 .vsix 或 .msi 以不同于早期版本的 Visual Studio 安装的项目和项目模板。 如果您拥有使用自定义项目或项目模板的扩展，则需要更新扩展。 本文介绍了您必须做什么。

此更改仅影响 Visual Studio 2017。 它不会影响早期版本的 Visual Studio。

如果要创建项目或项目模板作为 VSIX 扩展的一部分，请参阅[创建自定义项目和项目模板](../extensibility/creating-custom-project-and-item-templates.md)。

## <a name="template-scanning"></a>模板扫描

在 Visual Studio 的早期版本中 **，devenv /安装程序**或**devenv /installvstemplate**扫描本地磁盘以查找项目和项目模板。 从 Visual Studio 2017 开始，扫描仅针对用户级位置执行。 默认用户级位置是 **%USERPROFILE%%\文档\\<可视化工作室版本\>\Templates\\**。 如果向导中选择了 **"自动将模板导入 Visual Studio"** 选项，则此位置用于由**项目** > **导出模板..."** 命令生成的模板。

对于其他（非用户）位置，必须包含一个清单（.vstman）文件，该文件指定模板的位置和其他特征。 .vstman 文件与用于模板的 .vstemplate 文件一起生成。 如果使用 .vsix 安装扩展，则可以通过在 Visual Studio 2017 中重新编译扩展来实现此目的。 但是，如果您使用 .msi，则需要手动进行更改。 有关进行这些更改需要执行哪些操作的列表，请参阅使用 安装 的**扩展的升级。MSI**稍后在本页。

## <a name="how-to-update-a-vsix-extension-with-project-or-item-templates"></a>如何使用项目或项目模板更新 VSIX 扩展

1. 在 Visual Studio 2017 中打开解决方案。 系统将要求您升级代码。 单击“确定”。

2. 升级完成后，您可能需要更改安装目标的版本。 在 VSIX 项目中，打开源.扩展.vsixmanifest 文件并选择"**安装目标**"选项卡。如果 **"版本范围"** 字段为 **[14.0]，** 请单击 **"编辑"** 并将其更改为包括 Visual Studio 2017。 例如，您可以将其设置为 **{14.0，15.0}** 以将扩展安装到 Visual Studio 2015 或 Visual Studio 2017，或者将其设置为 **[15.0]** 以将其安装到 Visual Studio 2017。

3. 重新编译代码。

4. 关闭 Visual Studio。

5. 安装 VSIX。

6. 您可以通过执行以下操作来测试更新：

    1. 文件扫描更改由以下注册表项激活：

         **reg 添加 hklm_software_microsoft_visualstudio_15.0_VSTemplate /v 禁用模板扫描 /t REG_DWORD /d 1 /reg：32**

    2. 添加密钥后，运行**devenv /installvstemplate。**

    3. 重新打开视觉工作室。 您应该在预期位置找到模板。

    > [!NOTE]
    > 当注册表项存在时，Visual Studio 扩展性项目模板不可用。 您必须删除注册表项（并重新运行**devenv /installvstemplate）** 才能使用它们。

## <a name="other-recommendations-for-deploying-project-and-item-templates"></a>部署项目和项目模板的其他建议

- 避免使用压缩模板文件。 压缩模板文件需要取消压缩才能检索资源和内容，因此它们使用成本更高。 相反，应将项目和项目模板部署为其目录下的单个文件，以加快模板初始化。 对于 VSIX 扩展，SDK 生成任务将在创建 VSIX 文件时自动解压缩任何压缩模板。

- 避免对模板名称、说明、图标或预览使用包/资源 ID 条目，以避免在模板发现期间加载不必要的资源程序集。 相反，您可以使用本地化的清单为每个区域设置创建模板条目，该区域设置使用本地化的名称或属性。

- 如果将模板作为文件项包含，则清单生成可能不会为您提供预期的结果。 在这种情况下，您必须向 VSIX 项目添加手动生成的清单。

## <a name="file-changes-in-project-and-item-templates"></a>项目和项目模板中的文件更改
我们显示 Visual Studio 2015 和 Visual Studio 2017 版本的模板文件之间的差异点，以便您可以正确创建新文件。

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

 下面是由重建 VSIX 项目产生的 .vstman 文件（您可以在 VSIX 项目的清单目录中找到它）：

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

 [模板数据](../extensibility/templatedata-element-visual-studio-templates.md)元素提供的信息保持不变。 VSTemplate 容器>元素指向关联模板的 .vstemplate 文件。 ** \<**

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

 下面是由重建 VSIX 项目产生的 .vstman 文件（您可以在 VSIX 项目的清单目录中找到它）：

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

 模板数据>元素提供的信息保持不变。 ** \<** VSTemplate 容器>元素指向关联模板的 .vstemplate 文件**\<**

 有关 .vstman 文件的不同元素的详细信息，请参阅[可视化工作室模板清单架构参考](../extensibility/visual-studio-template-manifest-schema-reference.md)。

## <a name="upgrades-for-extensions-installed-with-an-msi"></a>使用 安装的扩展的升级。微星

某些基于 MSI 的扩展将模板部署到常见的模板位置，例如以下目录：

- **\<可视化工作室安装目录>_通用7_IDE<\\项目模板/项目模板\>**

- **\<可视化工作室安装目录>_Common7_IDE_扩展\\<扩展名称\>\\<项目/项目模板\>**

如果扩展执行基于 MSI 的部署，则需要手动生成模板清单，并确保模板包含在扩展设置中。 比较上面列出的 .vstman 示例和[可视化工作室模板清单架构参考](../extensibility/visual-studio-template-manifest-schema-reference.md)。

为项目和项目模板创建单独的清单，它们应指向上面指定的根模板目录。 每个扩展和区域设置创建一个清单。

## <a name="see-also"></a>请参阅

- [故障排除模板发现](troubleshooting-template-discovery.md)
- [创建自定义项目和项目模板](creating-custom-project-and-item-templates.md)
