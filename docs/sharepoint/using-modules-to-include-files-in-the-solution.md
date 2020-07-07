---
title: 使用模块在解决方案中包括文件 |Microsoft Docs
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
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015822"
---
# <a name="use-modules-to-include-files-in-the-solution"></a>使用模块在解决方案中包括文件
  有时可能需要将文件部署到 SharePoint 服务器，而不考虑它们的文件类型，例如新的母版页。 为此，可以使用*模块*（不要与 [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] 代码模块混淆）。 模块是 SharePoint 解决方案中的文件的容器。 部署解决方案时，模块中的文件将复制到 SharePoint 服务器上的指定文件夹中。

## <a name="module-items-and-elements"></a>模块项和元素
 若要创建模块，请将其添加到项目中，方法是在 "**添加新项**" 对话框中选择它。 然后，修改其*Elements.xml*文件，使其包含要部署的文件的名称、文件在系统中的位置，以及应在 SharePoint 服务器上将这些文件复制到的位置。

 下面是模块*Elements.xml*文件的示例：

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
|*Elements.xml*|模块的定义文件。|
|*Sample.txt*|作为模块中的文件示例的占位符文件。|

 *Elements.xml*文件包含以下元素：

|元素名称|说明|
|------------------|-----------------|
|元素|包含模块中定义的所有元素。|
|模块|Module 元素具有单个属性*名称*，该属性以格式指定模块的名称 `<Module Name="Module1">` 。<br /><br /> 请注意，如果更改模块的名称（或其*文件夹名称*属性），则必须手动更新 module 元素中的名称。<br /><br /> 如果为 Module 元素中的文件指定子目录， [!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] （WSS）将自动为其创建匹配的目录结构。|
|文件|File 元素具有两个参数：*路径*和*Url*。<br /><br /> -Path： SharePoint 解决方案中文件的名称和位置。 格式为、 `Path="Module1\Sample.txt"` 。<br /><br /> -Url：要将文件部署到 SharePoint 服务器上的位置。 格式为、 `Url="Module1/Sample.txt"` 。<br /><br /> -Type：具有以下两个设置的可选属性： *GhostableInLibrary*和*Ghostable*。 格式为、 `Type="GhostableInLibrary"` 。 指定*GhostableInLibrary*表示将文件添加到 SharePoint 中的文档库，以及在将文件添加到库时伴随文件附带的列表项。 指定*Ghostable*会导致将文件添加到文档库之外的 SharePoint。|

 要部署的每个文件都需要 `<File>` 在*Elements.xml*中有一个单独的元素项。

## <a name="see-also"></a>另请参阅
- [如何：使用模块包括文件](../sharepoint/how-to-include-files-by-using-a-module.md)
- [如何：预配文件](/previous-versions/office/developer/sharepoint-2010/ms441170(v=office.14))
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [为 SharePoint 创建 web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
