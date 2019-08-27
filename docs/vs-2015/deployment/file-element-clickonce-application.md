---
title: '&lt;文件&gt;元素 （ClickOnce 应用程序） |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
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
caps.latest.revision: 26
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 88fce548d5adbd6d4dc930db767fd3e52690490b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68148779"
---
# <a name="ltfilegt-element-clickonce-application"></a>&lt;文件&gt;元素 （ClickOnce 应用程序）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

标识下载和应用程序使用的所有非程序集文件。  
  
## <a name="syntax"></a>语法  
  
```  
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
  
|特性|描述|  
|---------------|-----------------|  
|`name`|必需。 标识文件的名称。|  
|`size`|必需。 指定大小，以字节为单位的文件。|  
|`group`|可选，如果`optional`特性是未指定或设置为`false`; 如果`optional`是`true`。 此文件所属的组的名称。 名称可以是由开发人员，选择任何 Unicode 字符串值，用于下载文件中使用按需<xref:System.Deployment.Application.ApplicationDeployment>类。|  
|`optional`|可选。 指定此文件必须下载第一个应用程序时运行，或是否该文件之前按需的应用程序请求它应驻留只能在服务器上。 如果`false`或未定义，该文件将下载应用程序首次运行或安装时。 如果`true`、`group`必须为有效的应用程序清单中指定。 `optional` 不能为 true 如果`writeableType`的值指定`applicationData`。|  
|`writeableType`|可选。 指定此文件是一个数据文件。 当前，唯一有效的值是：`applicationData`。|  
  
## <a name="typelib"></a>typelib  
 `typelib`元素是可选元素的子文件。 元素描述为 COM 组件所属的类型库。 元素具有以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`tlbid`|必需。 分配给类型库的 GUID。|  
|`version`|必需。 类型库的版本号。|  
|`helpdir`|必需。 包含有关该组件的帮助文件的目录。 可能是长度为零。|  
|`resourceid`|可选。 区域设置标识符 (LCID) 的十六进制字符串表示形式。 它是一到四个十六进制数字不带 0x 前缀和不带前导零。 LCID 可能有一个非特定语言的子语言标识符。|  
|`flags`|可选。 此类型库的类型库标志的字符串表示形式。 具体而言，它应为"RESTRICTED"、"控制"、"隐藏"和"HASDISKIMAGE"之一。|  
  
## <a name="comclass"></a>comClass  
 `comClass`元素是可选的子`file`，但如果元素是必需[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序包含 COM 组件，它想要部署使用免注册 com。 元素具有以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`clsid`|必需。 以 GUID 形式表示的 COM 组件的类 ID。|  
|`description`|可选。 类名。|  
|`threadingModel`|可选。 使用进程内 COM 类的线程处理模型。 如果此属性为 null，则使用没有线程模型。 客户端的主线程上创建组件和来自其他线程的调用封送到此线程。 以下列表显示了有效的值：<br /><br /> `Apartment`、 `Free`、 `Both`和 `Neutral`。|  
|`tlbid`|可选。 此 COM 组件的类型库的的 GUID。|  
|`progid`|可选。 依赖于版本的编程标识符与 COM 组件关联。 格式`ProgID`是`<vendor>.<component>.<version>`。|  
|`miscStatus`|可选。 在程序集中的重复项清单所提供的信息`MiscStatus`注册表项。 如果值为`miscStatusIcon`， `miscStatusContent`， `miscStatusDocprint`，或`miscStatusThumbnail`找不到属性、 中列出的相应默认值`miscStatus`用于缺少的属性。 值可以是下表中的属性值的以逗号分隔列表。 可以使用此属性，如果 COM 类是需要一个 OCX 类`MiscStatus`注册表项值。|  
|`miscStatusIcon`|可选。 在程序集中的重复项清单 DVASPECT_ICON 提供的信息。 它可以提供一个对象的图标。 值可以是下表中的属性值的以逗号分隔列表。 可以使用此属性，如果 COM 类是需要一个 OCX 类`Miscstatus`注册表项值。|  
|`miscStatusContent`|可选。 在程序集中的重复项清单 DVASPECT_CONTENT 提供的信息。 屏幕或打印机，它可以提供可显示复合文档。 值可以是下表中的属性值的以逗号分隔列表。 可以使用此属性，如果 COM 类是需要一个 OCX 类`MiscStatus`注册表项值。|  
|`miscStatusDocPrint`|可选。 在程序集中的重复项清单 DVASPECT_DOCPRINT 提供的信息。 如同打印到打印机，它可以在屏幕上提供可显示的对象表示形式。 值可以是下表中的属性值的以逗号分隔列表。 可以使用此属性，如果 COM 类是需要一个 OCX 类`MiscStatus`注册表项值。|  
|`miscStatusThumbnail`|可选。 在程序集中的重复项清单 DVASPECT_THUMBNAIL 提供的信息。 它可以提供可浏览工具中显示的对象的缩略图。 值可以是下表中的属性值的以逗号分隔列表。 可以使用此属性，如果 COM 类是需要一个 OCX 类`MiscStatus`注册表项值。|  
  
## <a name="cominterfaceexternalproxystub"></a>comInterfaceExternalProxyStub  
 `comInterfaceExternalProxyStub`元素是可选的子`file`元素，但可能是必需的如果[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序包含 COM 组件，它想要部署使用免注册 com。 该元素包含以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`iid`|必需。 接口 ID (IID) 由该代理服务器提供服务。 IID 必须具有与之相关的大括号。|  
|`baseInterface`|可选。 从其引用的接口的接口的 IID`iid`派生。|  
|`numMethods`|可选。 实现由接口的方法数。|  
|`name`|可选。 该接口作为它的名称将显示在代码中。|  
|`tlbid`|可选。 包含由指定的接口的说明的类型库`iid`属性。|  
|`proxyStubClass32`|可选。 将 IID 映射到在 32 位代理 Dll 的 CLSID。|  
  
## <a name="cominterfaceproxystub"></a>comInterfaceProxyStub  
 `comInterfaceProxyStub`元素是可选的子`file`元素，但可能是必需的如果[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序包含 COM 组件，它想要部署使用免注册 com。 该元素包含以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`iid`|必需。 接口 ID (IID) 由该代理服务器提供服务。 IID 必须具有与之相关的大括号。|  
|`baseInterface`|可选。 从其引用的接口的接口的 IID`iid`派生。|  
|`numMethods`|可选。 实现由接口的方法数。|  
|`Name`|可选。 该接口作为它的名称将显示在代码中。|  
|`Tlbid`|可选。 包含由指定的接口的说明的类型库`iid`属性。|  
|`proxyStubClass32`|可选。 将 IID 映射到在 32 位代理 Dll 的 CLSID。|  
|`threadingModel`|可选。 可选。 使用进程内 COM 类的线程处理模型。 如果此属性为 null，则使用没有线程模型。 客户端的主线程上创建组件和来自其他线程的调用封送到此线程。 以下列表显示了有效的值：<br /><br /> `Apartment`、 `Free`、 `Both`和 `Neutral`。|  
  
## <a name="windowclass"></a>windowClass  
 `windowClass`元素是可选的子`file`元素，但可能是必需的如果[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序包含 COM 组件，它想要部署使用免注册 com。 元素是指由 COM 组件，必须具有应用于它的版本定义的窗口类。 该元素包含以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`versioned`|可选。 控件的内部窗口类注册中使用的名称是否包含含有窗口类的程序集的版本。 此属性的值可以是`yes`或`no`。 默认值为 `yes`。 值`no`仅应在同一个窗口类由某个端组件和等效的非并行组件定义，并且你想要将它们视为相同的窗口类。 请注意，窗口类注册的常用规则用于 — 仅注册窗口类的第一个组件将能够注册它，因为它不具有应用于它的版本。|  
  
## <a name="hash"></a>hash  
 `hash`元素是可选的子`file`元素。 `hash` 元素没有属性。  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 使用应用程序中的所有文件的哈希算法作为安全检查，以确保部署之后没有任何文件发生更改。 如果`hash`元素不包含，不会执行此检查。 因此，省略`hash`不建议元素。  
  
 如果清单中包含不进行哈希处理的文件，该清单不能进行数字签名，因为用户不能验证未经哈希的文件的内容。  
  
## <a name="dsigtransforms"></a>dsig:Transforms  
 `dsig:Transforms`元素是必需的子`hash`元素。 `dsig:Transforms` 元素没有属性。  
  
## <a name="dsigtransform"></a>dsig:Transform  
 `dsig:Transform`元素是必需的子`dsig:Transforms`元素。 `dsig:Transform` 元素具有以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`Algorithm`|用于计算此文件的摘要算法。 当前使用的唯一值[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]是`urn:schemas-microsoft-com:HashTransforms.Identity`。|  
  
## <a name="dsigdigestmethod"></a>dsig:DigestMethod  
 `dsig:DigestMethod`元素是必需的子`hash`元素。 `dsig:DigestMethod` 元素具有以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`Algorithm`|用于计算此文件的摘要算法。 当前使用的唯一值[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]是`http://www.w3.org/2000/09/xmldsig#sha1`。|  
  
## <a name="dsigdigestvalue"></a>dsig:DigestValue  
 `dsig:DigestValue`元素是必需的子`hash`元素。 `dsig:DigestValue` 元素没有属性。 其文本值为指定的文件的计算哈希值。  
  
## <a name="remarks"></a>备注  
 此元素标识组成应用程序的所有非程序集文件，并特别是，文件验证有关的哈希值。 此元素还可以包括与文件关联的组件对象模型 (COM) 隔离数据。 如果一个文件发生更改，应用程序清单文件还必须更新以反映更改。  
  
## <a name="example"></a>示例  
 下面的代码示例演示`file`应用程序中的元素的部署使用的应用程序清单[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]。  
  
```  
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
  
## <a name="see-also"></a>请参阅  
 [ndptecclick](../deployment/clickonce-application-manifest.md)
