---
title: 类型化与非类型化数据集
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
ms.assetid: c83ba0bb-5425-4d47-8891-6b4dbf937701
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 31933e2045981fd6a0f38fb19a9480787c9f282a
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68925588"
---
# <a name="typed-vs-untyped-datasets"></a>类型化与非类型化数据集
类型化数据集是第一个派生自基类<xref:System.Data.DataSet>的数据集, 然后使用存储在 .xsd 文件中的**数据集设计器**中的信息来生成新的强类型化数据集类。 将生成架构 (表、列等) 中的信息, 并将其作为一组第一类对象和属性编译到这个新的数据集类中。 因为类型化数据集继承自基类<xref:System.Data.DataSet> , 所以类型化类将假定<xref:System.Data.DataSet>类的所有功能, 并且可与<xref:System.Data.DataSet>采用类的实例作为参数的方法一起使用。

与此相反, 非类型化数据集没有对应的内置架构。 与类型化数据集中一样, 非类型化数据集包含表、列等, 但它们只作为集合公开。 (但是, 在您手动在非类型化数据集中创建表和其他数据元素后, 您可以使用数据集的<xref:System.Data.DataSet.WriteXmlSchema%2A>方法将该数据集的结构导出为架构。)

## <a name="contrast-data-access-in-typed-and-untyped-datasets"></a>对类型化和非类型化数据集中的数据访问进行对比度
类型化数据集的类具有一个对象模型, 其中其属性采用表和列的实际名称。 例如, 如果使用类型化数据集, 则可以通过使用如下所示的代码来引用列:

[!code-csharp[VbRaddataDatasets#4](../data-tools/codesnippet/CSharp/typed-vs-untyped-datasets_1.cs)]
[!code-vb[VbRaddataDatasets#4](../data-tools/codesnippet/VisualBasic/typed-vs-untyped-datasets_1.vb)]

相反, 如果使用非类型化的数据集, 则等效的代码为:

[!code-csharp[VbRaddataDatasets#5](../data-tools/codesnippet/CSharp/typed-vs-untyped-datasets_2.cs)]
[!code-vb[VbRaddataDatasets#5](../data-tools/codesnippet/VisualBasic/typed-vs-untyped-datasets_2.vb)]

类型化访问不仅更易于阅读, 还可以在 Visual Studio**代码编辑器**中的 IntelliSense 完全支持。 除了更易于使用以外, 类型化的数据集的语法还在编译时提供类型检查, 大大降低了向数据集成员赋值时出现错误的可能性。 如果更改<xref:System.Data.DataSet>类中列的名称, 并编译应用程序, 则会收到生成错误。 通过双击**任务列表**中的生成错误, 可以直接跳到引用旧列名称的代码行或代码行。 在运行时, 对类型化数据集中的表和列的访问也稍微快一些, 因为访问是在编译时确定的, 而不是在运行时集合。

即使类型化数据集有很多优点, 但在各种情况下, 非类型化数据集也很有用。 最显而易见的情况是, 没有可用于数据集的架构。 例如, 如果您的应用程序与返回数据集的组件交互, 但您事先并不知道它的结构是什么, 就可能会发生这种情况。 同样, 在使用不具有静态可预测结构的数据时也是如此。 在这种情况下, 使用类型化数据集是不切实际的, 因为您必须重新生成数据结构中每个更改的类型化数据集类。

更常见的情况是, 在没有可用架构的情况下, 可能会动态创建一个数据集。 在这种情况下, 数据集只是一个方便的结构, 您可以在其中保留信息, 只要数据可以以关系方式表示。 同时, 你可以利用数据集的功能, 例如序列化信息以传递到另一个进程或写出 XML 文件。

## <a name="see-also"></a>请参阅

- [数据集工具](../data-tools/dataset-tools-in-visual-studio.md)