---
title: "事件 &#39;&lt;eventname1&gt;&#39; 不能实现事件 &#39;&lt;eventname2&gt;&#39; 上接口 &#39;&lt;接口&gt;&#39; 因为它们的委托类型 &#39;&lt;delegate1&gt;&#39; 和 &#39;&lt;delegate2&gt;&#39; 不匹配"
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc31423
- bc31423
helpviewer_keywords: BC31423
ms.assetid: 2e754b66-5836-48ff-9697-b9c0d7085f18
caps.latest.revision: "6"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: b0fcbbf8a6e23270e4dcbf9d813c773e1522a92a
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="event-39lteventname1gt39-cannot-implement-event-39lteventname2gt39-on-interface-39ltinterfacegt39-because-their-delegate-types-39ltdelegate1gt39-and-39ltdelegate2gt39-do-not-match"></a>事件 &#39;&lt;eventname1&gt;&#39; 不能实现事件 &#39;&lt;eventname2&gt;&#39; 上接口 &#39;&lt;接口&gt;&#39; 因为它们的委托类型 &#39;&lt;delegate1&gt;&#39; 和 &#39;&lt;delegate2&gt;&#39; 不匹配
[!INCLUDE[vbprvb](~/includes/vbprvb-md.md)]不能实现某个事件，因为该事件的委托类型不匹配的委托类型的接口中的事件。 如果在接口中定义了多个事件，然后试图用一个事件同时实现这些事件，则可能发生此错误。 只有当所有要实现的事件都使用 `As` 语法进行声明并指定相同的委托类型时，事件才能实现两个或更多个事件。  
  
 **错误 ID:** BC31423  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   单独实现事件。  
  
     - 或 -  
  
-   在接口中使用定义的事件`As`语法并指定相同的委托类型。  
  
## <a name="see-also"></a>另请参阅  
 [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)  
 [Delegate 语句](../../../visual-basic/language-reference/statements/delegate-statement.md)  
 [事件](../../../visual-basic/programming-guide/language-features/events/index.md)
