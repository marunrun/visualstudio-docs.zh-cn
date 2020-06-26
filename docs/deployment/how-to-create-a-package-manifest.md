---
title: 如何-创建包清单 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- package files [Windows Installer]
- package files [ClickOnce]
- prerequisites, custom bootstrapper package
- dependencies, custom bootstrapper packages
ms.assetid: 5aecc507-2764-42f2-ae6f-c227971cf0af
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dc3a1263136fe4c50b2c7020e1557a7a693691b6
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382518"
---
# <a name="how-to-create-a-package-manifest"></a>如何：创建程序包清单
若要为应用程序部署先决条件，可以使用引导程序包。 引导程序包包含单个产品清单文件，但每个区域设置都包含包清单。 不同本地化版本间的共享功能应进入产品清单。

 有关产品清单的详细信息，请参阅[如何：创建产品清单](../deployment/how-to-create-a-product-manifest.md)。

## <a name="create-the-package-manifest"></a>创建包清单

#### <a name="to-create-the-package-manifest"></a>创建包清单

1. 为引导程序包创建目录。 此示例使用*C:\package*。

2. 使用区域设置的名称创建一个子目录 *，如英语*。

3. 在 Visual Studio 中，创建一个名为*package.xml*的 XML 文件，并将其保存到*C:\package\en*文件夹中。

4. 添加 XML 以列出引导程序包的名称、此本地化包清单的区域性以及可选的许可协议。 下面的 XML 使用 `DisplayName` `Culture` 在后面的元素中定义的变量和。

    ```xml
    <Package
        xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"
        Name="DisplayName"
        Culture="Culture"
        LicenseAgreement="eula.txt">
    ```

5. 添加 XML 以列出区域设置特定目录中的所有文件。 下面的 XML 使用名为*eula.txt*的文件，该文件适用于**en**区域设置。

    ```xml
    <PackageFiles>
      <PackageFile Name="eula.txt"/>
    </PackageFiles>
    ```

6. 添加 XML 以定义引导程序包的可本地化字符串。 下面的 XML 为**en**区域设置添加错误字符串。

    ```xml
      <Strings>
        <String Name="DisplayName">Custom Bootstrapper Package</String>
        <String Name="CultureName">en</String>
        <String Name="NotAnAdmin">You must be an administrator to install
    this package.</String>
        <String Name="GeneralFailure">A general error has occurred while
    installing this package.</String>
    </Strings>
    ```

7. 将*C:\package*文件夹复制到 Visual Studio 引导程序目录。 对于 Visual Studio 2010，这是*\Program Files\Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages*目录。

## <a name="example"></a>示例
 包清单包含特定于区域设置的信息，如错误消息、软件许可条款和语言包。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Package
  xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"
  Name="DisplayName"
  Culture="Culture"
  LicenseAgreement="eula.txt">

  <PackageFiles>
    <PackageFile Name="eula.txt"/>
  </PackageFiles>

  <Strings>
    <String Name="DisplayName">Custom Bootstrapper Package</String>
    <String Name="Culture">en</String>
    <String Name="NotAnAdmin">You must be an administrator to install this package.</String>
    <String Name="GeneralFailure">A general error has occurred while
installing this package.</String>
  </Strings>
</Package>
```

## <a name="see-also"></a>请参阅
- [产品和包架构引用](../deployment/product-and-package-schema-reference.md)