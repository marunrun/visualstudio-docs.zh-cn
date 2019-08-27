---
title: 如何：创建程序包清单 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
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
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c711c50ab484cc88b1d6aff5c8e3018cead69953
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68153836"
---
# <a name="how-to-create-a-package-manifest"></a>如何：创建包清单
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

若要部署应用程序的先决条件，你可以使用引导程序包。 引导程序包包含一个单一产品清单文件，但是包清单的每个区域设置。 在不同的本地化版本之间共享的功能应进入产品清单。  
  
 有关包清单的详细信息，请参阅[如何：创建产品清单](../deployment/how-to-create-a-product-manifest.md)。  
  
## <a name="creating-the-package-manifest"></a>创建程序包清单  
  
#### <a name="to-create-the-package-manifest"></a>若要创建程序包清单  
  
1. 创建引导程序包的目录。 此示例使用 C:\package。  
  
2. 与区域设置，例如 en 表示英语名称创建一个子目录。  
  
3. 在 Visual Studio 中，创建一个 XML 文件，名为`package.xml`，并将其保存到 C:\package\en 文件夹。  
  
4. 添加 XML 以列出引导程序包的名称、 此本地化的包清单和可选的许可协议的区域性。 下面的 XML 使用的变量`DisplayName`和`Culture`，其定义中的更高版本的元素。  
  
    ```  
    <Package  
        xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"  
        Name="DisplayName"  
        Culture="Culture"  
        LicenseAgreement="eula.txt">  
    ```  
  
5. 添加 XML 以列出特定于区域设置的目录中的所有文件。 下面的 XML 使用的文件，名为适用于 eula.txt **en**区域设置。  
  
    ```  
    <PackageFiles>  
      <PackageFile Name="eula.txt"/>  
    </PackageFiles>  
    ```  
  
6. 添加 XML 以定义引导程序包可本地化的字符串。 下面的 XML 将添加的英语区域设置的错误字符串。  
  
    ```  
      <Strings>  
        <String Name="DisplayName">Custom Bootstrapper Package</String>  
        <String Name="CultureName">en</String>  
        <String Name="NotAnAdmin">You must be an administrator to install   
    this package.</String>  
        <String Name="GeneralFailure">A general error has occurred while   
    installing this package.</String>  
    </Strings>  
    ```  
  
7. C:\package 文件夹复制到 Visual Studio 引导程序目录。 对于 Visual Studio 2010 中，这是 \Program Files\Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages 目录。  
  
## <a name="example"></a>示例  
 包清单包含特定于区域设置的信息，如错误消息、 软件许可条款和语言包。  
  
```  
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
 [产品和包架构引用](../deployment/product-and-package-schema-reference.md)
