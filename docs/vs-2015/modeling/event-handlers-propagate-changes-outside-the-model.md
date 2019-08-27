---
title: 事件处理程序模型外部传播更改 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming domain models
- Domain-Specific Language, events
ms.assetid: 0ac8d1e4-239f-4370-ba1d-3769bb38b8a5
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 24ef57b545360cccbf75039b5f64a0f53e636dd8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68181756"
---
# <a name="event-handlers-propagate-changes-outside-the-model"></a>事件处理程序在模型外部传播更改
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在可视化和建模 SDK，你可以定义存储事件处理程序将更改传播到应用商店中，如非存储变量、 文件、 模型中其他存储，或其他外部资源[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]扩展。 存储的事件处理程序在其中触发事件发生在事务结束后执行。 它们还可在撤消或重做操作。 因此，应用商店与规则不同，存储事件是最适用于更新商店外的值。 .NET 与事件不同，存储事件处理程序注册为侦听到类： 无需注册每个实例的单独处理程序。 有关如何选择不同的方式来处理更改之间的详细信息，请参阅[对的响应并传播更改](../modeling/responding-to-and-propagating-changes.md)。  
  
 图形表面和其他用户界面控件是可以由存储事件的外部资源的示例。  
  
### <a name="to-define-a-store-event"></a>若要定义的存储事件  
  
1. 选择你想要监视的事件的类型。 有关完整列表，请查看的属性<xref:Microsoft.VisualStudio.Modeling.EventManagerDirectory>。 每个属性对应于事件的类型。 最常用的事件类型包括：  
  
   - `ElementAdded` – 当模型元素时，触发，关系链接、 形状或连接线创建。  
  
   - ElementPropertyChanged – 触发时的值`Normal`更改域属性。 仅当新的和旧值不相等，则触发事件。 该事件不能应用于计算的和自定义存储属性。  
  
        它不能应用于对应于关系链接在角色属性。 请改用`ElementAdded`要监视的域关系。  
  
   - `ElementDeleted` – 模型元素后触发，关系、 形状或连接线已被删除。 您仍然可以访问的属性值的元素，但它将具有与其他元素的任何关系。  
  
2. 添加的分部类定义_YourDsl_**DocData**单独的代码文件中**DslPackage**项目。  
  
3. 作为方法，如以下示例所示编写事件代码。 它可以是`static`，除非你想要访问`DocData`。  
  
4. 重写`OnDocumentLoaded()`注册处理程序。 如果你有多个处理程序，可以在同一位置进行注册。  
  
   注册代码的位置并不重要。 `DocView.LoadView()` 是另一个位置。  
  
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
  
## <a name="using-events-to-make-undoable-adjustments-in-the-store"></a>使用事件存储区中进行可撤消的调整  
 存储事件不通常用于传播更改，在存储，因为事件处理程序执行提交事务后。 相反，将使用的存储规则。 有关详细信息，请参阅[规则将传播的更改中的模式](../modeling/rules-propagate-changes-within-the-model.md)。  
  
 但是，您可以使用事件处理程序来做其他更新，到应用商店中，如果您希望用户能够撤消独立于原始事件的其他更新。 例如，假设的小写字符均唱片集标题的常见约定。 你可以编写的应用商店事件处理程序后用户已将它以大写形式键入更正为小写形式的标题。 但用户可以使用撤消命令以取消所做的更正，还原大写字符。 第二个撤消会删除用户的更改。  
  
 与此相反，如果您编写了一个存储规则，以执行相同的操作，用户的更改和所做的更正应该在同一事务中，以便用户无法撤消而不会丢失原始更改的调整。  
  
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
  
 如果您编写更新存储的事件：  
  
- 使用`store.InUndoRedoOrRollback`若要避免更改中撤消的模型元素。 事务管理器将恢复到其原始状态存储中设置的所有内容。  
  
- 使用`store.InSerializationTransaction`若要避免从文件加载模型时更改。  
  
- 所做的更改将导致更多的事件触发。 请确保避免无限循环。  
  
## <a name="store-event-types"></a>存储事件类型  
 每个事件类型对应于 Store.EventManagerDirectory 中的集合。 可以添加或移除事件处理程序在任何时候，但通常要将文档加载时添加它们。  
  
|`EventManagerDirectory` 属性名称|时执行|  
|-------------------------------------------|-------------------|  
|ElementAdded|创建域类、 域关系、 形状、 连接符或关系图的实例。|  
|ElementDeleted|模型元素已从存储的元素目录中删除，不再源或目标的任何关系。 元素不实际从内存中删除，但会保留在以后撤消。|  
|ElementEventsBegun|外部事务结束时调用。|  
|ElementEventsEnded|当处理完所有其他事件时调用。|  
|ElementMoved|模型元素已从一个存储分区移动到另一个。<br /><br /> 这没有与关系图上形状的位置。|  
|ElementPropertyChanged|域属性的值已更改。 这被执行仅当旧的和新值不相等。|  
|RolePlayerChanged|关系的两个角色 （结束） 之一引用的新元素。|  
|RolePlayerOrderChanged|在角色中具有多重性大于 1，已更改的一系列链接。|  
|TransactionBeginning||  
|TransactionCommitted||  
|TransactionRolledBack||  
  
## <a name="see-also"></a>请参阅  
 [响应并传播更改](../modeling/responding-to-and-propagating-changes.md)   
 [示例代码：线路关系图](http://code.msdn.microsoft.com/Visualization-Modeling-SDK-763778e8)
