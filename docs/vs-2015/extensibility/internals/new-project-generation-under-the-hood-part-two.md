---
title: 新项目生成：在幕后，第二部分 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio], new project dialog
- projects [Visual Studio], new project generation
ms.assetid: 73ce91d8-0ab1-4a1f-bf12-4d3c49c01e13
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6643c52ff8e5801c562524e99c4e3f03c00f74b9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687484"
---
# <a name="new-project-generation-under-the-hood-part-two"></a>生成新项目：揭秘，第 2 部分
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在 ["新项目生成](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md) " 中：在幕后，我们看到了一个 " **新建项目** " 对话框的填充方式。 假设您已经选择了一个 **Visual c # Windows 应用程序**，填充了 " **名称** " 和 " **位置** " 文本框，然后单击 "确定"。  
  
## <a name="generating-the-solution-files"></a>生成解决方案文件  
 选择应用程序模板 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 将指示解压缩并打开相应的 .vstemplate 文件，并启动一个模板来解释此文件中的 XML 命令。 这些命令在新的或现有的解决方案中创建项目和项目项。  
  
 包含 .vstemplate 文件的相同 .zip 文件夹中的模板解压缩源文件，称为项模板。 模板将这些文件复制到新项目，并相应地对其进行自定义。 有关项目和项模板的概述，请参阅 [笔尖： Visual Studio 模板](https://msdn.microsoft.com/141fccaa-d68f-4155-822b-27f35dd94041)。  
  
### <a name="template-parameter-replacement"></a>模板参数替换  
 当模板将项模板复制到新的项目时，它会将任何模板参数替换为字符串，以自定义该文件。 模板参数是一种特殊的标记，该标记前面和后面跟有美元符号，例如 $date $。  
  
 让我们看一看典型的项目项模板。 提取并检查 Program Files\Microsoft Visual Studio 8\Common7\IDE\ProjectTemplates\CSharp\Windows\1033\WindowsApplication.zip 文件夹中的 Program.cs。  
  
```  
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
  
 如果创建名为 Simple 的新 Windows 应用程序项目，则模板会将参数替换为 `$safeprojectname$` 项目的名称。  
  
```  
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
  
## <a name="a-look-inside-a-vstemplate-file"></a>中的外观。.Vstemplate 文件  
 基本的 .vstemplate 文件具有此格式  
  
```  
<VSTemplate Version="2.0.0"     xmlns="http://schemas.microsoft.com/developer/vstemplate/2005"     Type="Project">  
    <TemplateData>  
    </TemplateData>  
    <TemplateContent>  
    </TemplateContent>  
</VSTemplate>  
```  
  
 我们查看 \<TemplateData> 了 [新项目生成中的部分：在幕后，第一部分](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)。 本节中的标记用于控制 " **新建项目** " 对话框的外观。  
  
 部分中的标记 \<TemplateContent> 控制新项目和项目项的生成。 下面是 \<TemplateContent> \Program Files\Microsoft Visual Studio 8\Common7\IDE\ProjectTemplates\CSharp\Windows\1033\WindowsApplication.zip 文件夹中 cswindowsapplication 文件的部分。  
  
```  
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
  
 \<Project>标记控制项目的生成， \<ProjectItem> 标记控制项目项的生成。 如果参数 ReplaceParameters 为 true，则模板将自定义项目文件或项中的所有模板参数。 在这种情况下，将自定义除 Settings 之外的所有项目项。  
  
 TargetFileName 参数指定生成的项目文件或项的名称和相对路径。 这使你可以为项目创建文件夹结构。 如果未指定此参数，则项目项的名称将与项目项模板的名称相同。  
  
 生成的 Windows 应用程序文件夹结构如下所示：  
  
 ![SimpleSolution](../../extensibility/internals/media/simplesolution.png "SimpleSolution")  
  
 模板中的第一个和唯一的 \<Project> 标记将读取：  
  
```  
<Project File="WindowsApplication.csproj" ReplaceParameters="true">  
```  
  
 这将指示新项目模板通过复制并自定义模板项 windowsapplication.zip 来创建简单的 .csproj 项目文件。  
  
### <a name="designers-and-references"></a>设计器和引用  
 可以在解决方案资源管理器中看到 "属性" 文件夹存在并且包含所需的文件。 但项目引用和设计器文件依赖项（例如 Resources.Designer.cs 和 Form1.cs 的 Form1.Designer.cs）呢？  它们是在生成时在简单的 .csproj 文件中设置的。  
  
 下面是 \<ItemGroup> 从简单的 .csproj 创建项目引用：  
  
```  
<ItemGroup>  
    <Reference Include="System" />  
    <Reference Include="System.Data" />  
    <Reference Include="System.Deployment" />  
    <Reference Include="System.Drawing" />  
    <Reference Include="System.Windows.Forms" />  
    <Reference Include="System.Xml" />  
</ItemGroup>  
```  
  
 您可以看到，这是解决方案资源管理器中显示的六个项目引用。 下面是另一个部分 \<ItemGroup> 。 为清楚起见，已经删除了许多代码行。 此部分使 Settings.Designer.cs 依赖于设置。设置：  
  
```  
<ItemGroup>  
    <Compile Include="Properties\Settings.Designer.cs">  
        <DependentUpon>Settings.settings</DependentUpon>  
    </Compile>  
</ItemGroup>  
```  
  
## <a name="see-also"></a>另请参阅  
 [生成新项目：揭秘，第 1 部分](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)  
 [MSBuild](../../msbuild/msbuild.md)
