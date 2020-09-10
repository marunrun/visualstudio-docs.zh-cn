---
title: LocationFieldMRUPrefix 元素（Visual Studio 模板）
titleSuffix: ''
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#LocationFieldMRUPrefix
helpviewer_keywords:
- <LocationFieldMRUPrefix> element [Visual Studio Templates]
- LocationFieldMRUPrefix element [Visual Studio Templates]
ms.assetid: 03443691-9eb5-46f4-9169-cc2552a04bcb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 28ad23961ba9cd9b8bcdb0467f061353fe0ecdb5
ms.sourcegitcommit: 2a201c93ed526b0f7e5848657500f1111b08ac2a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2020
ms.locfileid: "89741348"
---
# <a name="locationfieldmruprefix-element-visual-studio-templates"></a> (Visual Studio 模板的 LocationFieldMRUPrefix 元素) 

指定 " **新建项目** " 和 " **添加新项** " 对话框中最近使用的 (MRU) 路径。

## <a name="syntax"></a>语法

```xml
<LocationFieldMRUPrefix> ... </LocationFieldMRUPrefix>
```

## <a name="attributes-and-elements"></a>特性和元素

 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

 无。

### <a name="child-elements"></a>子元素

 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|

## <a name="remarks"></a>备注

 此元素只应用于通过生成的模板 [!INCLUDE[vsipprvsip](../extensibility/includes/vsipprvsip_md.md)] 。

## <a name="see-also"></a>请参阅

- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
