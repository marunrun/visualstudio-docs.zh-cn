---
title: 如何：选择要使用的 XML 架构
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: d6fda3ef-d465-4788-8514-2f2d528d658c
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2acafe0c782b39bb7aa345b5456df7238703cb20
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592641"
---
# <a name="how-to-select-the-xml-schemas-to-use"></a>如何：选择要使用的 XML 架构

"XML 编辑器" 提供的架构缓存位于 *%VSInstallDir%\xml\Schemas*目录中。 架构缓存中包括用于智能感知和 XML 文档验证的常见 XML 架构。

使用 "**架构**" 文档属性可以选择一个或多个 XML 架构定义语言（XSD）架构。 可以从架构缓存或其他位置选择架构。

指定的架构保存在（隐藏的）解决方案用户选项文件（. *.suo*）以及所有其他 XML 文档属性。 因此，下次打开该解决方案时，不必重新输入这些值。

> [!NOTE]
> 编辑器可以使用内联架构或 `xsd:schemaLocation` 特性引用的架构进行验证。 有关详细信息，请参阅[XML 文档验证](../xml-tools/xml-document-validation.md)。

## <a name="to-select-an-xml-schema-from-the-schema-cache"></a>从架构缓存中选择 XML 架构

1. 在“XML 编辑器”中打开文件。

2. 在文档属性窗口中，单击 "**架构**" 字段。 当浏览按钮（...）出现时，单击它。

   ![XML 文件的架构属性](media/properties-schemas.png)

   " [XML 架构" 对话框](xml-schemas-dialog-box.md)随即打开。 此对话框列出了包含的所有架构。架构缓存中的*xsd*扩展（包括在*catalog .xml*文件中引用的架构）和当前解决方案中的任何架构、在 Visual Studio 中打开、在 `xsd:schemaLocation` 特性中引用，或者在 "**架构**" 属性中引用。

3. 通过执行下列操作之一选择用于验证的架构：

   - 选择 " **XML 架构**" 对话框中列出的架构，单击 "**使用**" 列，然后选择 "**使用此架构**"。

     或

   - 选择 " **XML 架构**" 对话框中列出的多个架构，然后右键单击并选择 "**使用此架构**"。

4. 选择 **“确定”** 。

   所选架构的列表将复制回 "**架构**" 文档属性。

## <a name="to-add-an-xml-schema-to-the-schema-cache"></a>将 XML 架构添加到架构缓存中

1. 在文档属性窗口中，单击 "**架构**" 字段上的按钮。

2. 单击“添加”。

   此时将打开 "**打开 XSD 架构**" 对话框。

3. 浏览并选择要添加到架构缓存的架构。

4. 单击“打开”。

   将架构添加到架构缓存中，并将 "**使用**" 列的值设置为 "**使用此架构**"。

## <a name="to-delete-an-xml-schema-from-the-schema-cache"></a>从架构缓存中删除 XML 架构

1. 在文档属性窗口中，单击 "**架构**" 字段上的按钮。

2. 选择要删除的架构，然后单击 "**删除**"。

   此架构即会从内存中的架构缓存中移除，但不会从文件系统中移除。

   > [!NOTE]
   > 如果仍然通过 `schemaLocation` 属性引用架构，或者匹配 `targetNamespace`，则在这种情况下，**删除**将无法在这种情况下工作，因为它是自动关联的。 在这种情况下，建议将架构标记为 "**使用**" 列中的 "**不使用所选架构**"。

## <a name="see-also"></a>另请参阅

- [架构缓存](../xml-tools/schema-cache.md)
- ["XML 架构" 对话框](../xml-tools/xml-schemas-dialog-box.md)
- [XML 编辑器](../xml-tools/xml-editor.md)
