---
title: 如何-指定通过 ClickOnce 发布的文件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- Microsoft.VisualStudio.Publish.BaseProvider.Dialog.File
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, file exclusion
- files, publishing via ClickOnce
ms.assetid: 579c134a-d50f-4e0c-8e05-2a4ff654896a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c7ab6d724b40168f84227edb6ccfafc6245c30e0
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85381777"
---
# <a name="how-to-specify-which-files-are-published-by-clickonce"></a>如何：指定通过 ClickOnce 发布的文件
发布 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序时，会将项目中的所有非代码文件与应用程序一起部署。 在某些情况下，你可能不希望或不需要发布某些文件，或者可能想要根据条件安装某些文件。 Visual Studio 提供排除文件、将文件标记为数据文件或系统必备项的功能，并为条件安装创建文件组。

 应用程序的文件 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 在 "**应用程序文件**" 对话框中管理，可从 "**项目设计器**" 的 "**发布**" 页访问。

 最初，只有一个名为的文件组 **（必需）**。 你可以创建其他文件组并向其分配文件。 你无法更改应用程序运行所需的文件的**下载组**。 例如，应用程序的 .exe 或标记为数据文件的文件必须属于 **（必需）** 组。

 文件的默认 "发布状态" 值标记为 " **（自动）**"。 例如，默认情况下，应用程序的 .exe 的发布状态为 "**包含（自动）** "。

 将 "**生成操作**" 属性设置为 "**内容**" 的文件被指定为应用程序文件，并在默认情况下将标记为 "已包含"。 它们可以包含、排除或标记为数据文件。 下面列出了例外情况：

- 默认情况下，将数据文件（如 SQL 数据库（*.mdf*和 *.mdb*）文件和 XML 文件）标记为数据文件。

- 添加引用时，对程序集（*.dll*文件）的引用被指定为以下内容：如果**Copy Local**为**False**，则默认情况下，该程序集标记为必备组件（**必备项（自动）**），该程序集必须存在于 GAC 中，然后才能安装应用程序。 如果**Copy Local**为**True**，则默认情况下，程序集将标记为应用程序程序集（**包括（自动）**），并将在安装时复制到应用程序文件夹中。 只有在 "应用程序文件" 对话框中，COM 引用的**独立**属性设置为 " **True**" 时，它才会显示在 "**应用程序文件**" 对话框*中。* 默认情况下，将包含它。

### <a name="to-add-files-to-the-application-files-dialog-box"></a>将文件添加到 "应用程序文件" 对话框

1. 在**解决方案资源管理器**中选择数据文件。

2. 在属性窗口中，将 "**生成操作**" 属性更改为 "**内容**" 值。

### <a name="to-exclude-files-from-clickonce-publishing"></a>从 ClickOnce 发布中排除文件

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击 "**应用程序文件**" 按钮以打开 "**应用程序文件**" 对话框。

4. 在 "**应用程序文件**" 对话框中，选择要排除的文件。

5. 在 "**发布状态**" 字段中，从下拉列表中选择 "**排除**"。

### <a name="to-mark-files-as-data-files"></a>将文件标记为数据文件

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击 "**应用程序文件**" 按钮以打开 "**应用程序文件**" 对话框。

4. 在 "**应用程序文件**" 对话框中，选择要标记为数据的文件。

5. 在 "**发布状态**" 字段中，从下拉列表中选择 "**数据文件**"。

### <a name="to-mark-files-as-prerequisites"></a>将文件标记为系统必备组件

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击 "**应用程序文件**" 按钮以打开 "**应用程序文件**" 对话框。

4. 在 "**应用程序文件**" 对话框中，选择要标记为必备组件的应用程序集（*.dll*文件）。 请注意，应用程序必须具有应用程序程序集的引用，才能使其显示在列表中。

5. 在 "**发布状态**" 字段中，从下拉列表中选择 "**系统必备**"。

### <a name="to-add-a-new-file-group"></a>添加新的文件组

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击 "**应用程序文件**" 按钮以打开 "**应用程序文件**" 对话框。

4. 在 "**应用程序文件**" 对话框中，选择要包括在新组中的文件的**组**字段。

    > [!NOTE]
    > 文件必须在 "**应用程序文件**" 对话框中显示文件名之前，将 "**生成操作**" 属性设置为 "**内容**"。

5. 在 "**下载组**" 字段中， **\<New...>** 从下拉列表中选择。

6. 在 "**新建组**" 对话框中，输入组的名称，然后单击 **"确定"**。

### <a name="to-add-a-file-to-a-group"></a>向组中添加文件

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击 "**应用程序文件**" 按钮以打开 "**应用程序文件**" 对话框。

4. 在 "**应用程序文件**" 对话框中，选择要包括在新组中的文件的**组**字段。

5. 在 "**下载组**" 字段中，从下拉列表中选择一个组。

    > [!NOTE]
    > 你无法更改应用程序运行所需的文件的**下载组**。

## <a name="see-also"></a>请参阅
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)