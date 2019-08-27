---
title: Visual Studio 中的索引编制的工作区 |Microsoft Docs
ms.date: 02/21/2018
ms.topic: conceptual
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 9bf7df777d27003fa5763debc772a8804ec28ef5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62952689"
---
# <a name="workspace-indexing"></a>工作区索引

在解决方案中，项目系统负责提供功能的生成、 调试**GoTo**符号搜索和的详细信息。 项目系统可以完成这项工作，因为他们了解关系和项目中的文件的功能。 [打开文件夹](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)工作区需要相同的见解，以便提供丰富 IDE 功能。 收集和方便永久存储此数据是名为工作区索引的过程。 此索引的数据可以通过一系列异步 Api 进行查询。 扩展程序可以参与索引的过程通过提供<xref:Microsoft.VisualStudio.Workspace.Indexing.IFileScanner>知道如何处理某些类型的文件的 s。

## <a name="types-of-indexed-data"></a>类型的索引的数据

有三种类型的数据编制索引。 请注意文件扫描程序从预期的类型不同于从索引反序列化的类型。

|数据|文件扫描程序类型|索引查询结果类型|相关的类型|
|--|--|--|--|
|参考资料|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileReferenceInfo>|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileReferenceResult>|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileReferenceInfoType>|
|Symbols|<xref:Microsoft.VisualStudio.Workspace.Indexing.SymbolDefinition>|<xref:Microsoft.VisualStudio.Workspace.Indexing.SymbolDefinitionSearchResult>|<xref:Microsoft.VisualStudio.Workspace.Indexing.ISymbolService> 应使用而不是`IIndexWorkspaceService`的查询|
|数据值|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileDataValue>|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileDataResult`1>||

## <a name="querying-for-indexed-data"></a>查询索引数据

有两种异步类型可用于访问保留的数据。 第一种是通过<xref:Microsoft.VisualStudio.Workspace.Indexing.IIndexWorkspaceData>。 它提供了到单个文件的基本访问权限`FileReferenceResult`和`FileDataResult`数据，并缓存结果。 第二个是<xref:Microsoft.VisualStudio.Workspace.Indexing.IIndexWorkspaceService>这不会使用缓存，但可实现更多的查询功能。

```csharp
using Microsoft.VisualStudio.Workspace;
using Microsoft.VisualStudio.Workspace.Indexing;

private static IIndexWorkspaceData GetCachedIndexedData(IWorkspace workspace)
{
    // Gets access to indexed data wrapped in a cache.
    return workspace?.GetIndexWorkspaceDataService()?.CreateIndexWorkspaceData();
}

private static IIndexWorkspaceService GetDirectIndexedData(IWorkspace workspace)
{
    // Gets direct access to indexed data.
    // Can also be casted to IIndexWorkspaceService2.
    return workspace?.GetIndexWorkspaceService();
}
```

## <a name="participating-in-indexing"></a>参与索引

工作区索引大致遵循以下顺序：

1. 发现和文件系统中的实体 （仅在上初始开始扫描） 工作区的持久性。
1. 每个文件，具有最高优先级的匹配提供程序需要扫描`FileReferenceInfo`s。
1. 每个文件，具有最高优先级的匹配提供程序需要扫描`SymbolDefinition`s。
1. 每个文件，所有提供程序会要求为`FileDataValue`s。

扩展可以通过实现导出扫描仪`IWorkspaceProviderFactory<IFileScanner>`导出的类型和<xref:Microsoft.VisualStudio.Workspace.Indexing.ExportFileScannerAttribute>。 `SupportedTypes`特性参数应为一个或多个值从<xref:Microsoft.VisualStudio.Workspace.Indexing.FileScannerTypeConstants>。 有关示例扫描程序，请参阅 VS SDK[示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples/blob/master/Open_Folder_Extensibility/C%23/SymbolScannerSample/TxtFileSymbolScanner.cs)。

> [!WARNING]
> 不导出的文件扫描程序支持`FileScannerTypeConstants.FileScannerContentType`类型。 Microsoft 仅供内部使用，使用它。

在高级的情况下，扩展可能动态地支持一组任意的文件类型。 而不是 MEF 导出`IWorkspaceProviderFactory<IFileScanner>`，可以导出扩展`IWorkspaceProviderFactory<IFileScannerProvider>`。 此工厂类型的索引开始时，会将其导入，实例化，并可能对其<xref:Microsoft.VisualStudio.Workspace.Indexing.IFileScannerProvider.GetSymbolScannersAsync%2A>调用方法。 `IFileScanner` 支持的任何值的实例`FileScannerTpeConstants`会采用，而不仅仅是符号。

## <a name="next-steps"></a>后续步骤

* [工作区和语言服务](workspace-language-services.md)-了解如何将语言服务集成到一个打开的文件夹的工作区。
* [工作区生成](workspace-build.md)-打开文件夹支持构建如 MSBuild 和生成文件系统。