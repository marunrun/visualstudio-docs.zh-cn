---
title: 如何：从生成中排除项目
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: how-to
ms.assetid: 17a837ca-5db9-46cd-b5a7-b14ad1d2c47d
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c30dd912378fd933d29bff1d8828f31de58f9afa
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85284316"
---
# <a name="how-to-exclude-projects-from-a-build"></a>如何：从生成中排除项目

你可以生成解决方案，但不生成其包含的所有项目。 例如，你可以排除会中断生成的项目。 在调查并解决问题之后，你可以再生成该项目。

可以采用以下方法排除项目：

- 将其从活动解决方案配置中暂时删除。

- 创建不包含该项目的解决方案配置。

有关详细信息，请参阅[了解生成配置](../ide/understanding-build-configurations.md)。

## <a name="to-temporarily-remove-a-project-from-the-active-solution-configuration"></a>从活动解决方案配置中暂时删除项目

1. 在菜单栏上，依次选择“生成” > “Configuration Manager” 。

2. 在“项目上下文”表中，找到要从生成中排除的项目。

3. 在项目的“生成”列中，清除复选框。

4. 选择“关闭”按钮，然后重新生成解决方案。

## <a name="to-create-a-solution-configuration-that-excludes-a-project"></a>创建排除项目的解决方案配置

1. 在菜单栏上，依次选择“生成” > “Configuration Manager” 。

2. 在“活动解决方案配置”列表中，选择 \<New>。

3. 在“名称”框中，输入解决方案配置的名称。

4. 在“从以下对象复制设置”列表中，选择新配置所要基于的解决方案配置（例如，“调试”），然后选择“确定”按钮  。

5. 在“配置管理器”对话框中，清除待排除项目的“生成”列中的复选框，然后选择“关闭”按钮  。

6. 在“标准”工具栏上，确保“解决方案配置”框中的新解决方案配置是活动配置 。

7. 在菜单栏上，依次选择“生成” > “重新生成解决方案”。

## <a name="skipped-projects"></a>跳过的项目

可在生成期间因项目并非最新或已将其从配置中排除而跳过这些项目。 Visual Studio 会使用 MSBuild 生成项目。 如果输出早于输入，则 MSBuild 仅生成目标，其中时间由文件时间戳决定。 要强制重新生成，请使用命令“生成” > “重新生成解决方案” 。

在“输出”窗口的“生成”窗格中，Visual Studio 会报告处于最新状态的项目数量、成功构建的数量、失败的数量和跳过的数量 。 跳过计数不包括因是最新状态而未生成的项目。 如果从活动配置中排除项目，则会在生成期间跳过这些项目。 在生成输出中，会看到一条消息显示已跳过此项目：

```output
2>------ Skipped Build: Project: ConsoleApp2, Configuration: Debug x86 ------
2>Project not selected to build for this solution configuration
```

要查看为何跳过了某项目，请记下活动配置（在上例中为 `Debug x86`），然后选择“生成” > “Configuration Manager” 。 如本文中所述，可查看或更改每个配置会跳过的具体项目。

## <a name="see-also"></a>请参阅

- [了解生成配置](../ide/understanding-build-configurations.md)
- [如何：创建和编辑配置](../ide/how-to-create-and-edit-configurations.md)
- [如何：同时生成多个配置](../ide/how-to-build-multiple-configurations-simultaneously.md)
