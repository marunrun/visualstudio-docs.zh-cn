---
title: 事件处理程序在模型外部传播更改 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming domain models
- Domain-Specific Language, events
ms.assetid: 0ac8d1e4-239f-4370-ba1d-3769bb38b8a5
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a23a8d28f336728789fe9cbbe38f965cc56763d7
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295516"
---
# <a name="event-handlers-propagate-changes-outside-the-model"></a>事件处理程序在模型外部传播更改
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在可视化和建模 SDK 中，可以定义存储事件处理程序以将更改传播到存储区之外的资源，例如非存储变量、文件、其他存储中的模型或其他 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 扩展。 存储事件处理程序在触发事件发生的事务结束后执行。 还会在撤消或重做操作中执行这些操作。 因此，与存储规则不同，存储事件对于更新存储区之外的值最为有用。 与 .NET 事件不同，存储事件处理程序已注册为侦听类：不必为每个实例注册单独的处理程序。 有关如何在不同方式之间进行选择以处理更改的详细信息，请参阅[响应和传播更改](../modeling/responding-to-and-propagating-changes.md)。

 图形表面和其他用户界面控件是可通过存储事件处理的外部资源的示例。

### <a name="to-define-a-store-event"></a>定义存储事件

1. 选择要监视的事件类型。 有关完整列表，请查看 <xref:Microsoft.VisualStudio.Modeling.EventManagerDirectory>的属性。 每个属性都对应于一种事件类型。 最常使用的事件类型包括：

   - `ElementAdded` –当创建模型元素、关系链接、形状或连接符时触发。

   - ElementPropertyChanged –在 `Normal` 域属性的值发生更改时触发。 仅当新值和旧值不相等时，才会触发事件。 事件不能应用于计算的存储属性和自定义存储属性。

        它不能应用于与关系链接对应的角色属性。 请改用 `ElementAdded` 来监视域关系。

   - `ElementDeleted` –在删除模型元素、关系、形状或连接符后触发。 你仍可访问元素的属性值，但它不与其他元素建立关系。

2. 将_yourdsl 可_**DocData**的分部类定义添加到**DslPackage**项目的单独代码文件中。

3. 以方法的形式编写事件代码，如以下示例中所示。 它可以 `static`，除非你想要访问 `DocData`。

4. 重写 `OnDocumentLoaded()` 以注册处理程序。 如果有多个处理程序，则可以将它们全部注册到同一位置。

   注册代码的位置并不重要。 `DocView.LoadView()` 是一种替代位置。

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.VisualStudio.Modeling;

namespace Company.MusicLib
{
  partial class MusicLibDocData
  {
    // Register store events here or in DocView.LoadView().
    protected override void OnDocumentLoaded()
    {
      base.OnDocumentLoaded(); // Don’t forget this.

      #region Store event handler registration.
      Store store = this.Store;
      EventManagerDirectory emd = store.EventManagerDirectory;
      DomainRelationshipInfo linkInfo = store.DomainDataDirectory
          .FindDomainRelationship(typeof(ArtistAppearsInAlbum));
      emd.ElementAdded.Add(linkInfo,
          new EventHandler<ElementAddedEventArgs>(AddLink));
      emd.ElementDeleted.Add(linkInfo,
          new EventHandler<ElementDeletedEventArgs>(RemoveLink));

      #endregion Store event handlers.
    }

    private void AddLink(object sender, ElementAddedEventArgs e)
    {
      ArtistAppearsInAlbum link = e.ModelElement as ArtistAppearsInAlbum;
      if (link != null)
            ExternalDatabase.Add(link.Artist.Name, link.Album.Title);
    }
    private void RemoveLink(object sender, ElementDeletedEventArgs e)
    {
      ArtistAppearsInAlbum link = e.ModelElement as ArtistAppearsInAlbum;
      if (link != null)
            ExternalDatabase.Delete(link.Artist.Name, link.Album.Title);
    }
  }

}

