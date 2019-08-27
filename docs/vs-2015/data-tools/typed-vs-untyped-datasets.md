---
title: 类型化与非类型化数据集 |Microsoft Docs
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: c83ba0bb-5425-4d47-8891-6b4dbf937701
caps.latest.revision: 8
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 0d02f72a686d0f271e387e550122451db34c019a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68192781"
---
# <a name="typed-vs-untyped-datasets"></a>类型化与非类型化数据集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

类型化数据集是首先派生自基本的数据集<xref:System.Data.DataSet>类，然后使用中的信息**数据集设计器**，它存储在一个.xsd 文件，生成一个新强类型化数据集类。 生成并编译到这个新的数据集类作为第一类对象和属性的一组架构 （表、 列等） 中的信息。 由于类型化数据集继承自基类<xref:System.Data.DataSet>类，类型化的类假定所有的功能<xref:System.Data.DataSet>类，并可用于的一个实例的方法<xref:System.Data.DataSet>类作为参数。  
  
 非类型化的数据集，与此相反，有没有相应的内置架构。 类型化数据集，如中所示的非类型化数据集包含表、 列等，但那些仅作为集合公开。 (但是，手动创建的表和其他数据元素中的非类型化数据集后，您可以导出数据集的结构作为架构通过使用数据集的<xref:System.Data.DataSet.WriteXmlSchema%2A>方法。)  
  
## <a name="contrasting-data-access-in-typed-and-untyped-datasets"></a>对比中类型化和非类型化数据集的数据访问  
 类型化数据集的类已在其中的属性采用的表和列的实际名称的对象模型。 例如，如果您正在使用类型化数据集，您可以通过使用如下所示的代码引用的列：  
  
 [!code-csharp[VbRaddataDatasets#4](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDatasets/CS/Form1.cs#4)]
 [!code-vb[VbRaddataDatasets#4](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDatasets/VB/Form1.vb#4)]  
  
 与此相反，如果您正在使用的非类型化数据集，则是等效的代码：  
  
 [!code-csharp[VbRaddataDatasets#5](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDatasets/CS/Form1.cs#5)]
 [!code-vb[VbRaddataDatasets#5](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDatasets/VB/Form1.vb#5)]  
  
 类型化的访问才不易于阅读，但还完全支持 IntelliSense 中的[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]**代码编辑器**。 除了要更轻松地使用，类型化数据集的语法提供了类型检查在编译时，极大地减少中将值分配到数据集成员的错误的可能性。 如果更改中的列的名称在<xref:System.Data.DataSet>类，然后编译你的应用程序，您将收到生成错误。 通过双击中的生成错误**任务列表**，您可以直接转到行或行的代码引用旧的列名称。 访问表和列在类型化数据集也是在运行时速度稍快由于访问权限取决于在编译时，不能通过在运行时的集合。  
  
 即使类型化数据集有许多优点，非类型化数据集是在很多情况下很有用。 最显而易见的情形是无架构数据集不可用。 这可能会出现，例如，如果你的应用程序与返回的数据集的组件进行交互，但您不知道提前其结构是什么。 同样，有些的时候当您正在使用不具有静态、 可预测结构的数据。 在这种情况下，它是不切实际的使用类型化数据集，因为您将需要重新生成具有数据结构中每个更改的类型化数据集类。  
  
 一般来说，有很多时候您可能无可用架构动态创建的数据集。 在这种情况下，数据集是只是方便使用的结构，您可以在其中保存信息，只要数据可以表示关系的方式。 同时，可以充分利用数据集的功能，例如，序列化的信息将传递到另一个进程，或写出 XML 文件的能力。
