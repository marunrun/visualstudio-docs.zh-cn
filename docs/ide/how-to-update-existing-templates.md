---
title: 更新现有项目项模板
ms.date: 01/02/2018
ms.topic: conceptual
helpviewer_keywords:
- item templates, updating
- Visual Studio templates, updating
- project templates, updating
- updating templates [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 44f99646330d3c8a75bd94310bc0adf9073f9d49
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75591354"
---
# <a name="how-to-update-existing-templates"></a>如何：更新现有模板

创建模板并将文件压缩为一个 .zip 文件后，可能想要修改该模板  。 为此，可手动更改模板中的文件，也可从基于该模板的项目中导出新模板。

## <a name="use-the-export-template-wizard"></a>使用“导出模板向导”

Visual Studio 提供了“导出模板向导”，该向导可用于更新现有模板  ：

1. 从菜单栏中选择“文件” > “新建” > ’“项目”    。

1. 选择要更新的模板，然后继续完成新项目的创建步骤。

1. 修改 Visual Studio 中的项目。 例如，更改输出类型或将新文件添加到项目中。

1. 在“项目”菜单上，选择“导出模板”   。

    “导出模板向导”随即打开  。

1. 按照向导中的提示将模板以 .zip 文件导出  。

1. （可选）请将 .zip 文件放在以下目录中以供选择：%USERPROFILE%\Documents\Visual Studio \<version\>\Templates\ProjectTemplates   。 如果未在“导出模板向导”中选择“自动将模板导入 Visual Studio”选项，则需执行此步骤   。

1. 删除旧的模板 .zip 文件  。

## <a name="manually-update-an-existing-template"></a>手动更新现有模板

可通过修改压缩的 .zip 文件中的文件来更新现有模板，而无需使用“导出模板向导”   。

### <a name="to-manually-update-an-existing-template"></a>手动更新现有模板

1. 找到包含模板的 .zip 文件  。 用户项目模板通常位于 %USERPROFILE%\Documents\Visual Studio \<version\>\Templates\ProjectTemplates  。

1. 解压缩 .zip 文件  。

1. 修改或删除当前的模板文件，或向该模板添加新文件。

1. 打开、修改并保存 .vstemplate XML 文件，以处理已更新的行为或新文件  。

    有关 .vstemplate 架构的详细信息，请参阅 [Visual Studio 模板架构引用（扩展性）](../extensibility/visual-studio-template-schema-reference.md)  。 有关可在源文件中进行参数化的内容的详细信息，请参阅[模板参数](../ide/template-parameters.md)。

1. 选择模板中的文件，然后通过右键单击或从上下文菜单中选择“发送至” > “压缩的文件夹（zip 格式）”   。

    所选的文件将压缩到一个 .zip 文件中  。

1. 将新 .zip 文件放在旧 .zip 文件的同一目录中   。

1. 删除解压缩的模板文件和旧的 .zip 模板文件  。

## <a name="see-also"></a>请参阅

- [自定义模板](../ide/customizing-project-and-item-templates.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [模板参数](../ide/template-parameters.md)
