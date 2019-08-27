---
title: 使用模块包括解决方案中的文件 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 569f1027163d5651d184254b4e6f57a02df2a39a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63007836"
---
# <a name="use-modules-to-include-files-in-the-solution"></a>使用模块包括解决方案中的文件
  可能您可能的想要将文件部署到 SharePoint 服务器，而不考虑它们的文件类型，如新的主页面。 若要执行此操作，可以使用*模块*(不要与混淆[!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)]代码模块)。 模块是 SharePoint 解决方案中的文件的容器。 部署解决方案时，该模块中的文件复制到 SharePoint 服务器上的指定文件夹。

## <a name="module-items-and-elements"></a>模块项和元素
 若要创建一个模块，将其添加到项目中选择它在**添加新项**对话框。 然后，修改其*Elements.xml*文件以包括你想要部署，其中它们位于在系统上，且它们应在 SharePoint 服务器上复制的文件的名称。

 下面是举例*Elements.xml*模块文件：

```xml
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
    <Module Name="Module1">
        <File Path="Module1\Sample.txt" Url="Module1/Sample.txt" />
    </Module>
</Elements>

```

 新创建的模块包含以下默认文件：

|文件名|描述|
|---------------|-----------------|
|*Elements.xml*|模块定义文件。|
|*Sample.txt*|一个占位符文件作为模块中的文件的示例。|

 *Elements.xml*文件包含下列元素：

|元素名称|描述|
|------------------|-----------------|
|元素|包含所有模块中定义的元素。|
|模块|模块元素具有单个属性*名称*，，指定的模块的名称格式`<Module Name="Module1">`。<br /><br /> 请注意，如果您更改模块的名称 (或其*文件夹名称*属性)，则必须手动更新模块元素中的名称。<br /><br /> 如果在模块元素中，指定该文件的子目录[!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)](WSS) 将自动为其创建匹配的目录结构。|
|文件|文件元素具有两个参数，*路径*并*Url*。<br /><br /> 路径：名称和位置的 SharePoint 解决方案中的文件。 格式为， `Path="Module1\Sample.txt"`。<br /><br /> -Url:该文件在 SharePoint 服务器的部署位置。 格式为， `Url="Module1/Sample.txt"`。<br /><br /> 类型：一个具有两个设置的可选特性：*GhostableInLibrary*并*Ghostable*。 格式为， `Type="GhostableInLibrary"`。 指定*GhostableInLibrary*意味着该文件将添加到列表项添加到库时随附的文件以及在 SharePoint 中的文档库。 指定*Ghostable*会导致将添加到 SharePoint 文档库外的文件。|

 你想要部署的每个文件需要一个单独`<File>`元素中的条目*Elements.xml*。

## <a name="see-also"></a>请参阅
- [如何：通过使用模块包括文件](../sharepoint/how-to-include-files-by-using-a-module.md)
- [如何：设置文件](http://go.microsoft.com/fwlink/?LinkID=144271)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [为 SharePoint 创建 web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
