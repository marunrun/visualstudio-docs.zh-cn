---
title: 使用 DSL 库在 DSL 之间共享类
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 36c49d3447a5f1fafcf4601057c66ebedcb193ec
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63003381"
---
# <a name="sharing-classes-between-dsls-by-using-a-dsl-library"></a>使用 DSL 库在 DSL 之间共享类
在 Visual Studio 可视化和建模 SDK 中，可以创建可导入到另一个 DSL 的 DSL 定义不完整。 这允许您考虑通用部分类似的模型。

## <a name="creating-and-using-dsl-libraries"></a>创建和使用 DSL 库

#### <a name="to-create-a-dsl-library"></a>若要创建的 DSL 库

1. 创建一个新的 DSL 项目，并选择的 Dsl 解决方案模板。

     使用空模型，将创建单个的 DSL 项目。

2. 您可以添加域类、 关系、 形状等。

     库中的元素不需要形成单个嵌入树。

     若要定义一种关系，可以使用导入程序，创建两个域类，并创建它们之间的关系。

     请考虑设置**继承修饰符**到的域类的`Abstract`。

3. 您可以添加在 DSL 资源管理器，如连接生成器中定义的元素。

4. 您可以添加自定义项，需要额外的代码，例如验证约束。

5. 单击**转换所有模板**。

6. 生成项目。

7. 当你将分发的其他人使用 DSL 时，必须提供编译的程序集 (DLL) 和文件`DslDefinition.dsl`。 可以下的文件夹中找到的已编译的程序集 `Dsl\bin\*`

#### <a name="to-import-a-dsl-library"></a>将 DSL 库导入

1. 在另一个 DSL 定义中，在**DSL 资源管理器**，右键单击 DSL 的根类，然后单击**添加新的 DslLibrary 导入**。

2. 在属性窗口中设置**文件路径**的库。 可以使用相对或绝对路径。

    导入的库在 DSL 资源管理器，显示在只读模式下。

3. 您可以使用导入的类作为基类。 在导入的 DSL 中，创建一个域类，在属性窗口中，设置**基类**到导入的类。

4. 单击转换所有模板。

5. 将对由 DSL 库项目生成的程序集 (DLL) 的引用添加到 DSL 项目中。

6. 生成解决方案。

   DSL 库在可以导入其他库。 当导入一个库时，其导入也会自动显示在 DSL 资源管理器。

## <a name="see-also"></a>请参阅

- [如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
