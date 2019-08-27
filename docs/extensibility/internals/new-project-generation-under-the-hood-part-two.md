---
title: 生成新项目：实质上，第二部分 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio], new project dialog
- projects [Visual Studio], new project generation
ms.assetid: 73ce91d8-0ab1-4a1f-bf12-4d3c49c01e13
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4ea614be39456f5d6a31ea6c9c12221b4db09bbd
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66311009"
---
# <a name="new-project-generation-under-the-hood-part-two"></a>生成新项目：揭秘，第 2 部分

在[生成新项目：实质上，第一部分](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)我们已了解如何**新建项目**填充框的对话框。 让我们假定你已选择了**Visual C# Windows 应用程序**中，已填写**名称**并**位置**文本框中，然后单击确定。

## <a name="generating-the-solution-files"></a>生成解决方案文件
 选择应用程序模板会将定向[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]解压缩，然后打开相应的.vstemplate 文件，并启动一个模板来解释此文件中的 XML 命令。 这些命令创建新的或现有解决方案中项目和项目项。

 该模板解压缩源文件，保存.vstemplate 文件的同一个.zip 文件夹从调用项模板。 该模板将这些文件复制到新项目中，相应地自定义它们。

### <a name="template-parameter-replacement"></a>模板参数替换
 模板复制到新的项目项模板，它也将与字符串以自定义文件中替换任何模板参数。 模板参数是一个特殊的标记，是前面和后面一个美元符号，例如、 $date$。

 让我们看一下典型的项目项模板。 提取并检查 Program.cs Program Files\Microsoft Visual Studio 8\Common7\IDE\ProjectTemplates\CSharp\Windows\1033\WindowsApplication.zip 文件夹中。

```csharp
using System;
using System.Collections.Generic;
using System.Windows.Forms;

namespace $safeprojectname$
{
    static class Program
    {
        // source code deleted here for brevity
    }
}
```

如果您创建一个新的名为简单的 Windows 应用程序项目，该模板将替换`$safeprojectname$`参数与项目的名称。

```csharp
using System;
using System.Collections.Generic;
using System.Windows.Forms;

namespace Simple
{
    static class Program
    {
        // source code deleted here for brevity
    }
}
```

 有关模板参数的完整列表，请参阅[模板参数](../../ide/template-parameters.md)。

## <a name="a-look-inside-a-vstemplate-file"></a>深入介绍。VSTemplate 文件
 基本.vstemplate 文件的格式

```xml
<VSTemplate Version="2.0.0"     xmlns="http://schemas.microsoft.com/developer/vstemplate/2005"     Type="Project">
    <TemplateData>
    </TemplateData>
    <TemplateContent>
    </TemplateContent>
</VSTemplate>
```

 我们会学会\<TemplateData > 部分中[生成新项目：实质上，第一部分](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)。 在本部分中的标记用于控制的外观**新的项目**对话框。

 中的标记\<TemplateContent > 部分的新项目和项目项生成的控件。 下面是\<TemplateContent > \Program Files\Microsoft Visual Studio 8\Common7\IDE\ProjectTemplates\CSharp\Windows\1033\WindowsApplication.zip 文件夹中的 cswindowsapplication.vstemplate 文件中的部分。

```xml
<TemplateContent>
  <Project File="WindowsApplication.csproj" ReplaceParameters="true">
    <ProjectItem ReplaceParameters="true"
      TargetFileName="Properties\AssemblyInfo.cs">
      AssemblyInfo.cs
    </ProjectItem>
    <ProjectItem TargetFileName="Properties\Resources.resx">
      Resources.resx
    </ProjectItem>
    <ProjectItem ReplaceParameters="true"       TargetFileName="Properties\Resources.Designer.cs">
      Resources.Designer.cs
    </ProjectItem>
    <ProjectItem TargetFileName="Properties\Settings.settings">
      Settings.settings
    </ProjectItem>
    <ProjectItem ReplaceParameters="true"       TargetFileName="Properties\Settings.Designer.cs">
      Settings.Designer.cs
    </ProjectItem>
    <ProjectItem ReplaceParameters="true" OpenInEditor="true">
      Form1.cs
    </ProjectItem>
    <ProjectItem ReplaceParameters="true">
      Form1.Designer.cs
    </ProjectItem>
    <ProjectItem ReplaceParameters="true">
      Program.cs
    </ProjectItem>
  </Project>
</TemplateContent>
```

 \<项目 > 标记，控制项目的生成和\<ProjectItem > 标记，控制项目项的生成。 如果参数 ReplaceParameters 为 true，该模板将自定义项的项目文件中的所有模板参数。 在这种情况下，所有项目项是自都定义，但 Settings.settings 除外。

 TargetFileName 参数指定的名称和生成的项目文件或项的相对路径。 这允许您创建您的项目的文件夹结构。 如果未指定此参数，项目项将具有与项目项模板相同的名称。

 生成 Windows 应用程序文件夹结构如下所示：

 ![SimpleSolution](../../extensibility/internals/media/simplesolution.png "SimpleSolution")

 第一个且仅\<项目 > 模板读取的标记：

```xml
<Project File="WindowsApplication.csproj" ReplaceParameters="true">
```

 这会指示要通过复制和自定义模板项 windowsapplication.csproj 创建 Simple.csproj 项目文件的新项目模板。

### <a name="designers-and-references"></a>设计器和引用
 在解决方案资源管理器中，您可以看到属性文件夹存在且包含预期的文件。 但什么有关项目引用，并且设计器文件依赖项，如 Resources.resx，到 Resources.Designer.cs 和到 Form1.cs Form1.Designer.cs？  这些设置在 Simple.csproj 文件在生成时。

 下面是\<ItemGroup > 从 Simple.csproj 创建的项目引用：

```xml
<ItemGroup>
    <Reference Include="System" />
    <Reference Include="System.Data" />
    <Reference Include="System.Deployment" />
    <Reference Include="System.Drawing" />
    <Reference Include="System.Windows.Forms" />
    <Reference Include="System.Xml" />
</ItemGroup>
```

 您可以看到，这些是在解决方案资源管理器中显示的六个项目引用。 以下是从另一个部分\<ItemGroup >。 为清楚起见，多行代码已被删除。 本部分使 Settings.Designer.cs Settings.settings 依赖于：

```xml
<ItemGroup>
    <Compile Include="Properties\Settings.Designer.cs">
        <DependentUpon>Settings.settings</DependentUpon>
    </Compile>
</ItemGroup>
```

## <a name="see-also"></a>请参阅

- [生成新项目：揭秘，第 1 部分](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)
- [MSBuild](../../msbuild/msbuild.md)