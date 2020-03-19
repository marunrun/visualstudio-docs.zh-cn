---
title: XmlPoke 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- XmlPoke task [MSBuild]
- MSBuild, XmlPoke task
ms.assetid: 6ba1953c-be3b-4df8-8561-e133408f8270
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f44ce4736900fde35716ca3ec9dabb2d55c6df51
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75588377"
---
# <a name="xmlpoke-task"></a>XmlPoke 任务

将 XPath 查询指定的值设置为 XML 文件。

## <a name="parameters"></a>参数

 下表描述了 `XmlPoke` 任务的参数。

|参数|说明|
|---------------|-----------------|
|`Namespaces`|可选 `String` 参数。<br /><br /> 指定 XPath 查询前缀的命名空间。 `Namespaces` 是 XML 代码片段，由 `Namespace` 元素组成，包含 `Prefix` 和 `Uri` 属性。 属性 `Prefix` 指定与 `Uri` 属性中指定的命名空间关联的前缀。 不要使用空的 `Prefix`。|
|`Query`|可选 `String` 参数。<br /><br /> 指定 XPath 查询。|
|`Value`|必选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定要插入到指定路径的值。|
|`XmlInputPath`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定 XML 输入为文件路径。|

## <a name="remarks"></a>备注

 除了具有表中列出的参数外，此任务还将从本身继承自 <xref:Microsoft.Build.Tasks.TaskExtension> 类的 <xref:Microsoft.Build.Utilities.Task> 类继承参数。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="example"></a>示例

下面是一个要修改的 sample.xml：

```xml
<Package xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
         xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest"
         xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10" >
<Identity Name="Sample.Product " Publisher="CN=1234" Version="1.0.0.0" />
<mp:PhoneIdentity PhoneProductId="456" PhonePublisherId="0" />
</Package>
```

在此示例中，如果要修改 `/Package/mp:PhoneIdentity/PhonePublisherId`，请使用

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <Namespace>
        <Namespace Prefix="dn" Uri="http://schemas.microsoft.com/appx/manifest/foundation/windows10" />
        <Namespace Prefix="mp" Uri="http://schemas.microsoft.com/appx/2014/phone/manifest" />
        <Namespace Prefix="uap" Uri="http://schemas.microsoft.com/appx/manifest/uap/windows10" />
    </Namespace>
</PropertyGroup>

<Target Name="Poke">
  <XmlPoke
    XmlInputPath="Sample.xml"
    Value="MyId"
    Query="/dn:Package/mp:PhoneIdentity/@PhoneProductId"
    Namespaces="$(Namespace)"/>
</Target>
</Project>
```

此处，`dn` 用作默认命名空间的假命名空间前缀。

## <a name="see-also"></a>另请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
