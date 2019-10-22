---
title: 项目设计器 ->“引用”页 (Visual Basic) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesReference
- vb.ProjectPropertiesUnusedReference
- vb.ProjectPropertiesReferencePaths
helpviewer_keywords:
- References page in Project Designer
- Project Designer, References page
- Unused References dialog box
ms.assetid: 5a47c595-e084-401c-86e1-74e0bf74fd86
caps.latest.revision: 40
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8bb18ec8dd12431d650d844e3698c1986c8d8bd8
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665633"
---
# <a name="references-page-project-designer-visual-basic"></a>项目设计器 ->“引用”页 (Visual Basic)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

使用项目设计器的“引用”页可以管理项目中的引用、Web 引用和导入的命名空间。 项目可包含对 COM 组件、XML Web service、.NET Framework 类库或程序集以及其他类库的引用。 有关使用引用的详细信息，请参阅[管理项目中的引用](../../ide/managing-references-in-a-project.md)。

 若要访问“引用”页，请在“解决方案资源管理器”中选择项目节点（而非“解决方案”节点）。 然后在菜单栏上依次选择“项目”、“属性”。 当“项目设计器”出现时，单击“引用”选项卡。

## <a name="uielement-list"></a>UIElement 列表
 借助以下选项，可以在项目中选择或移除引用和导入的命名空间。

 **未使用的引用**单击此按钮可访问 "**未使用的引用**" 对话框。

 借助“未使用的引用”对话框，可以移除包含在项目中但实际上未被代码使用的引用。 它包含一个网格，其中列出项目中的“引用名称”、“路径”，以及有关未使用命名空间引用的其他信息。 在该网格中，选择要从项目中移除的命名空间引用，然后单击“移除”。

 **引用路径**单击此按钮可访问 "**引用路径**" 对话框。

> [!NOTE]
> 当项目系统查找一个程序集引用时，系统通过在以下位置查找，按以下顺序解析引用：
>
> 1. 项目文件夹。 “显示所有文件”未生效时，解决方案资源管理器中会出现项目文件夹文件。
>    2. 在“引用路径”对话框中指定的文件夹。
>    3. 其文件出现在“添加引用”对话框中的文件夹。
>    4. 项目的 obj 文件夹。 （向项目添加 COM 引用时，可将一个或多个程序集添加到项目的 obj 文件夹中。）

 **引用**此列表显示项目中的所有引用，已使用或未使用。

 **添加**单击此按钮可将引用或 Web 引用添加到 "**引用**" 列表。

 选择“引用”即可通过“添加引用”对话框向项目添加引用。

 选择“Web 引用”即可通过“添加 Web 引用”对话框向项目添加 Web 引用。

 **删除**在 "**引用**" 列表中选择一个或多个引用，然后单击此按钮将其删除。

 **更新 Web 引用**选择 "**引用**" 列表中的 Web 引用，然后单击此按钮进行更新。

 **导入的命名空间**您可以在此框中键入自己的命名空间，然后单击 "**添加用户导入**"，将其添加到命名空间列表中。

 可以为用户导入的命名空间创建别名。 为此，可以使用“别名=命名空间”的格式输入别名和命名空间。 使用长命名空间时此格式十分有用，例如：`Http= MyOrg.ObjectLib.Internet.WebRequestMethods.Http`。

 **添加用户导入**单击此按钮可将 "**导入的命名空间**" 框中指定的命名空间添加到导入的命名空间列表。 只有在所指定的命名空间已不在列表中时，此按钮才是活动的。

 **命名空间列表**此列表显示所有可用的命名空间。 已选择项目中所含命名空间对应的复选框。

 **更新用户导入**在 "命名空间" 列表中选择用户指定的命名空间，在 "**导入的命名空间**" 框中键入要替换为的名称，然后单击此按钮将更改为新命名空间。 只有当所选的命名空间是通过使用“添加用户导入”按钮添加到列表中时，按钮才是活动的。 可以添加：

- 类或命名空间，例如 <xref:System.Math?displayProperty=fullName>。

- 别名导入，例如 `VB=Microsoft.VisualBasic`。

- XML 命名空间，例如 `<xmlns:xsl="http://www.w3.org/1999/XSL/Transform">`。

## <a name="see-also"></a>请参阅
 [钢笔尖如何：使用 "添加引用" 对话框添加或删除引用](https://msdn.microsoft.com/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)[如何：添加或移除导入的命名空间（Visual Basic）](../../ide/how-to-add-or-remove-imported-namespaces-visual-basic.md) [笔尖：添加 Web 引用对话框](https://msdn.microsoft.com/bdf05776-c591-40af-bfd7-e1e2aa1e87b5) [Imports 语句（XML 命名空间）](https://msdn.microsoft.com/library/1f4d50a6-08c7-4c2e-8206-ccae35fcd1b4)
