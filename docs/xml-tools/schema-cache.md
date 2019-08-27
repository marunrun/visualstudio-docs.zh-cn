---
title: XML 编辑器架构缓存
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 35a7fcad-f3bf-4a96-9008-4306e7276223
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 28f5a7ffe202e7e02b06e676501ab508ee1a4ab2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955548"
---
# <a name="schema-cache"></a>架构缓存

XML 编辑器提供的架构缓存位于 *%VSInstallDir%\xml\Schemas*目录。 架构缓存适用于您的计算机上的所有用户，并且包含用于智能感知和 XML 文档验证的标准 XML 架构。

XML 编辑器还可以查找解决方案中的架构，在指定架构**架构**的文档字段**属性**窗口中，并标识的架构`xsi:schemaLocation`和`xsi:noNamespaceSchemaLocation`属性。

下表介绍随 XML 编辑器中的架构。

| Filename | 描述 |
|-| - |
| *catalog.xsd* | “XML 编辑器”架构编录文件的架构。 有关架构编录的信息，请参见下文。 |
| *DotNetConfig.xsd* | Web.Config 文件的架构"<http://schemas.microsoft.com/.NETConfiguration/v2.0>"。 |
| *msbuild.xsd* | 有关 MSBuild 的 make，架构"<http://schemas.microsoft.com/developer/msbuild/2003>"。 |
| *msdata.xsd* | <xref:System.Data.DataSet> 类添加的 XSD 批注的架构“urn:schemas-microsoft-com:xml-msdata”。 |
| *msxsl.xsd* | Microsoft XSLT 脚本块扩展的架构 urn:schemas-microsoft-com:xslt。 |
| *SnippetFormat.xsd* | 代码段 XML 文件的架构。 有关示例，请参阅 *%VSInstallDir%\VC#\Expansions*。 |
| *Soap1.1.xsd* | 简单对象访问协议 (SOAP) 1.1 版中，架构 http://schemas.xmlsoap.org/soap/envelope/。 |
| *Soap1.2.xsd* | 简单对象访问协议 1.2 的架构。 |
| *SiteMapSchema.xsd* | ASP.NET 站点地图 XML 文件架构"<http://schemas.microsoft.com/AspNet/SiteMap-File-1.0>"。 |
| *wsdl.xsd* | Web 服务描述语言，架构 http://schemas.xmlsoap.org/wsdl/。 |
| *xenc.xsd* | 架构为 XML 加密 http://www.w3.org/2000/09/xmldsig#。 |
| *xhtml.xsd* | 为 XHTML 架构 http://www.w3.org/1999/xhtml。 |
| *xlink.xsd* | 架构 XLink1.0， http://www.w3.org/1999/xlink。 |
| *xml.xsd* | 描述 xml: space 和 xml: lang 属性架构 http://www.w3.org/XML/1998/namespace。 |
| *xmlsig.xsd* | XML 数字签名，架构 http://www.w3.org/2000/09/xmldsig#。 |
| *xsdschema.xsd* | 描述 XSD 本身中，架构 http://www.w3.org/2001/XMLSchema。 |
| *xslt.xsd* | 将转换为 XML 架构， http://www.w3.org/1999/XSL/Transform。 |

## <a name="update-schemas-in-the-cache"></a>更新缓存中的架构

编辑器在加载“XML 编辑器”软件包时加载架构缓存目录，并在运行时监视是否发生更改。 如果架构已添加，将自动加载到已知架构的内存中索引。 如果架构已移除，它将自动从内存中索引移除。 如果架构已更新，将自动使此架构的内存中缓存失效。

> [!NOTE]
> 由于架构缓存目录适用于整个计算机，因此，只应在此处添加标准的、适用于在计算机上可能创建的所有 Visual Studio 项目的架构。

“XML 编辑器”还支持在架构缓存目录中包含任意数目的架构编录文件。 架构编录可以指向您始终希望编辑器了解的其他架构位置。 *Catalog.xsd*文件定义编录文件的格式，并且包含在架构缓存目录。 *Catalog.xml*文件的默认目录，并且包含中的其他架构的链接 *%vsinstalldir%*。 下面是个例子*catalog.xml*文件：

```xml
<SchemaCatalog xmlns="http://schemas.microsoft.com/xsd/catalog">
  <Schema href="%VSInstallDir%/help/schemas/Favorites.xsd" targetNamespace="urn:Favorites-Schema"/>
  <Schema href="%VSInstallDir%/help/schemas/Links.xsd" targetNamespace="urn:Links-Schema"/>
  <Schema href="%VSInstallDir%/help/schemas/MyHelp.xsd" targetNamespace="urn:VSHelp-Schema"/>
</SchemaCatalog>
```

`href` 属性可以是指向架构的任何文件路径或 http URL。 文件路径可以相对于编录文档。 由分隔的以下变量 %%、 被编辑器识别和扩展路径中：

- VSInstallDir

- 系统

- ProgramFiles

- Programs

- CommonProgramFiles

- ApplicationData

- CommonApplicationData

- LCID

编录文档可以包含 `Catalog` 元素，该元素指向其他编录。 可以使用 `Catalog` 元素指向你的团队或公司共享的中心编录或与业务伙伴共享的联机编录。 `href` 属性是其他编录的文件路径或 http URL。 以下是 `Catalog` 元素的示例：

```xml
<Catalog href="file://c:/xcbl/xcblCatalog.xml"/>
```

编录还可以控制使用特殊的 `Association` 元素将架构与 XML 文档关联的方式。 此元素将具有特定文件扩展名，这可能很有用，因为 XML 编辑器不进行架构不具有任何自动关联没有目标命名空间的架构相关联`targetNamespace`属性。 在以下示例中，`Association` 元素将 dotNetConfig 架构与所有具有“config”文件扩展名的文件关联。

```xml
<Association extension="config" schema="%VSInstallDir%/xml/schemas/dotNetConfig.xsd"/>
```

## <a name="localized-schemas"></a>本地化的架构

在许多情况下*catalog.xml*文件不包含本地化架构条目。 您可以添加到的其他条目*catalog.xml*指向本地化的架构目录的文件。

在下面的示例中创建了一个新的 `Schema` 元素，该元素使用 %LCID% 变量指向本地化架构。

```xml
<Schema href="%InstallRoot%/Common7/IDE/Policy/Schemas/%LCID%/TDLSchema.xsd"
  targetNamespace="http://www.microsoft.com/schema/EnterpriseTemplates/TDLSchema"/>
```

## <a name="change-the-location-of-the-schema-cache"></a>更改架构缓存位置

你可以自定义架构缓存使用的位置**杂项**选项页。 如果有包含喜欢的架构的目录，可以将编辑器配置为转为使用这些架构。

> [!NOTE]
> 此更改只影响当前的 Visual Studio 用户。

### <a name="to-change-the-schema-cache-location"></a>更改架构缓存的位置

1. 从**工具**菜单中，选择**选项**。

2. 展开**文本编辑器**，展开**XML**，然后单击**杂项**。

3. 单击**浏览**按钮**架构**字段。

4. 选择架构缓存的文件夹，然后单击**确定**。

### <a name="to-add-another-directory-of-common-schemas"></a>添加其他常见架构目录

1. 编辑*catalog.xml* XML 编辑器架构缓存目录中的文件。

2. 添加一个新的 `<Catalog href="..."/>` 元素，指向其他架构的目录。

3. 保存更改。

   将自动重新加载编录。

## <a name="see-also"></a>请参阅

- [XML 编辑器](../xml-tools/xml-editor.md)