---
title: 使用模块包括解决方案中的文件 | Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, deployment modules
- SharePoint development in Visual Studio, modules
- modules [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 778bbc9cff2d7853628edbb5be6466acc55d9ab8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "86015822"
---
# <a name="use-modules-to-include-files-in-the-solution"></a>使用模块包括解决方案中的文件
  有时可能需要将文件部署到 SharePoint 服务器，而不考虑它们的文件类型（如新的母版页）。 为此，可使用模块（不要与 [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] 代码模块混淆）。 模块是 SharePoint 解决方案中文件的容器。 部署解决方案时，模块中的文件将复制到 SharePoint 服务器上的指定文件夹中。

## <a name="module-items-and-elements"></a>模块项和元素
 若要创建模块，请通过在“添加新项”对话框中选择模块来将它添加到项目中。 然后修改其 Elements.xml 文件以包含要部署的文件的名称、文件在系统中的位置，以及应将这些文件复制到的 SharePoint 服务器上的位置。

 下面是模块的 Elements.xml 文件的示例：

```xml
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
    <Module Name="Module1">
        <File Path="Module1\Sample.txt" Url="Module1/Sample.txt" />
    </Module>
</Elements>

```

 新创建的模块包含以下默认文件：

|文件名|说明|
|---------------|-----------------|
|Elements.xml|模块的定义文件。|
|*Sample.txt*|充当模块中文件示例的占位符文件。|

 Elements.xml 文件包含以下元素：

|元素名称|说明|
|------------------|-----------------|
|元素|包含模块中定义的所有元素。|
|模块|Module 元素只有一个特性：Name，它以 `<Module Name="Module1">` 格式指定模块的名称。<br /><br /> 请注意，如果更改模块的名称（或其“Folder Name”属性），则必须手动更新 Module 元素中的名称。<br /><br /> 如果为 Module 元素中的文件指定子目录，[!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] (WSS) 会自动为其创建匹配的目录结构。|
|文件|File 元素具有两个参数（Path 和 Url） 。<br /><br /> - Path：SharePoint 解决方案中文件的名称和位置。 格式为 `Path="Module1\Sample.txt"`。<br /><br /> - Url：将文件部署到 SharePoint 服务器中的位置。 格式为 `Url="Module1/Sample.txt"`。<br /><br /> - Type：一个可选特性，它有以下两个设置：GhostableInLibrary 和 Ghostable 。 格式为 `Type="GhostableInLibrary"`。 指定 GhostableInLibrary 意味着文件将添加到 SharePoint 中的文档库，同时有一个列表项会随文件一起添加到库中。 指定 Ghostable 会使文件添加到文档库外部的 SharePoint。|

 要部署的每个文件都需要在 Elements.xml 中有一个单独的 `<File>` 元素条目。

## <a name="see-also"></a>另请参阅
- [如何：使用模块包括文件](../sharepoint/how-to-include-files-by-using-a-module.md)
- [如何：预配文件](/previous-versions/office/developer/sharepoint-2010/ms441170(v=office.14))
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [为 SharePoint 创建 Web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
