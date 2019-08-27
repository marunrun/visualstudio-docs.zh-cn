---
title: Vspackage 中的资源 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, resources in
- resources, managed VSPackages
- VSPackages, managed resources
ms.assetid: cc8c17a6-b190-4856-b001-0c1104f104b2
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3abcfebb7bbcc0eaa6a05760de4531f020b41ddb
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66318730"
---
# <a name="resources-in-vspackages"></a>VSPackage 中的资源
在本机附属 UI Dll 托管的附属 Dll 或托管的 VSPackage 本身中，可以嵌入已本地化的资源。

 不能在 Vspackage 中嵌入一些资源。 可以嵌入以下托管的类型：

- 字符串

- 包加载密钥 （这也是字符串）

- 工具窗口图标

- 已编译的命令表输出 （首席技术官） 文件

- 首席技术官位图

- 命令行帮助

- 有关对话框数据

  托管包中的资源选择的资源 id。 异常是首席技术官文件，它必须命名为 CTMENU。 首席技术官文件必须出现在资源表作为`byte[]`。 由类型标识的所有其他资源项。

  可以使用<xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>属性以指示[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]托管的资源都可用。

  [!code-csharp[VSSDKResources#1](../../extensibility/internals/codesnippet/CSharp/resources-in-vspackages_1.cs)]
  [!code-vb[VSSDKResources#1](../../extensibility/internals/codesnippet/VisualBasic/resources-in-vspackages_1.vb)]

  设置<xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>在这种方式指示[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]例如，通过使用搜索资源时应忽略非托管的附属 Dll <xref:Microsoft.VisualStudio.Shell.Interop.IVsShell.LoadPackageString%2A>。 如果[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]遇到两个或多个资源具有相同的资源 ID，它使用找到的第一个资源。

## <a name="example"></a>示例
 下面的示例是一个工具窗口图标的托管表示形式。

```
<data name="1001"
type="System.Resources.ResXFileRef,System.Windows.Forms">
     <value>
     MyToolWinIcon.bmp;
     System.Drawing.Bitmap,
     System.Drawing,
     Version=1.0.0.0,
     Culture=neutral,
     PublicKeyToken=b03f5f7f11d50a3a
     </value>
</data>
```

 下面的示例演示如何嵌入必须命名为 CTMENU 的首席技术官字节数组。

```
<data name="CTMENU"
type="System.Resources.ResXFileRef,System.Windows.Forms">
     <value>
     MyPackage.cto;
     System.Byte[],
     mscorlib,
     Version=1.0.0.0,
     Culture=neutral,
     PublicKeyToken=b03f5f7f11d50a3a
     </value>
</data>
```

## <a name="implementation-notes"></a>实现说明
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 延迟加载的 Vspackage，只要有可能。 在 VSPackage 中嵌入的首席技术官文件的结果是，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]必须在安装期间，即在它生成合并的命令表加载在内存中的所有此类 Vspackage。 通过检查元数据，而无需在 VSPackage 中运行代码，可以从 VSPackage 中提取资源。 因此是最小的性能损失在此时，VSPackage 未初始化。

 当[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]请求资源从 VSPackage 安装完成后，该包是有可能已加载并初始化，因此是最小的性能损失。

## <a name="see-also"></a>请参阅
- [管理 VSPackages](../../extensibility/managing-vspackages.md)
- [MFC 应用程序中已本地化的资源：附属 DLL](/cpp/build/localized-resources-in-mfc-applications-satellite-dlls)
