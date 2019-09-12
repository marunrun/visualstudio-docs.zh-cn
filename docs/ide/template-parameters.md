---
title: 项目和项模板参数
ms.date: 01/02/2018
ms.topic: reference
helpviewer_keywords:
- Visual Studio templates, parameters
- template parameters [Visual Studio]
- project templates, parameters
- item templates, parameters
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 2fbc9d95a6e334c3dcd788c4b686a222c417b0df
ms.sourcegitcommit: 0f44ec8ba0263056ad04d2d0dc904ad4206ce8fc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2019
ms.locfileid: "70766115"
---
# <a name="template-parameters"></a>模板参数

实例化模板时，可替换模板中的值。 若要设置此功能，请使用模板参数  。 模板参数可用于替换值，例如模板中的类名和命名空间。 当用户添加新项或项目时，后台运行的模板向导会替换这些参数。

## <a name="declare-and-enable-template-parameters"></a>声明和启用模板参数

模板参数以 $参数$ 的格式进行声明  。 例如:

- $safeprojectname$

- $guid1$

- $guid5$

### <a name="enable-parameter-substitution-in-templates"></a>在模板中启用参数替换

1. 在模板的 .vstemplate  文件中，找到与要为之启用参数替换的项对应的 `ProjectItem` 元素。

1. 将 `ReplaceParameters` 元素的 `ProjectItem` 属性设置为 `true`。

1. 在项目项的代码文件中，在适当位置上包括参数。 例如，以下参数指定安全项目名称用于文件中的命名空间：

    ```csharp
    namespace $safeprojectname$
    ```

## <a name="reserved-template-parameters"></a>保留的模板参数

下表列出可供任何模板使用的保留的模板参数：

|参数|说明|
|---------------|-----------------|
|clrversion|公共语言运行时 (CLR) 的当前版本。|
|ext_*|将 `ext_` 前缀添加到任何参数，以引用父模板的变量。 例如 `ext_safeprojectname`。|
|guid[1-10]|一个用于替换项目文件中的项目 GUID 的 GUID。 可指定最多 10 个唯一的 GUID（例如，`guid1`）。|
|itemname|在其中使用参数的文件的名称。|
|machinename|当前的计算机名称（例如，Computer01）。|
|projectname|创建项目时由用户提供的名称。|
|registeredorganization|来自 HKLM\Software\Microsoft\Windows NT\CurrentVersion\RegisteredOrganization 的注册表项值。|
|rootnamespace|当前项目的根命名空间。 此参数仅适用于项模板。|
|safeitemname|与 `itemname` 相同，但所有不安全字符和空格替换为了下划线。|
|safeitemrootname|与 `safeitemname` 相同。|
|safeprojectname|用户在创建项目时提供的名称，但名称中删除了所有不安全字符和空格。|
|time|以 DD/MM/YYYY 00:00:00 格式表示的当前时间。|
|specifiedSolutionName|解决方案的名称。 在选中“创建解决方案目录”时，`specifiedSolutionName` 具有解决方案名称。 在未选中“创建解决方案目录”时，`specifiedSolutionName` 为空。|
|userdomain|当前的用户域。|
|username|当前的用户名称。|
|webnamespace|当前网站的名称。 此参数在 Web 窗体模板中用于保证类名是唯一的。 如果网站在 Web 服务器的根目录下，则此模板参数解析为 Web 服务器的根目录。|
|year|以 YYYY 格式表示的当前年份。|

> [!NOTE]
> 模板参数区分大小写。

## <a name="custom-template-parameters"></a>自定义模板参数

除了在参数替换过程中使用的默认保留的模板参数之外，还可以指定自己的模板参数和值。 有关详细信息，请参阅 [CustomParameters 元素（Visual Studio 模板）](../extensibility/customparameters-element-visual-studio-templates.md)。

## <a name="example-use-the-project-name-for-a-file-name"></a>示例：对文件名使用项目名称

可以使用属性 `TargetFileName` 中的参数为项目项指定变量文件名。

以下示例指定可执行文件的名称使用由 `$projectname$` 指定的项目名称。

```xml
<TemplateContent>
    <ProjectItem
        ReplaceParameters="true"
        TargetFileName="$projectname$.exe">
            File1.exe
    </ProjectItem>
      ...
</TemplateContent>
```

## <a name="example-use-the-safe-project-name-for-the-namespace-name"></a>示例：对命名空间名称使用安全项目名称

要将安全的项目名称用于 C# 类文件中的命名空间，请使用以下语法：

```csharp
namespace $safeprojectname$
{
    public class Class1
    {
        public Class1()
        { }
    }
}
```

引用文件时，在项目模板的 .vstemplate  文件中添加 `ReplaceParameters="true"` 属性：

```xml
<TemplateContent>
    <ProjectItem ReplaceParameters="true">
        Class1.cs
    </ProjectItem>
    ...
</TemplateContent>
```

## <a name="see-also"></a>请参阅

- [如何：替换模板中的参数](how-to-substitute-parameters-in-a-template.md)
- [自定义模板](../ide/customizing-project-and-item-templates.md)
- [如何：创建项目模板](../ide/how-to-create-project-templates.md)
- [模板架构引用](../extensibility/visual-studio-template-schema-reference.md)
