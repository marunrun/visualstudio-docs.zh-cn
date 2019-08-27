---
title: 如何：创建可以为 null 的类型（类设计器）
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- nullable types, Class Designer
- Class Designer [Visual Studio], nullable types
ms.assetid: 84673a89-3f6d-4668-919e-1c0f56182fe5
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 0212f7ef1c5b506ce7a1efbde60e7c46a424bfa3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62975518"
---
# <a name="how-to-create-a-nullable-type-in-class-designer"></a>如何：在类设计器中创建可以为 null 的类型

某些值类型并不是始终具有（或需要）定义的值。 这是数据库中的常见做法，数据库中某些字段可能没有分配任何值。 例如，可以向某个数据库字段分配 null 值，表示尚未向其分配值。

可以为 null 的类型是一种扩展的值类型，以便其可为该类型采用典型范围内的值，也可以采用 null 值。 例如，对于一个可以为 null 的 `Int32`（也以 Null\<Int32> 表示），可以为其分配从 -2147483648 到 2147483647 之间的任何值，或可为其分配 null 值。 可以为 Nullable\<bool> 分配的值包括 `True`、`False` 或 null（不分配任何值）。

可以为 null 的类型是 <xref:System.Nullable%601> 结构的实例。 可以为 null 的类型的每个实例都有两个公共只读属性，`HasValue` 和 `Value`：

- `HasValue` 是一种 `bool` 类型，指示变量是否包含定义的值。 `True` 表示该变量包含非 null 值。 可以通过使用语句（如 `if (x.HasValue)` 或 `if (y != null)`）来测试定义的值。

- `Value` 的类型与基础类型相同。 如果 `HasValue` 为 `True`，则 `Value` 包含有意义的值。 如果 `HasValue` 为 `False`，则访问 `Value` 将引发无效的操作异常。

默认情况下，声明某个变量是可以为 null 的类型后，它将不具备定义的值（即 `HasValue` 为 `False`），而非其基础值类型的默认值。

类设计器显示可以为 null 的类型，就像显示其基础类型一样。

若要深入了解 C# 中可以为 null 的类型，请参阅[可以为 null 的类型](/dotnet/csharp/programming-guide/nullable-types/index)。 若要深入了解 Visual Basic 中可以为 null 的类型，请参阅[可以为 null 的值类型](/dotnet/visual-basic/programming-guide/language-features/data-types/nullable-value-types)。

[!INCLUDE[note_settings_general](../../data-tools/includes/note_settings_general_md.md)]

## <a name="to-add-a-nullable-type-by-using-the-class-designer"></a>使用类设计器添加可以为 null 的类型

1. 在类图中，展开现有类，或创建一个新类。

2. 若要将类添加到项目，请在“类图”菜单上，单击“添加” > “添加类”。

3. 若要展开类形状，请在“类图”菜单上，单击“展开”。

4. 选择类形状。 请在“类图”菜单上，单击“添加” > “字段”。 将在类形状以及“类详细信息”窗口中显示默认名称为“字段”的新字段。

5. 在“类详细信息”窗口的“名称”列中（或类形状中），将新字段的名称更改为有效且有意义的名称。

6. 在“类详细信息”窗口的“类型”列中，通过指定以下内容来将该类型声明为可以为 null 的类型：

    - `int?` (Visual C#)
    - `Nullable(Of Integer)` (Visual Basic)

## <a name="to-add-a-nullable-type-by-using-the-code-editor"></a>使用代码编辑器添加可以为 null 的类型

1. 向项目中添加类。 在“解决方案资源管理器”中，选择项目节点，然后在“项目”菜单中单击“添加类”。

2. 在新类的 .cs 或 .vb 文件中，将新类中的一个或多个可以为 null 的类型添加到类声明。

    ```csharp
    // Declare a nullable type in Visual C#:
    class Test
    {
       int? building_number = 5;
    }
    ```

    ```vb
    ' Declare a nullable type in Visual Basic:
    Class Test
       Dim buildingNumber As Nullable(Of Integer) = 5
    End Class
    ```

3. 从类视图中，将新的类图标拖动到类设计器的设计图面上。 此时类图中将显示类形状。

4. 展开该类形状的详细信息，然后将鼠标指针移到类成员处。 工具提示将显示每个成员的声明。

5. 右键单击类形状，然后单击“类详细信息”。 可以在“类详细信息”窗口中查看或修改新类型的属性。

## <a name="see-also"></a>请参阅

- <xref:System.Nullable%601>
- [可以为 null 的类型](/dotnet/csharp/programming-guide/nullable-types/index)
- [使用可以为 null 的类型](/dotnet/csharp/programming-guide/nullable-types/using-nullable-types)
- [如何：标识可以为 null 的类型](/dotnet/csharp/programming-guide/nullable-types/how-to-identify-a-nullable-type)
- [可以为 null 的值类型](/dotnet/visual-basic/programming-guide/language-features/data-types/nullable-value-types)
