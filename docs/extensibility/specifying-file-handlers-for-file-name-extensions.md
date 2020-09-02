---
title: 指定文件扩展名的文件处理程序 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- file extensions, specifying file handlers
ms.assetid: e3de4730-a95c-465a-b3b2-92ca85364ad7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: af195aea09c91696843c6be42c20053bb8c095a2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80699755"
---
# <a name="specifying-file-handlers-for-file-name-extensions"></a>指定文件扩展名的文件处理程序
可以通过多种方式来确定处理具有特定文件扩展名的文件的应用程序。 OpenWithList 和 OpenWithProgids 谓词是在文件扩展名的注册表项下指定文件处理程序的两种方法。

## <a name="openwithlist-verb"></a>OpenWithList 谓词
 右键单击 Windows 资源管理器中的文件时，将显示 " **打开** " 命令。 如果有多个产品与扩展相关联，则会显示 " **打开方式** " 子菜单。

 可以通过在 HKEY_CLASSES_ROOT 中设置文件扩展名的 OpenWithList 键来注册不同的应用程序以打开扩展。 在 "**打开方式**" 对话框中的 "**推荐的程序**" 标题下显示的文件扩展名下面列出的应用程序。 下面的示例演示注册为打开 vcproj 文件扩展名的应用程序。

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)="VisualStudio.vcproj.14.0"
      OpenWithList\
         devenv.exe
```

> [!NOTE]
> 指定应用程序的键来自 HKEY_CLASSES_ROOT \Applications. 下的列表。

 通过添加 OpenWithList 密钥，你可以声明应用程序支持文件扩展名，即使其他应用程序获得扩展的所有权。 这可能是你的应用程序或其他应用程序的未来版本。

## <a name="openwithprogids"></a>OpenWithProgIDs
 Progid) 的编程标识符 (是标识应用程序或 COM 对象版本的 Classid 的友好版本。 每个可创建的对象都应有自己的 ProgID。 例如，VisualStudio 启动 Visual Studio .NET 2003，而 VisualStudio 启动 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 作为项目类型或项目项类型的所有者，您必须为您的文件扩展名创建特定于版本的 ProgID。 这些 Progid 可能是冗余的，因为多个 ProgID 可能会启动同一个应用程序。 有关详细信息，请参阅为 [文件扩展名注册谓词](../extensibility/registering-verbs-for-file-name-extensions.md)。

 为版本控制文件 Progid 使用以下命名约定，以避免与其他供应商的注册重复：

|文件扩展名|版本控制 ProgID|
|--------------------|----------------------|
|扩展名|ProductName. 扩展名. versionMajor. versionMinor|

 可以通过将版本 Progid 作为值添加到 HKEY_CLASSES_ROOT \OpenWithProgids 键，来注册能够打开特定文件扩展名的不同应用程序 \\ *\<extension>* 。 此注册表项包含与文件扩展名关联的备用 Progid 的列表。 与所列 Progid 关联的应用程序将显示在 " **打开方式**_产品名称_ " 子菜单中。 如果在和键中同时指定了相同的应用程序 `OpenWithList` `OpenWithProgids` ，则操作系统将合并重复项。

> [!NOTE]
> `OpenWithProgids`只有 WINDOWS XP 支持该密钥。 由于其他操作系统会忽略此密钥，因此请勿将其用作文件处理程序的唯一注册。 使用此密钥在 Windows XP 中提供更好的用户体验。

 添加所需的 Progid 作为 REG_NONE 类型的值。 下面的代码提供了一个为 ( 的文件扩展名注册 Progid 的示例。*ext*) 。

```
HKEY_CLASSES_ROOT\
   .ext\
      (default)="MyProduct.ext.14.0"
      OpenWithProgids
         progid        REG_NONE (zero-length binary value)
         otherprogid   REG_NONE (zero-length binary value)
```

 指定为文件扩展名默认值的 ProgID 是默认文件处理程序。 如果修改了以前版本的提供的文件扩展名的 ProgID， [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 或可以被其他应用程序使用，则必须 `OpenWithProgids` 为文件扩展名注册密钥，并在列表中指定新的 progid 以及所支持的旧 progid。 例如：

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)="VisualStudio.vcproj.14.0"
      OpenWithProgids
         vcprojfile              //old progid
         VisualStudio.vcproj.12.0 //old progid
         VisualStudio.vcproj.14.0 //new progid
```

 如果旧 ProgID 具有与之关联的谓词，则这些谓词还将显示在快捷菜单中的 "**以***产品名称*打开" 下。

## <a name="see-also"></a>另请参阅
- [关于文件扩展名](../extensibility/about-file-name-extensions.md)
- [注册文件扩展名的谓词](../extensibility/registering-verbs-for-file-name-extensions.md)
