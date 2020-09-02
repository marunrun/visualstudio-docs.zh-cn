---
title: '&lt;&gt; (ClickOnce 应用程序) 的文件元素 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://www.w3.org/2000/09/xmldsig#Transform
- urn:schemas-microsoft-com:asm.v2#file
- http://www.w3.org/2000/09/xmldsig#DigestValue
- http://www.w3.org/2000/09/xmldsig#DigestMethod
- http://www.w3.org/2000/09/xmldsig#Transforms
- urn:schemas-microsoft-com:asm.v2#hash
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <file> element [ClickOnce application manifest]
- manifests [ClickOnce], file element
ms.assetid: 56e3490c-eed5-4841-b1bf-eefe778b6ac9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9345f3f094e1c48204892cd40cca71a7e28eba7c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62900265"
---
# <a name="ltfilegt-element-clickonce-application"></a>&lt;&gt; (ClickOnce 应用程序) 的文件元素
标识应用程序下载和使用的所有 nonassembly 文件。

## <a name="syntax"></a>语法

```xml
<file
    name
    size
    group
    optional
    writeableType
>
    <typelib
        tlbid
        version
        helpdir
        resourceid
        flags
    />
    <comClass
        clsid
        description
        threadingModel
        tlbid
        progid
        miscStatus
        miscStatusIcon
        miscStatusContent
        miscStatusDocPrint
        miscStatusThumbnail
    />
    <comInterfaceExternalProxyStub
        iid
        baseInterface
        numMethods
        name
        tlbid
        proxyStubClass32
    />
    <comInterfaceProxyStub
        iid
        baseInterface
        numMethods
        name
        tlbid
        proxyStubClass32
    />
    <windowClass
        versioned
    />
</file>
```

## <a name="elements-and-attributes"></a>元素和属性
 `file` 元素是可选的。 元素具有以下属性。

|特性|说明|
|---------------|-----------------|
|`name`|必需。 标识文件的名称。|
|`size`|必需。 指定文件的大小（以字节为单位）。|
|`group`|如果 `optional` 未指定该特性或将其设置为，则为可选 `false` ; 如果为，则为必需 `optional` `true` 。 此文件所属的组的名称。 该名称可以是开发人员选择的任何 Unicode 字符串值，并用于使用类按需下载文件 <xref:System.Deployment.Application.ApplicationDeployment> 。|
|`optional`|可选。 指定此文件是否必须在首次运行应用程序时下载，或者文件是否应仅驻留在服务器上，直到应用程序按需请求该文件。 如果 `false` 或未定义，则在首次运行或安装应用程序时下载该文件。 如果为 `true` ， `group` 则必须为应用程序清单指定有效的。 `optional` 如果指定了值，则不能为 true `writeableType` `applicationData` 。|
|`writeableType`|可选。 指定此文件是数据文件。 当前，唯一有效的值是：`applicationData`。|

## <a name="typelib"></a>typelib
 `typelib`元素是 file 元素的可选子元素。 元素描述属于 COM 组件的类型库。 元素具有以下属性。

|特性|说明|
|---------------|-----------------|
|`tlbid`|必需。 分配给类型库的 GUID。|
|`version`|必需。 类型库的版本号。|
|`helpdir`|必需。 包含组件帮助文件的目录。 的长度可以为零。|
|`resourceid`|可选。  (LCID) 的区域设置标识符的十六进制字符串表示形式。 它是一个到四个十六进制数字，不含0x 前缀且不带前导零。 LCID 可能具有非特定的子语言标识符。|
|`flags`|可选。 此类型库的类型库标志的字符串表示形式。 具体而言，它应是 "受限制的"、"控件"、"隐藏" 和 "HASDISKIMAGE" 中的一个。|

## <a name="comclass"></a>comClass
 `comClass`元素是元素的一个可选子级 `file` ，但如果 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序包含它打算使用无需注册的 com 进行部署的 COM 组件，则此元素是必需的。 元素具有以下属性。

