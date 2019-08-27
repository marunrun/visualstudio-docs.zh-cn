---
title: 如何：指定通过 ClickOnce 发布的文件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: c04f500ceb8a1c95f643fe43c292bb668d54c2aa
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63406578"
---
# <a name="how-to-specify-which-files-are-published-by-clickonce"></a>如何：指定通过 ClickOnce 发布的文件
发布时[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]随应用程序部署项目中的应用程序，所有非代码文件。 在某些情况下，可能不希望或需要发布某些文件，或者可能想要安装某些基于条件的文件。 Visual Studio 提供的功能，若要排除的文件，将文件标记为数据文件或系统必备组件，并创建用于条件性安装的文件组。

 文件，以[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]在中管理应用程序**应用程序文件**对话框中，可通过访问**发布**页**项目设计器**。

 最初，没有名为的单个文件组 **（必需）** 。 可以创建其他文件组并向其分配文件。 不能更改**下载组**文件所需的应用程序运行。 例如，应用程序的.exe 或文件标记为数据文件必须属于 **（必需）** 组。

 默认发布状态文件值的标记为 **（自动）** 。 例如，应用程序的.exe 的发布状态为**包括 （自动）** 默认情况下。

 文件的工具**生成操作**属性设置为**内容**被指定为应用程序文件并将其标记为默认情况下包含。 它们可以包含、 排除，或标记为数据文件。 例外情况包括，如下所示：

- 例如，SQL 数据库数据文件 ( *.mdf*并 *.mdb*) 文件和 XML 文件将被标记为数据文件默认情况下。

- 程序集的引用 ( *.dll*文件) 时添加引用，如下所示指定：如果**Copy Local**是**False**，默认情况下作为系统必备程序集标记 (**必备组件 （自动）** ) 之前安装了应用程序必须位于 GAC 中。 如果**Copy Local**是**True**，该程序集标记为应用程序程序集默认情况下 (**包括 （自动）** ) 和要复制到位于安装的应用程序文件夹。 COM 引用将显示在**应用程序文件**对话框中 (作为 *.ocx*文件) 仅当其**独立**属性设置为**True**。 默认情况下，它将被包含。

### <a name="to-add-files-to-the-application-files-dialog-box"></a>若要将文件添加到应用程序文件对话框

1. 选择数据文件中的**解决方案资源管理器**。

2. 在属性窗口中更改**生成操作**属性设置为**内容**值。

### <a name="to-exclude-files-from-clickonce-publishing"></a>若要从 ClickOnce 发布中排除文件

1. 在“解决方案资源管理器”  中选择了项目的情况下，在“项目”  菜单上单击“属性”  。

2. 单击“发布”选项卡  。

3. 单击**应用程序文件**按钮以打开**应用程序文件**对话框。

4. 在中**应用程序文件**对话框框中，选择你想要排除的文件。

5. 在中**发布状态**字段中，选择**排除**从下拉列表。

### <a name="to-mark-files-as-data-files"></a>若要将文件标记为数据文件

1. 在“解决方案资源管理器”  中选择了项目的情况下，在“项目”  菜单上单击“属性”  。

2. 单击“发布”选项卡  。

3. 单击**应用程序文件**按钮以打开**应用程序文件**对话框。

4. 在中**应用程序文件**对话框框中，选择你想要将标记为数据文件。

5. 在中**发布状态**字段中，选择**数据文件**从下拉列表。

### <a name="to-mark-files-as-prerequisites"></a>若要将文件标记为系统必备组件

1. 在“解决方案资源管理器”  中选择了项目的情况下，在“项目”  菜单上单击“属性”  。

2. 单击“发布”选项卡  。

3. 单击**应用程序文件**按钮以打开**应用程序文件**对话框。

4. 在中**应用程序文件**对话框框中，选择应用程序程序集 ( *.dll*文件)，你想要将标记为系统必备组件。 请注意，你的应用程序必须具有对应用程序程序集的引用，以使其显示在列表中。

5. 在中**发布状态**字段中，选择**先决条件**从下拉列表。

### <a name="to-add-a-new-file-group"></a>若要添加新的文件组

1. 在“解决方案资源管理器”  中选择了项目的情况下，在“项目”  菜单上单击“属性”  。

2. 单击“发布”选项卡  。

3. 单击**应用程序文件**按钮以打开**应用程序文件**对话框。

4. 在中**应用程序文件**对话框中，选择**组**字段中为你想要包括在新组中的文件。

    > [!NOTE]
    > 文件必须具有**生成操作**属性设置为**内容**文件名称将显示在之前**应用程序文件**对话框。

5. 在中**下载组**字段中，选择 **\<新建...>** 从下拉列表。

6. 在中**新建组**对话框中，输入组的名称，然后单击**确定**。

### <a name="to-add-a-file-to-a-group"></a>若要将文件添加到组

1. 在“解决方案资源管理器”  中选择了项目的情况下，在“项目”  菜单上单击“属性”  。

2. 单击“发布”选项卡  。

3. 单击**应用程序文件**按钮以打开**应用程序文件**对话框。

4. 在中**应用程序文件**对话框中，选择**组**字段中为你想要包括在新组中的文件。

5. 在中**下载组**字段中，从下拉列表中选择一个组。

    > [!NOTE]
    > 不能更改**下载组**文件所需的应用程序运行。

## <a name="see-also"></a>请参阅
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)