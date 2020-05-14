---
title: 为文件名扩展名指定文件处理程序 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699755"
---
# <a name="specifying-file-handlers-for-file-name-extensions"></a>指定文件扩展名的文件处理程序
有许多方法可以确定处理具有特定文件扩展名的文件的应用程序。 OpenWithList 和 OpenWithProgids 谓词是两种在文件扩展名的注册表项下指定文件处理程序的方法。

## <a name="openwithlist-verb"></a>打开列表谓词
 当您右键单击 Windows 资源管理器中的文件时，您将看到 **"打开**"命令。 如果多个产品与扩展关联，您将看到 **"打开使用"** 子菜单。

 您可以通过在HKEY_CLASSES_ROOT中为文件扩展名设置 OpenWithList 密钥来注册不同的应用程序以打开扩展名。 此键下列出的文件扩展名下的应用程序将显示在"**打开"** 对话框中的 **"建议程序**"标题下。 下面的示例显示注册以打开 .vcproj 文件扩展名的应用程序。

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)="VisualStudio.vcproj.14.0"
      OpenWithList\
         devenv.exe
```

> [!NOTE]
> 指定应用程序的键来自HKEY_CLASSES_ROOT_应用程序"下的列表中。

 通过添加 OpenWithList 密钥，您可以声明应用程序支持文件扩展名，即使另一个应用程序拥有扩展名。 这可能是应用程序或其他应用程序的未来版本。

## <a name="openwithprogids"></a>打开与 ProgID
 编程标识符 （ProgID） 是标识应用程序或 COM 对象的版本的类标识的友好版本。 每个可创建对象都应有自己的 ProgID。 例如，VisualStudio.DTE.7.1 启动 Visual Studio .NET 2003，而 VisualStudio.DTE.10.0 启动[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。 作为项目类型或项目项类型的所有者，必须为文件扩展名创建特定于版本的 ProgID。 这些 ProgID 可能是冗余的，因为多个 ProgID 可以启动相同的应用程序。 有关详细信息，请参阅[注册文件名扩展名的谓词](../extensibility/registering-verbs-for-file-name-extensions.md)。

 对版本化文件 ProgID 使用以下命名约定，以避免与其他供应商的注册重复：

|文件扩展名|版本化 ProgID|
|--------------------|----------------------|
|.扩展|产品名称。 扩展.version 主要.version 次要|

 通过将版本化 ProgID 作为值添加到 HKEY_CLASSES_ROOT\\*\<扩展名>*_OpenWithProgids 密钥，可以注册能够打开特定文件扩展名的不同应用程序。 此注册表项包含与文件扩展名关联的备用 ProgID 的列表。 与列出的 ProgID 关联的应用程序将显示在 **"使用**_产品名称_打开"子菜单中。 如果在`OpenWithList`和`OpenWithProgids`键中都指定了相同的应用程序，则操作系统将合并重复项。

> [!NOTE]
> 该`OpenWithProgids`密钥仅在 Windows XP 中受支持。 由于其他操作系统忽略此密钥，因此不要将其用作文件处理程序的唯一注册。 使用此键在 Windows XP 中提供更好的用户体验。

 将所需的 ProgID 添加为类型REG_NONE的值。 以下代码提供了注册文件扩展名 （的 ProgID 的示例（。*ext*）。

```
HKEY_CLASSES_ROOT\
   .ext\
      (default)="MyProduct.ext.14.0"
      OpenWithProgids
         progid        REG_NONE (zero-length binary value)
         otherprogid   REG_NONE (zero-length binary value)
```

 指定为文件扩展名的默认值的 ProgID 是默认文件处理程序。 如果修改以前版本附带[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]的文件扩展名的 ProgID，或者可以由其他应用程序接管的文件扩展名，则必须注册文件扩展名的`OpenWithProgids`密钥，并在列表中指定新的 ProgID 以及您支持的旧 ProgID。 例如：

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)="VisualStudio.vcproj.14.0"
      OpenWithProgids
         vcprojfile              //old progid
         VisualStudio.vcproj.12.0 //old progid
         VisualStudio.vcproj.14.0 //new progid
```

 如果旧的 ProgID 具有与其关联的谓词，则这些谓词也会显示在快捷菜单中的 **"使用***产品名称*打开"下。

## <a name="see-also"></a>请参阅
- [关于文件扩展名](../extensibility/about-file-name-extensions.md)
- [注册文件扩展名的谓词](../extensibility/registering-verbs-for-file-name-extensions.md)
