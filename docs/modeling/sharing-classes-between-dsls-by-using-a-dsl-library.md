---
title: 使用 DSL 库在 DSL 之间共享类
ms.date: 11/04/2016
ms.topic: conceptual
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a09622a2cc7ae6d2a2451ac1de6b628020cff19f
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72747410"
---
# <a name="sharing-classes-between-dsls-by-using-a-dsl-library"></a>使用 DSL 库在 DSL 之间共享类
在 Visual Studio 可视化和建模 SDK 中，可以创建可导入到另一个 DSL 的不完整 DSL 定义。 这使您可以对类似模型的常见部分进行因式分解。

## <a name="creating-and-using-dsl-libraries"></a>创建和使用 DSL 库

#### <a name="to-create-a-dsl-library"></a>创建 DSL 库

1. 创建新的 DSL 项目，并选择 "DSL 库" 解决方案模板。

     将使用空模型创建单个 DSL 项目。

2. 您可以添加域类、关系、形状等。

     库中的元素不必构成单个嵌入树。

     若要定义导入程序可以使用的关系，请创建两个域类并创建它们之间的关系。

     请考虑将域类的**继承修饰符**设置为 `Abstract`。

3. 可以添加在 DSL 资源管理器中定义的元素，例如连接构建器。

4. 您可以添加需要其他代码的自定义项，如验证约束。

5. 单击 "**转换所有模板**"。

6. 生成项目。

7. 将 DSL 分发给其他人使用时，必须同时提供编译的程序集（DLL）和文件 `DslDefinition.dsl`。 可以在下的文件夹中查找已编译的程序集 `Dsl\bin\*`

#### <a name="to-import-a-dsl-library"></a>导入 DSL 库

1. 在其他 DSL 定义中，在**Dsl 资源管理器**中右键单击 dsl 的根类，然后单击 "**添加新的 DslLibrary 导入**"。

2. 在属性窗口中，设置库的**文件路径**。 您可以使用相对路径或绝对路径。

    导入的库在 DSL 资源管理器中显示为只读模式。

3. 您可以使用导入的类作为基类。 在导入 DSL 中创建域类，并在属性窗口中，将 "**基类**" 设置为导入的类。

4. 单击 "转换所有模板"。

5. 添加到 DSL 项目引用 DSL 库项目生成的程序集（DLL）。

6. 生成解决方案。

   DSL 库可以导入其他库。 导入库时，其导入还会自动显示在 DSL 资源管理器中。

## <a name="see-also"></a>请参阅

- [如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
