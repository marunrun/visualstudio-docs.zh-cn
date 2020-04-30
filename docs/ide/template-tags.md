---
title: 在项目模板上添加或编辑标签
description: 了解如何在 Visual Studio 的项目模板上添加或编辑标签。
ms.date: 04/30/2019
author: minsa110
ms.author: somin
manager: jillfra
ms.topic: reference
helpviewer_keywords:
- item templates, updating
- Visual Studio templates, updating
- project templates, updating
- updating templates [Visual Studio]
- template tagging, updating
- template tags, updating
ms.openlocfilehash: ef26a566229c228711ba6e57de50402df255c3dd
ms.sourcegitcommit: dab57cebd484228e6f0cf7ab1b9685c575410c06
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/25/2020
ms.locfileid: "82153027"
---
# <a name="add-tags-to-project-templates"></a>向项目模板添加标签

自 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/) 版本 16.1 预览版 2 起，可以向项目模板添加语言、平台和项目类型标签。 

“新建项目”  对话框中的两个位置使用了标签：

- 模板描述的下方将显示标签。

   ![“新建项目”对话框中带标签的项目模板](media/npd-item-with-template-tags.png)

- 可以借助标签搜索和筛选模板。

   ![在“新建项目”对话框中搜索和筛选](media/npd-search-and-filter.png)

可以通过更新 .vstemplate  XML 文件来添加标签。 可以使用内置到 Visual Studio 中的模板标签，也可以创建自定义模板标签。 仅在 Visual Studio 2019“新建项目”  对话框中显示模板标签。 模板标签不会影响模板在 Visual Studio 早期版本中的呈现效果。

## <a name="add-or-edit-tags"></a>添加或编辑标签

执行以下任意操作时，可能需要在项目模板的 .vstemplate  XML 中添加或编辑标签：

* 使用“导出模板”向导[创建新的项目模板](how-to-create-project-templates.md)。
* [更新现有项目模板](how-to-update-existing-templates.md)。
* [创建新的 VSIX 项目模板](../extensibility/getting-started-with-the-vsix-project-template.md)。

## <a name="syntax"></a>语法

```xml
<LanguageTag> Language Name </LanguageTag>
<PlatformTag> Platform Name </PlatformTag>
<ProjectTypeTag> Project Type </ProjectTypeTag>
```

## <a name="attributes"></a>特性

可以在高级用户场景中使用下面的可选属性：

|特性|描述|
|---------------|-----------------|
|`Package`|指定 Visual Studio 包 ID 的 GUID。|
|`ID`|指定 Visual Studio 资源 ID。|

语法：

```xml
<LanguageTag Package="{PackageID}" ID="ResourceID" />
<PlatformTag Package="{PackageID}" ID="ResourceID" />
<ProjectTypeTag Package="{PackageID}" ID="ResourceID" />
```

## <a name="elements"></a>元素

### <a name="child-elements"></a>子元素

无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|（必需）将此模板分类并定义此模板在  “新建项目”或“添加新项”  对话框中的显示方式。|

## <a name="text-value"></a>文本值

若未使用 `Package` 和 `ID` 属性，则必须提供文本值。

该文本提供模板的名称。

## <a name="built-in-tags"></a>内置标签

Visual Studio 提供了一系列内置标签。 添加内置标签时，标签将呈现本地化资源。 

以下列表显示在 Visual Studio 中可用的内置标签。 对应的值将显示在括号中。

| 语言标签 | 平台标签 | 项目类型标签 |
| -- | -- | -- |
| C++ (`cpp`) | Android (`android`) | 云 (`cloud`) |
| C# (`csharp`) | Azure (`azure`) | 控制台 (`console`) |
| F# (`fsharp`) | iOS (`ios`) | 桌面 (`desktop`) |
| Java (`java`) | Linux (`linux`) | 扩展 (`extension`) |
| JavaScript (`javascript`) | macOS (`macos`) | 游戏 (`games`) |
| Python (`python`) | tvOS (`tvos`) | IoT (`iot`) |
| 查询语言 (`querylanguage`) | Windows (`windows`) | 库 (`library`) |
| TypeScript (`typescript`) | Xbox (`xbox`) | 机器学习 (`machinelearning`) |
| Visual Basic (`visualbasic`) | | 移动 (`mobile`) |
| | | Office (`office`) |
| | | 其他 (`other`) |
| | | 服务 (`service`) |
| | | 测试 (`test`) |
| | | UWP (`uwp`) |
| | | Web (`web`) |

## <a name="example"></a>示例

下面的示例说明了 Visual C# 应用程序的项目模板的元数据：

```xml
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <LanguageTag>C#</LanguageTag>
        <PlatformTag>windows</PlatformTag>
        <PlatformTag>linux</PlatformTag>
        <PlatformTag>My Platform</PlatformTag>
        <ProjectTypeTag>console</ProjectTypeTag>
        <ProjectTypeTag>desktop</ProjectTypeTag>
    </TemplateData>
    <TemplateContent>
        <Project File="MyTemplate.csproj">
            <ProjectItem>Form1.cs<ProjectItem>
            <ProjectItem>Form1.Designer.cs</ProjectItem>
            <ProjectItem>Program.cs</ProjectItem>
            <ProjectItem>Properties\AssemblyInfo.cs</ProjectItem>
            <ProjectItem>Properties\Resources.resx</ProjectItem>
            <ProjectItem>Properties\Resources.Designer.cs</ProjectItem>
            <ProjectItem>Properties\Settings.settings</ProjectItem>
            <ProjectItem>Properties\Settings.Designer.cs</ProjectItem>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>请参阅

- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](creating-project-and-item-templates.md)
- [自定义项目和项模板](customizing-project-and-item-templates.md)
- [VSIX 项目模板入门](../extensibility/getting-started-with-the-vsix-project-template.md)
