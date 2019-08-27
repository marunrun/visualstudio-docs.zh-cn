---
title: 适用于解决方案资源管理器的文件嵌套规则
ms.date: 05/25/2018
ms.topic: conceptual
helpviewer_keywords:
- file nesting
- Solution Explorer, file nesting
author: angelosp
ms.author: angelpe
manager: jillfra
ms.openlocfilehash: a36ca2535785f72756ad66a69c2ebe4d7d5a373b
ms.sourcegitcommit: 32144a09ed46e7223ef7dcab647a9f73afa2dd55
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2019
ms.locfileid: "67587028"
---
# <a name="file-nesting-in-solution-explorer"></a>解决方案资源管理器中的文件嵌套

解决方案资源管理器  嵌套相关文件，以帮助对其进行组织并使之更易于找到。 例如，如果向项目添加 Windows 窗体，则窗体代码文件嵌套在解决方案资源管理器  的窗体下。 在 ASP.NET Core 项目中，可以进一步嵌套文件。 可以在文件嵌套预设“关闭”  、“默认”  和“Web”  之间进行选择。 此外可以[自定义文件嵌套方式](#customize-file-nesting)或[创建特定于解决方案和特定于项目的设置](#create-project-specific-settings)。

> [!NOTE]
> 功能当前仅支持用于 ASP.NET Core 项目。

## <a name="file-nesting-options"></a>文件嵌套选项

![用于开/关文件嵌套的按钮](media/filenesting_onoff.png)

非自定义文件嵌套的可用选项包括：

* **关闭**：此选项提供没有任何嵌套的扁平文件列表。

* **默认**：此选项提供解决方案资源管理器中的默认文件嵌套行为  。 如果给定项目类型没有任何设置，则不嵌套项目中的文件。 如果存在设置（例如对于 Web 项目），则应用嵌套。

* **Web**：此选项将“Web”文件嵌套行为应用到当前解决方案中的所有项目  。 它有多个规则，我们建议立即查看并请告诉我们你的想法。 下面的屏幕截图突出显示此选项中文件嵌套行为的几个示例：

   ![解决方案资源管理器中的文件嵌套](media/filenesting.png)

## <a name="customize-file-nesting"></a>自定义文件嵌套

如果不喜欢现成可用的选项，则可以创建自定义文件嵌套设置，指示解决方案资源管理器如何嵌套文件  。 可以添加任意数量的自定义文件嵌套设置，并且可以按需在它们中间进行切换。 若要创建新的自定义设置，可以使用空文件作为开始，也可以使用“Web”设置作为起始点  ：

![添加自定义文件嵌套规则](media/filenesting_addcustom.png)

我们建议使用“Web”设置作为起始点，因为它可以更轻松地与已运行的某些功能配合使用  。 如果使用“Web”设置作为起始点，则 .filenesting.json 文件类似以下文件   ：

![使用现有文件嵌套规则作为自定义设置的基础](media/filenesting_editcustom.png)

我们来关注节点 dependentFileProviders 及其子节点  。 每个子节点都是 Visual Studio 可以用来嵌套文件的规则类型。 例如，“文件名相同，但扩展名不同”是其中一种规则类型  。 可用规则包括：

* **extensionToExtension**：使用此规则类型在 file.ts 下嵌套 file.js  

* **fileSuffixToExtension**：使用此规则类型在 file.js 下嵌套 file-vsdoc.js  

* **addedExtension**：使用此规则类型在 file.html 下嵌套 file.html.css  

* **pathSegment**：使用此规则类型在 jquery.js 下嵌套 jquery.min.js  

* **allExtensions**：使用此规则类型在 file.js 下嵌套 file.*  

* **fileToFile**：使用此规则类型在 .bowerrc 下嵌套 bower.json  

### <a name="the-extensiontoextension-provider"></a>extensionToExtension 提供程序

通过此提供程序可以使用特定文件扩展名定义文件嵌套规则。 请看下面的示例：

![extentionToExtension 示例规则](media/filenesting_extensiontoextension.png) ![extentionToExtension 示例效果](media/filenesting_extensiontoextension_effect.png)

* 由于第一个 extensionToExtension 规则，cart.js 嵌套在 cart.ts 下   

* cart.js 不嵌套在 cart.tsx 下，因为规则中 .ts 位于 .tsx 之前，且仅能有一个父级    

* 由于第二个 extensionToExtension 规则，light.css 嵌套在 light.sass 下   

* 由于第三个 extensionToExtension 规则，home.html 嵌套在 home.md 下   

### <a name="the-filesuffixtoextension-provider"></a>fileSuffixToExtension 提供程序

此提供程序的工作方式与 extensionToExtension 提供程序类似，唯一的差异是规则查看的是文件后缀而不仅是扩展名  。 请看下面的示例：

![fileSuffixToExtension 示例规则](media/filenesting_filesuffixtoextension.png) ![fileSuffixToExtension 示例效果](media/filenesting_filesuffixtoextension_effect.png)

* 由于 fileSuffixToExtension 规则，portal-vsdoc.js 嵌套在 portal.js 下   

* 规则其他每个方面的工作方式都与 extensionToExtension 类似 

### <a name="the-addedextension-provider"></a>addedExtension 提供程序

此提供程序将有其他扩展名的文件嵌套在没有其他扩展名的文件下。 其他扩展名仅出现在完整文件名的末尾。

请看下面的示例：

![addedExtension 示例规则](media/filenesting_addedextension.png) ![addedExtension 示例效果](media/filenesting_addedextension_effect.png)

* 由于 addedExtension 规则，file.html.css 嵌套在 file.html 下   

> [!NOTE]
> 不要为 `addedExtension` 规则指定任何文件扩展名；它将自动应用到所有文件扩展名。 即，当任意文件包含的名称和扩展名与其他文件的名称和扩展名相同，并在末尾附加有额外的扩展名时，此文件将嵌套在另一个文件下。 无法将此提供程序的作用仅限制在特定文件扩展名。

### <a name="the-pathsegment-provider"></a>pathSegment 提供程序

此提供程序将有其他扩展名的文件嵌套在没有其他扩展名的文件下。 其他扩展名仅出现在完整文件名的中间。

请看下面的示例：

![pathSegment 示例规则](media/filenesting_pathsegment.png) ![pathSegment 示例效果](media/filenesting_pathsegment_effect.png)

* 由于 pathSegment 规则，jquery.min.js 嵌套在 jquery.js 下   

> [!NOTE]
> - 若未为 `pathSegment` 规则指定任何特定文件扩展名，它将应用到所有文件扩展名。 即，当任意文件包含的名称和扩展名与其他文件的名称和扩展名相同，并在中间部分附加有额外的扩展名时，此文件将嵌套在另一个文件下。
> - 可以通过下面的方式指定特定文件扩展名，来将 `pathSegment` 规则的作用限制在这些扩展名：
>
>    ```json
>    "pathSegment": {
>       "add": {
>         ".*": [
>           ".js",
>           ".css",
>           ".html",
>           ".htm"
>         ]
>       }
>    }
>    ```

### <a name="the-allextensions-provider"></a>allExtensions 提供程序

通过此提供程序可以为扩展名随意但基文件名相同的文件定义文件嵌套规则。 请看下面的示例：

![allExtensions 示例规则](media/filenesting_allextensions.png) ![allExtensions 示例效果](media/filenesting_allextensions_effect.png)

* 由于 allExtensions 规则，template.cs 和 template.doc 嵌套在 template.tt 下     。

### <a name="the-filetofile-provider"></a>fileToFile 提供程序

通过此提供程序可以基于整个文件名定义文件嵌套规则。 请看下面的示例：

![fileToFile 示例规则](media/filenesting_filetofile.png) ![fileToFile 示例效果](media/filenesting_filetofile_effect.png)

* 由于 fileToFile 规则，.bowerrc 嵌套在 bower.json 下   

### <a name="rule-order"></a>规则顺序

顺序在自定义设置文件的每个部分中都很重要。 可以通过在 dependentFileProvider 节点中上下移动规则更改规则执行的顺序  。 例如，如果有一个规则使 file.js 成为 file.ts 父级，而另一个规则使 file.coffee 成为 file.ts 父级，那么它们显示在文件中的顺序决定三个文件都存在时的嵌套行为     。 由于 file.ts 只能有一个父级，所以第一个执行的规则将成为父级  。

排序对规则部分本身也很重要，而不仅仅是对部分中的文件。 只要一对文件与文件嵌套规则匹配，就会忽略文件中往下的其他规则，并且处理下一对文件。

### <a name="file-nesting-button"></a>文件嵌套按钮

可以通过解决方案资源管理器中的同一按钮管理所有设置，包括自己的自定义设置  ：

![激活自定义文件嵌套规则](media/filenesting_activatecustom.png)

## <a name="create-project-specific-settings"></a>创建特定于项目的设置

可以通过每个解决方案和项目的右键单击菜单（关联菜单），创建解决方案专用设置和项目专用设置：

![特定于解决方案和项目的嵌套规则](media/filenesting_solutionprojectspecific.png)

特定于解决方案和特定于项目的设置与活动的 Visual Studio 设置结合。 例如，可能有一个空白的特定于项目的设置文件，但是解决方案资源管理器仍是嵌套文件  。 嵌套行为来自特定于解决方案的设置或 Visual Studio 设置。 合并文件嵌套设置的优先顺序是：“Visual Studio”>“解决方案”>“项目”。

可以通过启用“工具” > “选项” > “ASP.NET Core” > “文件嵌套”下的选项“忽略解决方案和项目设置”，指示 Visual Studio 忽略特定于解决方案和特定于项目的设置，即使是文件位于磁盘上      。

可以通过将“root”节点设为“true”，执行相反操作并指示 Visual Studio 仅使用特定于解决方案或特定于项目的设置    。 Visual Studio 停止合并该级别的文件，并且不将其与层次结构更高的文件合并。

特定于解决方案和特定于项目的设置可以签入到源代码管理，然后使用基本代码的整个团队可以共享它们。

## <a name="disable-file-nesting-rules-for-a-project"></a>禁用项目文件嵌套规则

可以通过对提供程序使用“删除”操作而不是“添加”操作，针对特定解决方案或项目禁用现有全局文件嵌套规则   。 例如，如果将以下设置代码添加到项目，则禁用所有可能对此特定项目全局存在的 pathSegment 规则  ：

```json
"dependentFileProviders": {
  "remove": {
    "pathSegment": {}
  }
}
```

## <a name="see-also"></a>请参阅

- [个性化 IDE](../ide/personalizing-the-visual-studio-ide.md)
- [Visual Studio 中的解决方案和项目](solutions-and-projects-in-visual-studio.md)
