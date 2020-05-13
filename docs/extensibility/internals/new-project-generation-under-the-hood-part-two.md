---
title: 新项目生成：在引擎盖下，第二部分 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio], new project dialog
- projects [Visual Studio], new project generation
ms.assetid: 73ce91d8-0ab1-4a1f-bf12-4d3c49c01e13
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8692f2012e5f2733982f04e35a7fed415e49c636
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707019"
---
# <a name="new-project-generation-under-the-hood-part-two"></a>生成新项目：揭秘，第 2 部分

在["新项目生成：罩下"中，第一部分](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)我们看到了**新项目**对话框的填充方式。 假设您选择了**Visual C++ Windows 应用程序**，填写了 **"名称**和**位置**"文本框，然后单击"确定"。

## <a name="generating-the-solution-files"></a>生成解决方案文件
 选择应用程序模板[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]可指示解压缩并打开相应的 .vstemplate 文件，并启动模板来解释此文件中的 XML 命令。 这些命令在新解决方案或现有解决方案中创建项目和项目项。

 模板从保存 .vstemplate 文件的同一 .zip 文件夹中解压缩源文件（称为项目模板）。 模板将这些文件复制到新项目，并相应地对其进行自定义。

### <a name="template-parameter-replacement"></a>模板参数替换
 当模板将项目模板复制到新项目时，它将任何模板参数替换为用于自定义文件的字符串。 模板参数是一个特殊的标记，它前面是美元符号，例如，$date$。

 让我们看一下典型的项目项模板。 提取并检查程序文件\微软可视化工作室 8_Common7_IDE_项目模板_CSharp_Windows_1033_Windows应用程序.zip 文件夹中的Program.cs。

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

如果创建新的 Windows 应用程序项目名为"简单"，则模板将`$safeprojectname$`参数替换为项目的名称。

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

## <a name="a-look-inside-a-vstemplate-file"></a>A 看 内部 。VSTemplate 文件
 基本 .vstemplate 文件具有此格式

```xml
<VSTemplate Version="2.0.0"     xmlns="http://schemas.microsoft.com/developer/vstemplate/2005"     Type="Project">
    <TemplateData>
    </TemplateData>
    <TemplateContent>
    </TemplateContent>
</VSTemplate>
```

 我们查看了"\<新项目生成"中的模板数据>部分[：在胡德下，第一部分](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)。 本节中的标记用于控制 **"新项目"** 对话框的外观。

 \<模板内容>部分中的标记控制新项目和项目项的生成。 下面是[程序文件\<]微软可视化工作室 8_Common7_PROJECTTemplate_CSharp_Windows_1033_Windows应用程序.zip 文件夹中的 cwindows 应用程序.vstemplate 文件中的模板内容>部分。

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

 项目\<>标记控制项目的生成，\<而项目项>标记控制项目项的生成。 如果参数替换参数为 true，模板将自定义项目文件或项中的所有模板参数。 在这种情况下，除"设置.设置"外，所有项目项都是自定义的。

 TargetFileName 参数指定结果项目文件或项的名称和相对路径。 这允许您为项目创建文件夹结构。 如果不指定此参数，项目项的名称将与项目项模板相同。

 生成的 Windows 应用程序文件夹结构如下所示：

 ![SimpleSolution](../../extensibility/internals/media/simplesolution.png "SimpleSolution")

 模板中的第一\<个也是唯一的项目>标记如下：

```xml
<Project File="WindowsApplication.csproj" ReplaceParameters="true">
```

 这指示新项目模板通过复制和自定义模板项 windows 应用程序.csproj 来创建 Simple.csproj 项目文件。

### <a name="designers-and-references"></a>设计师和参考资料
 您可以在解决方案资源管理器中看到"属性"文件夹存在并包含预期文件。 但是，项目引用和设计器文件依赖项（如对 Resources.resx Resources.Designer.cs和Form1.csForm1.Designer.cs）又如何呢？  生成时，这些文件将设置在 Simple.csproj 文件中。

 下面是创建项目引用\<的 Simple.csproj 的 ItemGroup>：

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

 您可以看到，这些是解决方案资源管理器中显示的六个项目引用。 下面是另\<一个项目组>的一节。 为了清楚起见，删除了许多行代码。 此部分使Settings.Designer.cs取决于设置设置：

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
