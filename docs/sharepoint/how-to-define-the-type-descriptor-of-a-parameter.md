---
title: 如何：定义参数的类型描述符 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], type descriptor
- BDC [SharePoint development in Visual Studio], parameter types
- BDC [SharePoint development in Visual Studio], type descriptor
- Business Data Connectivity service [SharePoint development in Visual Studio], parameter types
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0b3ae803576c98a86a45d175af45aa28b3852134
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "86016844"
---
# <a name="how-to-define-the-type-descriptor-of-a-parameter"></a>如何：定义参数的类型描述符
  类型描述符包含描述参数的数据类型的属性。 可以定义字段、实体或实体集合的类型描述符。 有关详细信息，请参阅 [TypeDescriptor](/previous-versions/office/developer/sharepoint-2007/ms543392\(v\=office.12\))。

### <a name="to-define-the-type-descriptor-of-a-parameter"></a>定义参数的类型描述符

1. 在 " **BDC 方法详细信息** " 窗口中，选择参数的类型描述符。

2. 在菜单栏上，依次选择 " **视图**"、" **属性窗口**"。

3. 在 " **属性** " 窗口中，设置类型描述符的属性。

     以下过程介绍如何将类型描述符定义为字段、实体或实体集合。

### <a name="to-define-a-field"></a>定义字段

1. 在 " **属性** " 窗口中，将类型描述符的 " **名称** " 属性设置为表示实体的类型中的字段的名称 (例如： **FirstName**) 。

2. 在 " **TypeName** " 属性旁边的列表中，选择适当的数据类型 (例如， **Int32**) 。

     有关其他可选参数的信息，请参阅 [TypeDescriptor](/previous-versions/office/developer/sharepoint-2007/ms543392\(v\=office.12\))。

### <a name="to-define-an-entity"></a>定义实体

1. 在 " **属性** " 窗口中，将 " **名称** " 属性设置为描述实体的名称 (例如： **Contact**) 。

2. 将 " **TypeName** " 属性设置为表示实体的类型的完全限定名称。 此类型可以是你的项目中的类，在你的解决方案中引用的程序集中定义的类型，或 BDC 对象模型中定义的类型。

    - 对于项目中的类，选择 " **TypeName** " 属性旁边的向下箭头，在出现的对话框中选择 " **当前项目** " 选项卡，然后选择项目中的类。

         完全限定名包括后跟 LOB 系统名称的命名空间和类名称。 下面的示例将 " **TypeName** " 属性的值设置为项目中的一个类。

         `MyBDCNamespace.BdcModel1.Contact, BdcModel1`

    - 对于你的解决方案中的程序集的类型，完全限定名包括类型名称、程序集名称、版本号、区域性和公钥标记。

         下面的示例将 **TypeName** 属性的值设置为在你的解决方案中引用的程序集中定义的类型。

         `MyNamespace.Contact, myAssemblyName, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089`

    - 对于 BDC 对象模型中定义的类型，完全限定名包括命名空间和类型名称。

         下面的示例将 **TypeName** 属性的值设置为 BDC 对象模型中的类型。

         `Microsoft.BusinessData.Runtime.DynamicType`

3. 在 " **BDC 方法详细信息** " 窗口中，打开为类型描述符显示的列表，然后选择 " **编辑**"。

     此时将打开 " **BDC 资源管理器** " 窗口。

4. 在 " **BDC 资源管理器**" 中，打开类型描述符的快捷菜单，然后选择 " **添加类型描述符**"。

     新的类型描述符将作为子类型描述符添加到实体类型描述符中。 将此类型描述符配置为字段。

5. 重复步骤 4，为实体的每个字段添加子类型描述符。

### <a name="to-define-a-collection-of-entities"></a>定义实体的集合

1. 在 " **BDC 方法详细信息** " 窗口中，选择所需参数的类型描述符。

2. 在菜单栏上，依次选择 " **视图**"、" **属性窗口**"。

3. 在 " **属性** " 窗口中，将 " **名称** " 属性设置为描述实体的名称 (例如： **Contacts**) 。

4. 将 **IsCollection** 属性设置为 **True**。 这表示此类型描述符是实体的集合。

5. 将 " **TypeName** " 属性设置为一个字符串，该字符串包含对接口的引用 <xref:System.Collections.Generic.IEnumerable%601> 以及表示该实体的类型的完全限定名称。 此类型可以是你的项目中的类，在你的解决方案中引用的程序集中定义的类型，或 BDC 对象模型中定义的类型。

   - 对于项目中的类，选择 " **TypeName** " 属性旁边的向下箭头，在出现的对话框中选择 " **当前项目** " 选项卡，然后选择项目中的类。

      完全限定名包括后跟 LOB 系统名称的命名空间和类名称。

      下面的示例将 **TypeName** 属性的值设置为项目中类的集合。

      `System.Collections.Generic.IEnumerable`1 [MyBDCNamespace，BdcModel1] "

   - 对于你的解决方案中的程序集的类型，完全限定名包括类型名称、程序集名称、版本号、区域性和公钥标记。

      下面的示例将 **TypeName** 属性的值设置为在你的解决方案中引用的程序集中的类型集合。

      `System.Collections.Generic.IEnumerable`1 [MyNamespace，myAssemblyName，Version = 4.0.0.0，Culture = 中立，PublicKeyToken = b77a5c561934e089] '

   - 对于 BDC 对象模型中定义的类型，完全限定名仅包括命名空间和类型名称。

      下面的示例将 **TypeName** 属性的值设置为 BDC 对象模型中定义的类型的集合。

      `System.Collections.Generic.IEnumerable`1 [BusinessData. DynamicType] "

6. 在 " **BDC 方法详细信息** " 窗口中，打开为类型描述符显示的列表，然后选择 " **编辑**"。

    此时将打开 " **BDC 资源管理器** " 窗口。

7. 在 " **BDC 资源管理器**" 中，打开类型描述符的快捷菜单，然后选择 " **添加类型描述符**"。

    新的类型描述符将作为子类型描述符添加到集合类型描述符中。 将此类型描述符配置为实体。

## <a name="see-also"></a>另请参阅
- [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)
- [如何：向模型添加实体](../sharepoint/how-to-add-an-entity-to-a-model.md)
- [如何：向方法添加参数](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [如何：定义方法实例](../sharepoint/how-to-define-a-method-instance.md)
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