```

## <a name="using-events-to-make-undoable-adjustments-in-the-store"></a>使用事件在存储中进行可撤消的调整
 存储事件通常不用于传播存储区中的更改，因为在提交事务后，事件处理程序会执行。 相反，应使用存储规则。 有关详细信息，请参阅[规则在模型内部传播更改](../modeling/rules-propagate-changes-within-the-model.md)。

 但是，如果您希望用户能够从原始事件中单独撤消其他更新，则可以使用事件处理程序对存储区进行其他更新。 例如，假设小写字符是唱片集标题的常见约定。 您可以编写一个存储事件处理程序，用于在用户键入大写后将标题更正为小写。 但是，用户可以使用 "撤消" 命令取消您的更正，同时还原大写字符。 第二次撤消会删除用户的更改。

 与此相反，如果你编写了一个用于执行相同操作的存储规则，则用户的更改和更正将在同一事务中，因此用户无法在不丢失原始更改的情况下撤消调整。

```

partial class MusicLibDocView
{
    // Register store events here or in DocData.OnDocumentLoaded().
    protected override void LoadView()
    {
      /* Register store event handler for Album Title property. */
      // Get reflection data for property:
      DomainPropertyInfo propertyInfo =
        this.DocData.Store.DomainDataDirectory
        .FindDomainProperty(Album.TitleDomainPropertyId);
      // Add to property handler list:
      this.DocData.Store.EventManagerDirectory
        .ElementPropertyChanged.Add(propertyInfo,
        new EventHandler<ElementPropertyChangedEventArgs>
             (AlbumTitleAdjuster));

      /*
      // Alternatively, you can set one handler for
      // all properties of a class.
      // Your handler has to determine which property changed.
      DomainClassInfo classInfo = this.Store.DomainDataDirectory
           .FindDomainClass(typeof(Album));
      this.Store.EventManagerDirectory
          .ElementPropertyChanged.Add(classInfo,
        new EventHandler<ElementPropertyChangedEventArgs>
             (AlbumTitleAdjuster));
       */
      return base.LoadView();
    }

// Undoable adjustment after a property is changed.
// Method can be static since no local access.
private static void AlbumTitleAdjuster(object sender,
         ElementPropertyChangedEventArgs e)
{
  Album album = e.ModelElement as Album;
  Store store = album.Store;

  // We mustn't update the store in an Undo:
  if (store.InUndoRedoOrRollback
      || store.InSerializationTransaction)
      return;

  if (e.DomainProperty.Id == Album.TitleDomainPropertyId)
  {
    string newValue = (string)e.NewValue;
    string lowerCase = newValue.ToLowerInvariant();
    if (!newValue.Equals(lowerCase))
    {
      using (Transaction t = store.TransactionManager
            .BeginTransaction("adjust album title"))
      {
        album.Title = lowerCase;
        t.Commit();
      } // Beware! This could trigger the event again.
    }
  }
  // else other properties of this class.
}

```

 如果编写更新存储的事件：

- 使用 `store.InUndoRedoOrRollback` 避免在撤消中更改模型元素。 事务管理器会将存储中的所有内容设置回其原始状态。

- 使用 `store.InSerializationTransaction` 可以避免在从文件中加载模型时进行更改。

- 更改将导致触发更多事件。 请确保避免出现无限循环。

## <a name="store-event-types"></a>存储事件类型
 每个事件类型对应于 EventManagerDirectory 中的一个集合。 你可以随时添加或删除事件处理程序，但在加载文档时通常会添加它们。

|`EventManagerDirectory` 属性名称|执行时间|
|-------------------------------------------|-------------------|
|ElementAdded|将创建域类、域关系、形状、连接符或关系图的实例。|
|ElementDeleted|模型元素已从存储的元素目录中移除，不再是任何关系的源或目标。 实际不会从内存中删除该元素，但会在将来撤消时保留。|
|ElementEventsBegun|在外部事务结束时调用。|
|ElementEventsEnded|在处理完所有其他事件后调用。|
|ElementMoved|模型元素已从一个存储区分区移到另一个。<br /><br /> 这与关系图上形状的位置无关。|
|ElementPropertyChanged|域属性的值已更改。 仅当旧值和新值不相等时，才执行此值。|
|RolePlayerChanged|关系的两个角色（结束）之一引用新元素。|
|RolePlayerOrderChanged|在多重性大于1的角色中，链接序列已更改。|
|TransactionBeginning||
|TransactionCommitted||
|TransactionRolledBack||

## <a name="see-also"></a>请参阅
 [响应并传播更改](../modeling/responding-to-and-propagating-changes.md)