|特性|说明|
|---------------|-----------------|
|`clsid`|必需。 以 GUID 表示的 COM 组件的类 ID。|
|`description`|可选。 类名。|
|`threadingModel`|可选。 进程内 COM 类使用的线程模型。 如果此属性为 null，则不使用线程模型。 在客户端的主线程上创建组件，并将来自其他线程的调用封送到此线程。 以下列表显示了有效值：<br /><br /> `Apartment`、`Free`、`Both` 和 `Neutral`。|
|`tlbid`|可选。 此 COM 组件的类型库的 GUID。|
|`progid`|可选。 与 COM 组件关联的与版本相关的编程标识符。 的格式 `ProgID` 为 `<vendor>.<component>.<version>` 。|
|`miscStatus`|可选。 在程序集清单中，注册表项提供的信息重复 `MiscStatus` 。 如果 `miscStatusIcon` 找不到、 `miscStatusContent` 、 `miscStatusDocprint` 或属性的值 `miscStatusThumbnail` ，则中列出的相应默认值 `miscStatus` 用于缺少的属性。 该值可以是下表中的属性值的逗号分隔列表。 如果 COM 类是需要注册表项值的 OCX 类，则可以使用此属性 `MiscStatus` 。|
|`miscStatusIcon`|可选。 程序集清单中的重复 DVASPECT_ICON 提供的信息。 它可以提供对象的图标。 该值可以是下表中的属性值的逗号分隔列表。 如果 COM 类是需要注册表项值的 OCX 类，则可以使用此属性 `Miscstatus` 。|
|`miscStatusContent`|可选。 程序集清单中的重复 DVASPECT_CONTENT 提供的信息。 它可为屏幕或打印机提供可显示的复合文档。 该值可以是下表中的属性值的逗号分隔列表。 如果 COM 类是需要注册表项值的 OCX 类，则可以使用此属性 `MiscStatus` 。|
|`miscStatusDocPrint`|可选。 程序集清单中的重复 DVASPECT_DOCPRINT 提供的信息。 它可以提供可在屏幕上显示的对象表示形式，就如同打印到打印机一样。 该值可以是下表中的属性值的逗号分隔列表。 如果 COM 类是需要注册表项值的 OCX 类，则可以使用此属性 `MiscStatus` 。|
|`miscStatusThumbnail`|可选。 程序集清单中的重复 DVASPECT_THUMBNAIL 提供的信息。 它可以提供浏览工具中可显示对象的缩略图。 该值可以是下表中的属性值的逗号分隔列表。 如果 COM 类是需要注册表项值的 OCX 类，则可以使用此属性 `MiscStatus` 。|

## <a name="cominterfaceexternalproxystub"></a>comInterfaceExternalProxyStub
 `comInterfaceExternalProxyStub`元素是元素的一个可选子级 `file` ，但如果 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序包含它打算使用免注册 COM 部署的 COM 组件，则可能需要该元素。 元素包含以下属性。

|特性|说明|
|---------------|-----------------|
|`iid`|必需。 接口 ID (IID) 此代理提供此接口。 IID 上必须有大括号。|
|`baseInterface`|可选。 所引用的接口派生自的接口的 IID `iid` 。|
|`numMethods`|可选。 接口实现的方法数。|
|`name`|可选。 将在代码中显示的接口的名称。|
|`tlbid`|可选。 类型库，其中包含由属性指定的接口的说明 `iid` 。|
|`proxyStubClass32`|可选。 将 IID 映射到32位代理 Dll 中的 CLSID。|

## <a name="cominterfaceproxystub"></a>comInterfaceProxyStub
 `comInterfaceProxyStub`元素是元素的一个可选子级 `file` ，但如果 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序包含它打算使用免注册 COM 部署的 COM 组件，则可能需要该元素。 元素包含以下属性。

