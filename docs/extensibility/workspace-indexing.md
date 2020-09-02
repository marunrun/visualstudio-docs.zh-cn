---
title: Visual Studio 中的工作区索引 |Microsoft Docs
ms.date: 02/21/2018
ms.topic: conceptual
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 9bf7df777d27003fa5763debc772a8804ec28ef5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62952689"
---
# <a name="workspace-indexing"></a>工作区索引

在解决方案中，项目系统负责提供生成、调试、 **转** 号搜索等功能。 项目系统可以执行此操作，因为它们了解项目内文件的关系和功能。 [打开的文件夹](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)工作区需要相同的见解来提供丰富的 IDE 功能。 此数据的收集和持久存储是称为 "工作区索引" 的过程。 此索引数据可通过一组异步 Api 进行查询。 扩展器可以通过提供 <xref:Microsoft.VisualStudio.Workspace.Indexing.IFileScanner> 知道如何处理某些类型的文件的来参与索引过程。

## <a name="types-of-indexed-data"></a>索引数据的类型

有三种索引的数据。 请注意，文件扫描程序中预期的类型与从索引反序列化的类型不同。

|数据|文件扫描器类型|索引查询结果类型|相关类型|
|--|--|--|--|
|参考|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileReferenceInfo>|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileReferenceResult>|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileReferenceInfoType>|
|符号|<xref:Microsoft.VisualStudio.Workspace.Indexing.SymbolDefinition>|<xref:Microsoft.VisualStudio.Workspace.Indexing.SymbolDefinitionSearchResult>|<xref:Microsoft.VisualStudio.Workspace.Indexing.ISymbolService> 应使用，而不是 `IIndexWorkspaceService` 查询|
|数据值|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileDataValue>|<xref:Microsoft.VisualStudio.Workspace.Indexing.FileDataResult`1>||

## <a name="querying-for-indexed-data"></a>查询索引数据

有两种可用于访问持久化数据的异步类型。 第一种是 <xref:Microsoft.VisualStudio.Workspace.Indexing.IIndexWorkspaceData> 。 它提供对单个文件和数据的基本访问权限 `FileReferenceResult` `FileDataResult` ，并缓存结果。 第二种是 <xref:Microsoft.VisualStudio.Workspace.Indexing.IIndexWorkspaceService> 不使用缓存，但允许使用更多查询功能。

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

1. 工作区中的文件系统实体的发现和持久性 (仅针对初始打开扫描) 。
1. 对于每个文件，要求最高优先级的匹配提供程序扫描 `FileReferenceInfo` 。
1. 对于每个文件，要求最高优先级的匹配提供程序扫描 `SymbolDefinition` 。
1. 对于每个文件，将要求所有提供程序提供 `FileDataValue` 。

扩展可以通过实现 `IWorkspaceProviderFactory<IFileScanner>` 和导出类型来导出扫描仪 <xref:Microsoft.VisualStudio.Workspace.Indexing.ExportFileScannerAttribute> 。 `SupportedTypes`特性参数应为来自的一个或多个值 <xref:Microsoft.VisualStudio.Workspace.Indexing.FileScannerTypeConstants> 。 有关示例扫描器，请参阅 VS SDK [示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples/blob/master/Open_Folder_Extensibility/C%23/SymbolScannerSample/TxtFileSymbolScanner.cs)。

> [!WARNING]
> 不要导出支持该类型的文件扫描仪 `FileScannerTypeConstants.FileScannerContentType` 。 它仅用于 Microsoft 内部用途。

在高级情况下，扩展可能会动态支持任意一组文件类型。 `IWorkspaceProviderFactory<IFileScanner>`扩展可以导出，而不是 MEF 导出 `IWorkspaceProviderFactory<IFileScannerProvider>` 。 索引开始时，此工厂类型会被导入、实例化并 <xref:Microsoft.VisualStudio.Workspace.Indexing.IFileScannerProvider.GetSymbolScannersAsync%2A> 调用其方法。 `IFileScanner` 支持任何值的实例 `FileScannerTpeConstants` ，而不仅仅是符号。

## <a name="next-steps"></a>后续步骤

* [工作区和语言服务](workspace-language-services.md) -了解如何将语言服务集成到打开的文件夹工作区中。
* [工作区生成](workspace-build.md) -打开文件夹支持 MSBuild 和生成文件等生成系统。