---
title: "XML 文档对象模型 (DOM) 层次结构"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9d187d4f-c76e-4223-a670-cc290783ce47
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 4d2ffaa994ce3c9b02ed0937967845be1b803f6d
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/23/2017
---
# <a name="xml-document-object-model-dom-hierarchy"></a>XML 文档对象模型 (DOM) 层次结构
下图显示了 XML 文档对象模型 (DOM) 的类层次结构，其中万维网联合会 (W3C) 名称用括号括起来，另外还有相关的类名。  
  
 ![XML 文档对象模型 &#40;DOM&#41; 层次结构](../../../../docs/standard/data/xml/media/dom-class-hierarchy.gif "Dom_class_hierarchy")  
XML 文档对象模型 (DOM) 层次结构  
  
 下列类不继承自 XmlNode：  
  
-   **XmlImplementation**  
  
-   **XmlNamedNodeMap**  
  
-   **XmlNodeList**  
  
-   **XmlNodeChangedEventArgs**  
  
 XmlImplementation 类用于创建 XML 文档。 有关详细信息，请参阅 [XML 文档创建](../../../../docs/standard/data/xml/xml-document-creation.md)。  
  
 XmlNamedNodeMap 类处理无序节点集。 有关详细信息，请参阅[按名称或索引检索无序节点](../../../../docs/standard/data/xml/unordered-node-retrieval-by-name-or-index.md)。  
  
 XmlNodeList 类处理有序节点列表。 有关详细信息，请参阅[按索引检索有序节点](../../../../docs/standard/data/xml/ordered-node-retrieval-by-index.md)。  
  
 XmlNodeChangedEventArgs 类处理在 XmlDocument 上注册的事件处理程序。 有关详细信息，请参阅[使用 XmlNodeChangedEventArgs 在 XML 文档中处理事件](../../../../docs/standard/data/xml/event-handling-in-an-xml-document-using-the-xmlnodechangedeventargs.md)。  
  
 XmlLinkedNode 类继承自 XmlNode。 它用于重写 XmlNode 中的两个方法：PreviousSibling 和 NextSibling 方法。 然后，这些重写方法由包含上一个和下一个同级的类 XmlCharacterData、XmlDeclaration、XmlDocumentType、XmlElement、XmlEntityReference 和 XmlProcessingInstruction 继承和使用。  
  
## <a name="see-also"></a>请参阅  
 [XML 文档对象模型 (DOM)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
