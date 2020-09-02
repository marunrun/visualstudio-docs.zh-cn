---
title: 如何：创建包清单 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153836"
---
# <a name="how-to-create-a-package-manifest"></a>如何：创建程序包清单
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

若要为应用程序部署先决条件，可以使用引导程序包。 引导程序包包含单个产品清单文件，但每个区域设置都包含包清单。 不同本地化版本间的共享功能应进入产品清单。  
  
 有关包清单的详细信息，请参阅 [如何：创建产品清单](../deployment/how-to-create-a-product-manifest.md)。  
  
## <a name="creating-the-package-manifest"></a>创建包清单  
  
#### <a name="to-create-the-package-manifest"></a>创建包清单  
  
1. 为引导程序包创建目录。 此示例使用 C:\package。  
  
2. 使用区域设置的名称创建一个子目录，如英语。  
  
3. 在 Visual Studio 中，创建一个名为的 XML 文件 `package.xml` ，并将其保存到 C:\package\en 文件夹中。  
  
4. 添加 XML 以列出引导程序包的名称、此本地化包清单的区域性以及可选的许可协议。 下面的 XML 使用 `DisplayName` `Culture` 在后面的元素中定义的变量和。  
  
    ```  
    <Package  
        xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"  
        Name="DisplayName"  
        Culture="Culture"  
        LicenseAgreement="eula.txt">  
    ```  
  
5. 添加 XML 以列出区域设置特定目录中的所有文件。 下面的 XML 使用名为 eula.txt 的文件，该文件适用于 **en** 区域设置。  
  
    ```  
    <PackageFiles>  
      <PackageFile Name="eula.txt"/>  
    </PackageFiles>  
    ```  
  
6. 添加 XML 以定义引导程序包的可本地化字符串。 下面的 XML 为 en 区域设置添加错误字符串。  
  
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
  
7. 将 C:\package 文件夹复制到 Visual Studio 引导程序目录。 对于 Visual Studio 2010，这是 \Program Files\Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages 目录。  
  
## <a name="example"></a>示例  
 包清单包含特定于区域设置的信息，如错误消息、软件许可条款和语言包。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [产品和包架构引用](../deployment/product-and-package-schema-reference.md)
