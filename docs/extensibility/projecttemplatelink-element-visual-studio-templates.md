---
title: 项目模板链接元素（视觉工作室模板） |微软文档
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectTemplateLink
helpviewer_keywords:
- <ProjectTemplateLink> element [Visual Studio Templates]
- ProjectTemplateLink element [Visual Studio Templates]
ms.assetid: b0449111-8b48-45a1-a031-ea24b765e969
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e6d402b6605f2e01a20d400c2c33573c686a1cdd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701823"
---
# <a name="projecttemplatelink-element-visual-studio-templates"></a>ProjectTemplateLink 元素（Visual Studio 模板）
在多项目模板中指定一个项目的 *.vstemplate*文件的路径。

 \<VStemplate \<>模板内容\<>项目集合\<>项目模板链接> -\<或\<-模板>\<模板内容>\<项目集合>\<解决方案文件夹>项目模板链接>

## <a name="syntax"></a>语法

```xml
<ProjectTemplateLink ProjectName="Name">
    PathToTemplateFile
</ProjectTemplateLink>
```

## <a name="attributes-and-elements"></a>特性和元素
 以下各部分描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|`ProjectName`|可选特性。<br /><br /> 指定多项目模板中每一个项目的名称。 "**新项目**"对话框无法为各个项目分配名称。|
|`CopyParameters`|使主要组模板中的所有变量可复制到每个链接模板。<br /><br /> 链接模板中的参数具有前缀 `"$ext_*$"`。 `$projectname$`例如，如果在父组模板中参数具有值**示例Project1，** 当链接模板轮到执行时，它将从父组模板获取`$ext_projectname$``$projectname$`参数 ，该参数是参数的副本。<br /><br /> 这使链接模板能够共享一些只能在父组模板中方便地创建的公用参数。<br /><br /> 此特性为可选特性，未包含此特性时，它将自动默认为 `false`。<br /><br /> 在 Visual Studio 2013 Update 2 中引入。 要参考正确的产品版本，请参阅[Visual Studio 2013 SDK 更新 2 中提供的参考程序集](https://msdn.microsoft.com/library/42b65c3e-e42b-4c39-98c8-bea285f25ffb)。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[ProjectCollection](../extensibility/projectcollection-element-visual-studio-templates.md)|指定多项目模板的组织和内容。|
|[SolutionFolder](../extensibility/solutionfolder-element-visual-studio-templates.md)|对多项目模板中的项目进行分组。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 此文本指定模板的 *.vstemplate*文件的路径。

## <a name="remarks"></a>备注
 多项目模板用作两个或多个项目的容器。 该`ProjectTemplateLink`元素用于指定模板中一个项目的 *.vstemplate*文件的位置。 多项目模板的 *.vstemplate*文件包含模板中每个项目`ProjectTemplateLink`的一个元素。 有关多项目模板的详细信息，请参阅[如何：创建多项目模板](../ide/how-to-create-multi-project-templates.md)。

## <a name="example"></a>示例
 此示例显示一个简单的多项目根 *.vstemplate*文件。 在此示例中，模板包含两个项目：`My Windows Application` 和 `My Class Library`。 `ProjectName` 元素的 `ProjectTemplateLink` 特性可为 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 设置要分配给此项目的名称。 如果该`ProjectName`属性不存在，*则 .vstemplate*文件的名称将用作项目名称。

```
<VSTemplate Version="3.0.0" Type="ProjectGroup"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>Multi-Project Template Sample</Name>
        <Description>An example of a multi-project template</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>VisualBasic</ProjectType>
    </TemplateData>
    <TemplateContent>
        <ProjectCollection>
            <ProjectTemplateLink ProjectName="My Windows Application">
                WindowsApp\MyTemplate.vstemplate
            </ProjectTemplateLink>
            <ProjectTemplateLink ProjectName="My Class Library" CopyParameters="true">
                ClassLib\MyTemplate.vstemplate
            </ProjectTemplateLink>
        </ProjectCollection>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>请参阅
- [可视化工作室模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [如何：创建多项目模板](../ide/how-to-create-multi-project-templates.md)