|特性|说明|
|---------------|-----------------|
|`iid`|必需。 接口 ID (IID) 此代理提供此接口。 IID 上必须有大括号。|
|`baseInterface`|可选。 所引用的接口派生自的接口的 IID `iid` 。|
|`numMethods`|可选。 接口实现的方法数。|
|`Name`|可选。 将在代码中显示的接口的名称。|
|`Tlbid`|可选。 类型库，其中包含由属性指定的接口的说明 `iid` 。|
|`proxyStubClass32`|可选。 将 IID 映射到32位代理 Dll 中的 CLSID。|
|`threadingModel`|可选。 可选。 进程内 COM 类使用的线程模型。 如果此属性为 null，则不使用线程模型。 在客户端的主线程上创建组件，并将来自其他线程的调用封送到此线程。 以下列表显示了有效值：<br /><br /> `Apartment`、`Free`、`Both` 和 `Neutral`。|

## <a name="windowclass"></a>windowClass
 `windowClass`元素是元素的一个可选子级 `file` ，但如果 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序包含它打算使用免注册 COM 部署的 COM 组件，则可能需要该元素。 元素引用由必须应用了版本的 COM 组件定义的窗口类。 元素包含以下属性。

|特性|说明|
|---------------|-----------------|
|`versioned`|可选。 控制在注册中使用的内部窗口类名称是否包含该窗口类的程序集的版本。 此属性的值可以是 `yes` 或 `no` 。 默认值为 `yes`。 `no`仅当并行组件和等效的非并行组件定义了同一窗口类，并且你希望将它们视为同一个窗口类时，才应使用此值。 请注意，适用于窗口类注册的常用规则是：只有注册了 window 类的第一个组件可以注册它，因为它没有应用于它的版本。|

## <a name="hash"></a>hash
 `hash`元素是元素的可选子元素 `file` 。 `hash` 元素没有属性。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 使用应用程序中所有文件的算法哈希作为安全检查，以确保在部署后没有任何文件发生更改。 如果 `hash` 不包含该元素，则不会执行此检查。 因此， `hash` 不建议省略元素。

 如果清单包含未进行哈希处理的文件，则无法对该清单进行数字签名，因为用户无法验证未经过哈希处理的文件的内容。

## <a name="dsigtransforms"></a>dsig:Transforms
 `dsig:Transforms`元素是元素的必需子元素 `hash` 。 `dsig:Transforms` 元素没有属性。

## <a name="dsigtransform"></a>dsig:Transform
 `dsig:Transform`元素是元素的必需子元素 `dsig:Transforms` 。 `dsig:Transform` 元素具有以下属性。

| 特性 | 说明 |
|-------------| - |
| `Algorithm` | 用于计算此文件摘要的算法。 目前使用的唯一值 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 是 `urn:schemas-microsoft-com:HashTransforms.Identity` 。 |

## <a name="dsigdigestmethod"></a>dsig:DigestMethod
 `dsig:DigestMethod`元素是元素的必需子元素 `hash` 。 `dsig:DigestMethod` 元素具有以下属性。

| 特性 | 说明 |
|-------------| - |
| `Algorithm` | 用于计算此文件摘要的算法。 目前使用的唯一值 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 是 `http://www.w3.org/2000/09/xmldsig#sha1` 。 |

## <a name="dsigdigestvalue"></a>dsig:DigestValue
 `dsig:DigestValue`元素是元素的必需子元素 `hash` 。 `dsig:DigestValue` 元素没有属性。 它的文本值为指定文件的计算所得的哈希值。

## <a name="remarks"></a>备注
 此元素标识构成应用程序的所有 nonassembly 文件，尤其是文件验证的哈希值。 此元素还可以包括组件对象模型 (COM) 与该文件关联的隔离数据。 如果文件发生更改，则还必须更新应用程序清单文件以反映所做的更改。

## <a name="example"></a>示例
 下面的代码示例演示 `file` 使用部署的应用程序的应用程序清单中的元素 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。

```xml
<file name="Icon.ico" size="9216">
  <hash>
    <dsig:Transforms>
      <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />
    </dsig:Transforms>
    <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
    <dsig:DigestValue>lVoj+Rh6RQ/HPNLOdayQah5McrI=</dsig:DigestValue>
  </hash>
</file>
```

## <a name="see-also"></a>另请参阅
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)