---
title: 模板参数 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio templates, parameters
- template parameters [Visual Studio]
- project templates, parameters
- item templates, parameters
ms.assetid: 1b567143-08c6-4d7a-b484-49f0671754fe
caps.latest.revision: 27
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2d7bb7e0f3dfee3dd1bf3e9b42afd5837a29f6ee
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72646809"
---
# <a name="template-parameters"></a>模板参数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在对模板进行实例化时，您可以通过在模板中使用参数来替换模板的关键部分的值，如类名和命名空间。 用户在“新建项目”或“添加新项”对话框中单击“确定”时，后台运行的模板向导会替换这些参数    。

## <a name="declaring-and-enabling-template-parameters"></a>声明和启用模板参数
 模板参数以 $参数$ 的格式进行声明  。 例如:

- $safeprojectname$

- $guid1$

- $guid5$

#### <a name="to-enable-parameter-substitution-in-templates"></a>在模板中启用参数替换

1. 在模板的 .vstemplate 文件中，定位到与要为其启用参数替换的项对应的 `ProjectItem` 元素。

2. 将 `ReplaceParameters` 元素的 `ProjectItem` 属性设置为 `true`。

3. 在项目项的代码文件中，在适当位置上包括参数。 例如，以下参数指定安全项目名称用于文件中的命名空间：

    ```
    namespace $safeprojectname$
    ```

## <a name="reserved-template-parameters"></a>保留的模板参数
 下表列出可供任何模板使用的保留模板参数。

> [!NOTE]
> 模板参数区分大小写。

|参数|说明|
|---------------|-----------------|
|`clrversion`|公共语言运行时 (CLR) 的当前版本。|
|`GUID [1-10]`|一个用于替换项目文件中的项目 GUID 的 GUID。 可指定最多 10 个唯一的 GUID（例如，`guid1)`。|
|`itemname`|“添加新项”对话框中由用户提供的名称  。|
|`machinename`|当前的计算机名称（例如，Computer01）。|
|`projectname`|“新建项目”对话框中由用户提供的名称  。|
|`registeredorganization`|来自 HKLM\Software\Microsoft\Windows NT\CurrentVersion\RegisteredOrganization 的注册表项值。|
|`rootnamespace`|当前项目的根命名空间。 此参数仅适用于项模板。|
|`safeitemname`|用户在“添加新项”对话框中提供的名称，名称中移除了所有的不安全字符和空格  。|
|`safeprojectname`|用户在“新建项目”对话框中提供的名称，名称中移除了所有的不安全字符和空格  。|
|`time`|以 DD/MM/YYYY 00:00:00 格式表示的当前时间。|
|`SpecificSolutionName`|解决方案的名称。 在选中“创建解决方案目录”时，`SpecificSolutionName` 具有解决方案名称。 在未选中“创建解决方案目录”时，`SpecificSolutionName` 为空。|
|`userdomain`|当前的用户域。|
|`username`|当前的用户名称。|
|`webnamespace`|当前网站的名称。 此参数在 Web 窗体模板中用于保证类名是唯一的。 如果网站在 Web 服务器的根目录下，则此模板参数会解析为 Web 服务器的根目录。|
|`year`|以 YYYY 格式表示的当前年份。|

## <a name="custom-template-parameters"></a>自定义模板参数
 除了在参数替换过程中使用的默认保留的模板参数之外，还可以指定自己的模板参数和值。有关详细信息，请参阅 [CustomParameters 元素（Visual Studio 模板）](../extensibility/customparameters-element-visual-studio-templates.md)

## <a name="example-replacing-files-names"></a>示例：替换文件名
 可以使用属性为 `TargetFileName` 的参数为项目项指定变量文件名。 例如，可以指定 .exe 文件使用由 `$projectname$` 指定的项目名称作为文件名。

```
<TemplateContent>
    <ProjectItem
        ReplaceParameters="true"
        TargetFileName="$projectname$.exe">
            File1.exe
    </ProjectItem>
      ...
</TemplateContent>
```

## <a name="example-using-the-project-name-for-the-namespace-name"></a>示例：使用项目名称作为命名空间名称
 要将项目名称用于 Visual C# 类文件 Class1.cs 中的命名空间，请使用以下语法：

```
#region Using directives

using System;
using System.Collections.Generic;
using System.Text;

#endregion

namespace $safeprojectname$
{
    public class Class1
        {
            public Class1()
                {

                }
         }
}
```

 引用文件 Class1.cs 时，请在项目模板的 .vstemplate 文件中包括以下 XML：

```
<TemplateContent>
    <ProjectItem ReplaceParameters="true">
        Class1.cs
    </ProjectItem>
    ...
</TemplateContent>
```

## <a name="see-also"></a>另请参阅
 [自定义模板](../ide/customizing-project-and-item-templates.md)
