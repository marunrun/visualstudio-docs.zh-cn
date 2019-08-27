---
title: XML 架构对话框 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 0271fa26-2205-49bd-96e0-ae1441571808
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 82247c2510d64f712cc4b703154ea16a4bb7e7e1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68150655"
---
# <a name="xml-schemas-dialog-box"></a>XML 架构对话框
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**XML 架构**对话框用于选择要与 XML 文档关联的 XML 架构定义语言 (XSD) 架构。 您可以从架构缓存中选择架构，也可以指定不在缓存中的架构。 选定的架构被视为架构集的一部分。 架构集用于 IntelliSense 和 XML 文档验证。  
  
 您可以访问**XML 架构**通过单击对话框中**架构**按钮，在文档属性窗口中，或选择**架构**从**XML**菜单。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **使用**  
 选择如何使用“XML 架构”。  
  
- **自动**。 当前文档未使用此架构，但是此架构可用于自动关联。 如果 XML 文档声明一个与此架构的 `targetNamespace` 匹配的命名空间，则将自动关联此架构并将其包含在架构集中。  
  
- **使用此架构**。 当前文档正在使用此架构。 用户已显式请求通过单击此列来使用此架构，或者根据匹配的 `targetNamespace` 自动关联此架构。  
  
- **不使用所选的架构**。 当前文档不使用此架构，即使此架构具有匹配的 `targetNamespace`。 当架构缓存或解决方案中有同一架构的多个版本时，可以使用此设置来解决冲突。  
  
  **目标 Namespace**  
  显示与 XML 架构关联的目标命名空间。  
  
  **文件的名称**  
  显示 XML 架构文件名。  
  
  **添加**  
  此时将打开**打开 XSD 架构**对话框中，这样就可以选择要添加到架构集中的其他架构。 将架构添加到架构设置**使用**列的值设置为**使用此架构**。  
  
  **移除**  
  从架构集中移除当前所选的架构。 该操作将从内存中的架构缓存中移除架构，但不从文件系统中移除架构。  
  
## <a name="see-also"></a>请参阅  
 [XML 编辑器组件](../xml-tools/xml-editor-components.md)   
 [如何：选择使用的 XML 架构](../xml-tools/how-to-select-the-xml-schemas-to-use.md)   
 [架构缓存](../xml-tools/schema-cache.md)
