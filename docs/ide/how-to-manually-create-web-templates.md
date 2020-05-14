---
title: 创建 Web 模板
ms.date: 01/02/2018
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio templates, Web
- templates [Visual Studio], Web
- Web templates [Visual Studio]
- project templates [Visual Studio], Web
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 245b20dd9cad465129d6c79c38e53b6379c2c09c
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75591003"
---
# <a name="how-to-manually-create-web-templates"></a>如何：手动创建 Web 模板

创建 Web 模板与创建其他种类的模板不同。 由于 Web 项目模板出现在“添加新网站”  对话框中，并且 Web 项目项由编程语言分类，vstemplate  文件必须将模板指定为 Web 模板，并识别该编程语言。

> [!NOTE]
> Web 模板必须包含一个空的  .webproj 文件，并且必须在 *元素的* 属性的 vstemplate 文件中引用它`File``Project`。 尽管 Web 项目不需要 .proj  项目文件，但有必要创建此存根文件以便 Web 模板正确运行。

## <a name="to-manually-create-a-web-template"></a>手动创建 Web 模板

1. 创建 Web 项目。

2. 修改或删除项目中的文件，或将新文件添加到项目。

3. 创建 XML 文件，并用 vstemplate  文件扩展名将其保存在与项目相同的目录中。 不要将其添加到 Visual Studio 的项目中。

4. 编辑 vstemplate  XML 文件以提供项目模板元数据。 有关详细信息，请参阅[以下示例](#example)。

5. 查找 vstemplate`ProjectType`*文件中的* 元素，将文本值设置为 `Web`。

6. 在该 `ProjectType` 元素之后，添加 `ProjectSubType` 元素并将文本值设置为模板的编程语言。 编程语言可以是下列值之一：

   - CSharp
   - VisualBasic

     例如:

     ```xml
     <TemplateData>
       ...
       <ProjectType>Web</ProjectType>
       <ProjectSubType>CSharp</ProjectSubType>
       ...
     </TemplateData>
     ```

7. 选择模板中的文件（包括 vstemplate  文件），右键单击所选文件，然后选择“发送至”   > “压缩的文件夹”  。 这些文件会压缩到一个 .zip 文件中  。

8. 将该 .zip 模板文件放入 Visual Studio 项目模板目录  。 默认情况下，此目录为 %USERPROFILE%\Documents\Visual Studio *Version\<\ProjectTemplates\>* 。

## <a name="example"></a>示例

以下示例显示 Web 项目模板的基本 vstemplate  文件：

```xml
<VSTemplate Version="2.0.0" Type="Project"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyWebProjecStarterKit</Name>
        <Description>A simple web template</Description>
        <Icon>icon.ico</Icon>
        <ProjectType>Web</ProjectType>
        <ProjectSubType>CSharp</ProjectSubType>
        <DefaultName>WebSite</DefaultName>
    </TemplateData>
    <TemplateContent>
        <Project File="WebApplication.webproj">
            <ProjectItem>icon.ico</ProjectItem>
            <ProjectItem OpenInEditor="true">Default.aspx</ProjectItem>
            <ProjectItem>Default.aspx.cs</ProjectItem>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>另请参阅

- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [Visual Studio 模板架构引用（扩展性）](../extensibility/visual-studio-template-schema-reference.md)
