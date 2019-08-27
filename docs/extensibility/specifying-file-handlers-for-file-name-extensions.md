---
title: 指定文件扩展名的文件处理程序 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- file extensions, specifying file handlers
ms.assetid: e3de4730-a95c-465a-b3b2-92ca85364ad7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7a80c17fc6de0efe691b1c36e4421cb2b62cbd00
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66331791"
---
# <a name="specifying-file-handlers-for-file-name-extensions"></a>指定文件扩展名的文件处理程序
有多种方法来确定处理特定文件扩展名的文件的应用程序。 OpenWithList 和 OpenWithProgids 谓词是两种方法来指定文件的文件扩展名的注册表项之下的处理程序。

## <a name="openwithlist-verb"></a>OpenWithList 谓词
 右键单击 Windows 资源管理器中的文件时，你将看到**打开**命令。 如果多个产品与扩展相关联，您将看到**打开**子菜单。

 你可以注册不同的应用程序通过在 HKEY_CLASSES_ROOT 中设置的文件扩展名的 OpenWithList 键打开扩展。 下显示下列出的文件扩展名为此密钥的应用程序**推荐的程序**中标题**打开**对话框。 下面的示例演示应用程序注册为打开.vcproj 文件扩展名。

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)="VisualStudio.vcproj.14.0"
      OpenWithList\
         devenv.exe
```

> [!NOTE]
> 指定应用程序的键是从 HKEY_CLASSES_ROOT\Applications 下的列表。

 添加 OpenWithList 键，来声明你的应用程序支持文件扩展名，即使另一个应用程序将获得该扩展的所有权。 这可能是你的应用程序或其他应用程序的未来版本。

## <a name="openwithprogids"></a>OpenWithProgIDs
 编程标识符 (Progid) 是友好版本 Classid 标识应用程序或 COM 对象的版本。 每个共同创建的对象应具有其自己的 ProgID。 例如，VisualStudio.DTE.7.1 启动 Visual Studio.NET 2003 VisualStudio.DTE.10.0 启动时[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。 作为项目类型或项目项类型的所有者，必须为您的文件扩展名来创建特定于版本的 ProgID。 以下 Progid 可能是冗余，多个 ProgID 可能会启动同一应用程序。 有关详细信息，请参阅[注册的文件扩展名的谓词](../extensibility/registering-verbs-for-file-name-extensions.md)。

 使用受版本控制文件的 Progid 为以下命名约定以避免重复使用来自其他供应商注册：

|文件扩展名|版本控制 ProgID|
|--------------------|----------------------|
|.extension|产品名称。 extension.versionMajor.versionMinor|

 您可以注册不同的应用程序能够打开特定文件扩展名，请将版本控制的 Progid 作为值添加到 HKEY_CLASSES_ROOT\\ *\<扩展 >* \OpenWithProgids 密钥。 此注册表项包含文件扩展名关联的备用 Progid 的列表。 在显示与列出的 Progid 关联的应用程序**打开**_产品名称_子菜单。 如果同一应用程序中同时指定`OpenWithList`和`OpenWithProgids`密钥，操作系统将合并重复项。

> [!NOTE]
> `OpenWithProgids`密钥仅支持在 Windows XP 中。 因为其他操作系统忽略此密钥，请不要使用它作为唯一的注册文件处理程序。 使用此密钥来提供在 Windows XP 中更好的用户体验。

 将所需的 Progid 添加为类型 REG_NONE 的值。 下面的代码提供注册文件扩展名的 Progid 的示例 (。*ext*)。

```
HKEY_CLASSES_ROOT\
   .ext\
      (default)="MyProduct.ext.14.0"
      OpenWithProgids
         progid        REG_NONE (zero-length binary value)
         otherprogid   REG_NONE (zero-length binary value)
```

 指定为文件扩展名的默认值是默认文件处理程序的 ProgID。 如果修改与以前版本的一起提供的文件扩展名的 ProgID[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]或将接管其他应用程序，则必须注册`OpenWithProgids`密钥文件扩展名，然后在与列表中指定的新 ProgID支持旧 Progid。 例如：

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)="VisualStudio.vcproj.14.0"
      OpenWithProgids
         vcprojfile              //old progid
         VisualStudio.vcproj.12.0 //old progid
         VisualStudio.vcproj.14.0 //new progid
```

 如果旧 ProgID 具有与其关联的谓词，则这些谓词也会出现下 **打开** *产品名称* 的快捷菜单中。

## <a name="see-also"></a>请参阅
- [关于文件扩展名](../extensibility/about-file-name-extensions.md)
- [注册文件扩展名的谓词](../extensibility/registering-verbs-for-file-name-extensions.md)