---
title: '&lt;&gt; (引导程序) 的 RelatedProducts 元素 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- MSBuild.GenerateBootstrapper.MissingDependency
- MSBuild.GenerateBootstrapper.DuplicateItems
- MSBuild.GenerateBootstrapper.IncludedProductIncluded
- MSBuild.GenerateBootstrapper.DependencyNotFound
- MSBuild.GenerateBootstrapper.PackageFileNotFound
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <RelatedProducts> element [bootstrapper]
ms.assetid: bf152712-4c1e-48bd-9b7f-311cf0fdb832
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 42756b21e631ec14e9c590833f6f0e95a317cc22
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "66747459"
---
# <a name="ltrelatedproductsgt-element-bootstrapper"></a>&lt;RelatedProducts &gt; 元素 (引导程序) 
`RelatedProducts`元素定义其他产品，这些产品依赖于或包含在当前产品中。

## <a name="syntax"></a>语法

```xml
<RelatedProducts>
    <DependsOnProduct
        Code
    />
    <EitherProducts>
        <DependsOnProduct
            Code
        />
    </EitherProducts>
    <IncludesProduct
        Code
    />
</RelatedProducts>
```

## <a name="elements-and-attributes"></a>元素和属性
 `RelatedProducts`元素是元素的子元素 `Product` 。 它没有属性。

## <a name="dependsonproduct"></a>DependsOnProduct
 `DependsOnProduct`元素指示当前产品依赖于命名产品，并且应在当前的产品之前安装该产品。 它是元素的子 `RelatedProducts` 元素。 `RelatedProducts`元素可能有一个或多个 `DependsOnProduct` 元素。

 `DependsOnProduct` 具有以下属性。

|特性|说明|
|---------------|-----------------|
|`Code`|由元素的特性指定的所包含产品的代码名称 `ProductCode` `Product` 。 有关详细信息，请参阅 [\<Product> 元素](../deployment/product-element-bootstrapper.md)。|

## <a name="eitherproducts"></a>EitherProducts
 `EitherProducts`元素定义零个或多个 `DependsOnProduct` 元素，但没有属性。 `DependsOnProduct`在当前产品之前，必须先安装此集中的至少一个。 `RelatedProducts`元素可以包含零个或多个 `EitherProducts` 元素。

## <a name="includesproduct"></a>IncludesProduct
 `IncludesProduct`元素表示产品包含在当前安装中，无需单独安装。 它是元素的子 `RelatedProducts` 元素。 `RelatedProducts`元素可能有一个或多个 `IncludesProduct` 元素。

 `IncludesProduct` 具有以下属性。

|特性|说明|
|---------------|-----------------|
|`Code`|由元素的特性指定的所包含产品的代码名称 `ProductCode` `Product` 。 有关详细信息，请参阅 [\<Product> 元素](../deployment/product-element-bootstrapper.md)。|

## <a name="example"></a>示例
 下面的代码示例指定与 .NET Framework 一起安装 Microsoft 安装程序，因此不需要单独安装。

```xml
<RelatedProducts>
    <IncludesProduct Code="Microsoft.Windows.Installer.2.0" />
</RelatedProducts>
```

## <a name="see-also"></a>另请参阅
- [\<Product> element](../deployment/product-element-bootstrapper.md)