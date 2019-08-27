---
title: '&lt;RelatedProducts&gt;元素 （引导程序） |Microsoft Docs'
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
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66747459"
---
# <a name="ltrelatedproductsgt-element-bootstrapper"></a>&lt;RelatedProducts&gt;元素 （引导程序）
`RelatedProducts`元素定义取决于或当前产品中包含其他产品。

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
 `RelatedProducts`元素是子元素的`Product`元素。 它没有任何属性。

## <a name="dependsonproduct"></a>DependsOnProduct
 `DependsOnProduct`元素表示当前产品取决于指定的产品，和之前的当前一个，应安装的命名的产品。 它是子级的`RelatedProducts`元素。 一个`RelatedProducts`元素可能具有一个或多个`DependsOnProduct`元素。

 `DependsOnProduct` 具有以下属性。

|特性|描述|
|---------------|-----------------|
|`Code`|所含的产品，由指定的代号`ProductCode`属性的`Product`元素。 有关详细信息，请参阅[\<产品 > 元素](../deployment/product-element-bootstrapper.md)。|

## <a name="eitherproducts"></a>EitherProducts
 `EitherProducts`元素定义零个或多`DependsOnProduct`元素，并且没有任何特性。 至少一个`DependsOnProduct`本组中之前，必须安装当前产品。 一个`RelatedProducts`元素可以具有零个或多`EitherProducts`元素。

## <a name="includesproduct"></a>IncludesProduct
 `IncludesProduct`元素表示产品包含在当前安装，并且不需要单独安装。 它是子级的`RelatedProducts`元素。 一个`RelatedProducts`元素可能具有一个或多个`IncludesProduct`元素。

 `IncludesProduct` 具有以下属性。

|特性|描述|
|---------------|-----------------|
|`Code`|所含的产品，由指定的代号`ProductCode`属性的`Product`元素。 有关详细信息，请参阅[\<产品 > 元素](../deployment/product-element-bootstrapper.md)。|

## <a name="example"></a>示例
 下面的代码示例指定 Microsoft 安装程序随.NET Framework 中，安装，因此不需要单独安装。

```xml
<RelatedProducts>
    <IncludesProduct Code="Microsoft.Windows.Installer.2.0" />
</RelatedProducts>
```

## <a name="see-also"></a>请参阅
- [\<产品 > 元素](../deployment/product-element-bootstrapper.md)