---
title: XML 架构设计器与 XML 编辑器的集成
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 43d7a8e6-bd94-4407-a800-15a145c74223
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 23a9220d84e2fb1a15545d1a880b0084952da77f
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592576"
---
# <a name="integration-with-xml-editor"></a>与 XML 编辑器集成

XML 架构设计器与 XML 编辑器集成。 如果在 XML 编辑器中修改 XSD 文件，则更改将反映在[Xml 架构资源管理器](../xml-tools/xml-schema-explorer.md)中。 如果已打开[图形视图](../xml-tools/graph-view.md)或[内容模型视图](../xml-tools/content-model-view.md)，则更改也会反映在该处。 可以通过以下方式在 XML 架构设计器和 XML 编辑器之间导航：

- 在 XML 编辑器中，右键单击某个节点，然后选择 **"在 XML 架构资源管理器中显示**"。

- 在图形视图和**XML 架构资源管理器**中，双击某个节点，或右键单击某个节点，然后选择 "**查看代码**"。 在内容模型视图中，右键单击某个节点，然后选择 "**查看代码**"。

以下屏幕截图显示在**Xml 架构资源管理器**中打开的 xml 架构。 **XML 架构资源管理器**在树视图中显示架构集。 "XML 编辑器" 显示当前在 " **Xml 架构资源管理器**" 中处于活动状态的节点的文本视图。

![XSDDesignerWithXMLEditor](../xml-tools/media/xsddesignerwithxmleditor.gif)

有时，在 "XML 编辑器" 和图形设计器中并排查看代码非常有用。 若要同时查看这两个文件，请右键单击 XML 编辑器中的任意位置，然后选择 "**视图设计器**"。 在 Visual Studio Windows 菜单中，选择 "**新建水平（或垂直）" 选项卡组**。

![XSDDesignerWithXMLEditorAndCMV](../xml-tools/media/xsddesignerwithxmleditorandcmv.gif)

## <a name="see-also"></a>另请参阅

- [XML 架构资源管理器](../xml-tools/xml-schema-explorer.md)
