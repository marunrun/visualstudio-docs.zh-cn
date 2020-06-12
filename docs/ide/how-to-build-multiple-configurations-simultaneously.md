---
title: 如何：生成多个配置
ms.date: 05/13/2020
ms.technology: vs-ide-compile
ms.topic: conceptual
ms.assetid: ba830937-3317-4674-8cc2-c0cd565603c5
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b6d6a3b4f9110f85ff42e8b9dcf6dd531c3802e2
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84183543"
---
# <a name="how-to-build-multiple-configurations-in-a-single-build-request"></a>如何：在单个生成请求中生成多个配置

通过使用“批量生成”对话框，可以在一个 IDE 操作中生成具有多个甚至所有生成配置的大多数项目类型。 但是，不能同时在多个生成配置中生成以下类型的项目：

1. 使用 JavaScript 为 Windows 生成的 [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] 应用。

2. 所有 Visual Basic 项目。

3. CMake 项目。

如果解决方案包含这两个项目类型的任何项目，则“批生成”不适用于该解决方案。 在这种情况下，该命令不会出现在“生成”菜单上。

   有关生成配置的详细信息，请参阅[了解生成配置](../ide/understanding-build-configurations.md)。

## <a name="to-build-a-project-in-multiple-build-configurations"></a>在多个生成配置中生成项目

1. 在菜单栏上，依次选择“生成” > “批生成” 。 或者按 Ctrl+Q 打开搜索框，然后搜索 `Batch Build`。

2. 在“生成”列中，选择要在其中生成项目的配置的复选框。

    > [!TIP]
    > 若要编辑或创建解决方案的生成配置，请在菜单栏上选择“生成” > “Configuration Manager”，以打开“Configuration Manager”对话框  。 在对解决方案的生成配置进行编辑后，请选择“批生成”对话框中的“重新生成”按钮，以更新解决方案中项目的所有生成配置 。

3. 选择“生成”或“重新生成”按钮以使用指定配置生成项目 。

## <a name="see-also"></a>请参阅

- [如何：创建和编辑配置](../ide/how-to-create-and-edit-configurations.md)
- [了解生成配置](../ide/understanding-build-configurations.md)
- [并行生成多个项目](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)