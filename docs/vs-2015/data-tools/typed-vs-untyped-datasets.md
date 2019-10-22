---
title: 类型化与非类型化的数据集 |Microsoft Docs
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: c83ba0bb-5425-4d47-8891-6b4dbf937701
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 39a16a200bbc057288ae2741e7d504566b0368e1
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667159"
---
# <a name="typed-vs-untyped-datasets"></a>类型化与非类型化数据集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

类型化数据集是第一次派生自基 <xref:System.Data.DataSet> 类，然后使用存储在 .xsd 文件中的**数据集设计器**中的信息来生成新的强类型化数据集类。 将生成架构（表、列等）中的信息，并将其作为一组第一类对象和属性编译到这个新的数据集类中。 由于类型化数据集继承自基本 <xref:System.Data.DataSet> 类，因此类型化类将假定 <xref:System.Data.DataSet> 类的所有功能，并且可与采用 <xref:System.Data.DataSet> 类实例作为参数的方法一起使用。

 与此相反，非类型化数据集没有对应的内置架构。 与类型化数据集中一样，非类型化数据集包含表、列等，但它们只作为集合公开。 （但是，在您手动在非类型化数据集中创建表和其他数据元素后，您可以使用数据集的 <xref:System.Data.DataSet.WriteXmlSchema%2A> 方法将该数据集的结构导出为架构。）

## <a name="contrasting-data-access-in-typed-and-untyped-datasets"></a>在类型化和非类型化数据集中进行对比的数据访问
 类型化数据集的类具有一个对象模型，其中其属性采用表和列的实际名称。 例如，如果使用类型化数据集，则可以通过使用如下所示的代码来引用列：

 [!code-csharp[VbRaddataDatasets#4](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDatasets/CS/Form1.cs#4)]
 [!code-vb[VbRaddataDatasets#4](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDatasets/VB/Form1.vb#4)]

 相反，如果使用非类型化的数据集，则等效的代码为：

 [!code-csharp[VbRaddataDatasets#5](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDatasets/CS/Form1.cs#5)]
 [!code-vb[VbRaddataDatasets#5](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDatasets/VB/Form1.vb#5)]

 类型化访问不仅更易于读取，还可以由 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]**代码编辑器**中的 IntelliSense 完全支持。 除了更易于使用以外，类型化的数据集的语法还在编译时提供类型检查，大大降低了向数据集成员赋值时出现错误的可能性。 如果更改 <xref:System.Data.DataSet> 类中列的名称，然后编译应用程序，则会收到生成错误。 通过双击**任务列表**中的生成错误，可以直接跳到引用旧列名称的代码行或代码行。 在运行时，对类型化数据集中的表和列的访问也稍微快一些，因为访问是在编译时确定的，而不是在运行时集合。

 即使类型化数据集有很多优点，但在各种情况下，非类型化数据集也很有用。 最显而易见的情况是，没有可用于数据集的架构。 例如，如果您的应用程序与返回数据集的组件交互，但您事先并不知道它的结构是什么，就可能会发生这种情况。 同样，在使用不具有静态可预测结构的数据时也是如此。 在这种情况下，使用类型化数据集是不切实际的，因为您必须重新生成数据结构中每个更改的类型化数据集类。

 更常见的情况是，在没有可用架构的情况下，可能会动态创建一个数据集。 在这种情况下，数据集只是一个方便的结构，您可以在其中保留信息，只要数据可以以关系方式表示。 同时，你可以利用数据集的功能，例如序列化信息以传递到另一个进程或写出 XML 文件。
