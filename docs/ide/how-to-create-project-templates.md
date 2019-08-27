---
title: 创建项目模板
ms.date: 01/02/2018
ms.topic: conceptual
f1_keywords:
- VS.ExportTemplateWizard
helpviewer_keywords:
- project templates [Visual Studio], creating
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 7cd5bd20d5840b560d5954d62e5d158eb1f6c6e6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62430505"
---
# <a name="how-to-create-project-templates"></a>如何：创建项目模板

本主题介绍如何使用“导出模板向导”创建模板，将模板打包为 .zip 文件。

## <a name="use-the-export-template-wizard"></a>使用“导出模板向导”

1. 创建项目。

    > [!NOTE]
    > 如果命名的项目将成为模板的源，则只使用有效的标识符字符。 否则，从模板创建的项目中可能发生编译错误。 有关有效标识符字符的详细信息，请参阅[已声明的元素名称 (Visual Basic)](/dotnet/visual-basic/programming-guide/language-features/declared-elements/declared-element-names) 或[标识符 (C++)](/cpp/cpp/identifiers-cpp)。 或者，可使用[模板参数](../ide/template-parameters.md)为类和命名空间使用“安全”名称。

2. 编辑项目，直到可以将它导出为一个模板。 例如，可能需要编辑代码文件以指出应替换参数的位置。 请参阅[如何：替换模板中的参数](../ide/how-to-substitute-parameters-in-a-template.md)。

3. 在“项目”菜单上，选择“导出模板”。

   “导出模板向导”随即打开。

4. 在“选择模板类型”页上，选择“项目模板”。 选择要导出到模板的项目，然后选择“下一步”。

::: moniker range="vs-2017"

5. 在“选择模板选项”页面上，输入模板的名称和可选说明、图标和预览图像。 这些项将出现在“新建项目”对话框中。 选择“完成”。

   项目会导出到一个 .zip 文件中，并放在指定的输出位置，还可以导入到 Visual Studio（如果选择）。

若要在“新建项目”对话框中找到模板，请展开“已安装”，然后展开 .vstemplate 文件中与 `ProjectType` 元素对应的类别。 例如，默认情况下，包含 `<ProjectType>CSharp</ProjectType>` 的 .vstemplate 文件显示在“已安装” > “Visual C#”下。 可将模板组织到项目类型的子目录中，只需在该目录中创建一个文件夹，然后将模板的 .zip 文件放入其中即可。 有关详细信息，请参阅[如何：查找和组织模板](../ide/how-to-locate-and-organize-project-and-item-templates.md)。

::: moniker-end

::: moniker range=">=vs-2019"

5. 在“选择模板选项”页面上，输入模板的名称和可选说明、图标和预览图像。 这些项将显示在创建新项目所在的对话框中。 选择“完成”。

   项目会导出到一个 .zip 文件中，并放在指定的输出位置，还可以导入到 Visual Studio（如果选择）。

要在创建新项目所在的对话框中查找模板，请按名称搜索或浏览列表。 （用户模板目前无法根据语言或项目类型进行筛选。）

::: moniker-end

## <a name="other-ways-to-create-project-templates"></a>创建项目模板的其他方法

可通过将构成项目的文件收集到一个文件夹中来手动创建项目模板，然后使用相应的元数据创建 .vstemplate XML 文件。 有关详细信息，请参阅[如何：手动创建 Web 模板](../ide/how-to-manually-create-web-templates.md)。

如果已安装 Visual Studio SDK，可以使用“VSIX 项目”模板将完成的模板包装到 VSIX 文件中，供部署使用。 有关详细信息，请参阅 [VSIX 项目模板入门](../extensibility/getting-started-with-the-vsix-project-template.md)。

## <a name="see-also"></a>请参阅

- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [如何：创建项模板](../ide/how-to-create-item-templates.md)
- [VSIX 项目模板入门](../extensibility/getting-started-with-the-vsix-project-template.md)