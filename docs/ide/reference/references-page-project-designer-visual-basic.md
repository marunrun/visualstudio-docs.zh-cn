---
title: 项目设计器 ->“引用”页 (Visual Basic)
ms.date: 06/21/2017
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesReference
- vb.ProjectPropertiesUnusedReference
- vb.ProjectPropertiesReferencePaths
helpviewer_keywords:
- References page in Project Designer
- Project Designer, References page
ms.assetid: 5a47c595-e084-401c-86e1-74e0bf74fd86
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bbc53a1582a2a4f76de2ea402544137405f5d9f3
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68926136"
---
# <a name="references-page-project-designer-visual-basic"></a>项目设计器 ->“引用”页 (Visual Basic)

使用“项目设计器”  的“引用”  页可以管理项目中的引用、Web 引用和导入的命名空间。 项目可包含对 COM 组件、XML Web service、.NET 库或程序集以及其他类库的引用。 有关使用引用的详细信息，请参阅[管理项目中的引用](../../ide/managing-references-in-a-project.md)。

若要访问“引用”页，请在“解决方案资源管理器”中选择项目节点（而非“解决方案”节点）    。 然后在菜单栏上依次选择“项目”  、“属性”  。 当“项目设计器”出现时，单击“引用”选项卡  。

## <a name="uielement-list"></a>UIElement 列表

借助以下选项，可以在项目中选择或移除引用和导入的命名空间。

引用路径 

单击此按钮，访问“引用路径”对话框  。

> [!NOTE]
> 当项目系统查找一个程序集引用时，系统通过在以下位置查找，按以下顺序解析引用：
>
> 1. 项目文件夹。 “显示所有文件”未生效时，解决方案资源管理器中会出现项目文件夹文件   。
> 2. 在“引用路径”对话框中指定的文件夹  。
> 3. 其文件出现在“添加引用”对话框中的文件夹  。
> 4. 项目的 obj 文件夹。 （向项目添加 COM 引用时，可将一个或多个程序集添加到项目的 obj 文件夹中。）

 **参考资料**

此列表显示项目中的所有引用，包括使用的或未使用的引用。

 **添加**

单击此按钮即可向“引用”  列表添加一个引用或 Web 引用。

选择“引用”即可通过“添加引用”对话框向项目添加引用  。

选择“Web 引用”  即可通过“添加 Web 引用”  对话框向项目添加 Web 引用。

 **移除**

在“引用”列表中选择一个或多个引用，然后单击此按钮即可将其删除  。

 更新 Web 引用 

在“引用”  列表中选择一个 Web 引用，然后单击此按钮即可进行更新。

 导入的命名空间 

可以在此框中键入自己的命名空间，并单击“添加用户导入”，将其添加到命名空间列表  。

可以为用户导入的命名空间创建别名。 为此，可以使用“别名=命名空间”的格式输入别名和命名空间   。 使用长命名空间时此格式十分有用，例如：`Http= MyOrg.ObjectLib.Internet.WebRequestMethods.Http`。

 添加用户导入 

单击此按钮即可将在“导入的命名空间”框中指定的命名空间添加到导入的命名空间列表  。 只有在所指定的命名空间已不在列表中时，此按钮才是活动的。

 命名空间列表 

此列表显示所有可用的命名空间。 已选择项目中所含命名空间对应的复选框。

 更新用户导入 

在命名空间列表中选择用户指定的命名空间，在“导入的命名空间”框中键入要替换的名称，然后单击此按钮，更改为新的命名空间  。 只有当所选的命名空间是通过使用“添加用户导入”按钮添加到列表中时，按钮才是活动的  。 可以添加：

- 类或命名空间，例如 <xref:System.Math?displayProperty=fullName>。

- 别名导入，例如 `VB=Microsoft.VisualBasic`。

- XML 命名空间，例如 `<xmlns:xsl="http://www.w3.org/1999/XSL/Transform">`。

## <a name="see-also"></a>另请参阅

- [管理项目中的引用](../../ide/managing-references-in-a-project.md)
- [如何：添加或删除导入的命名空间 (Visual Basic)](../../ide/how-to-add-or-remove-imported-namespaces-visual-basic.md)
- [Imports 语句（XML 命名空间）](/dotnet/visual-basic/language-reference/statements/imports-statement-xml-namespace)
