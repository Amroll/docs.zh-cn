---
title: "ICorProfilerCallback::ClassLoadFinished 方法"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name:
- ICorProfilerCallback.ClassLoadFinished
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ClassLoadFinished
helpviewer_keywords:
- ClassLoadFinished method [.NET Framework profiling]
- ICorProfilerCallback::ClassLoadFinished method [.NET Framework profiling]
ms.assetid: 3dd80fbe-d62d-4d4d-acf8-5b7d0efe607e
topic_type:
- apiref
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: ae55325f514f9bec3efdf4764958e4b3fafd922b
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2017
---
# <a name="icorprofilercallbackclassloadfinished-method"></a>ICorProfilerCallback::ClassLoadFinished 方法
通知探查器加载已完成某个类。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT ClassLoadFinished(  
    [in] ClassID classId,  
    [in] HRESULT hrStatus);  
```  
  
#### <a name="parameters"></a>参数  
 `classId`  
 [in]标识已加载的类。  
  
 `hrStatus`  
 [in]一个 HRESULT，指示类是否成功加载。  
  
## <a name="remarks"></a>备注  
 值`classId`无效的信息请求之前，不能`ClassLoadFinished`调用方法。  
  
 加载类的某些部分可能会继续之后`ClassLoadFinished`回调。 失败的 HRESULT 在`hrStatus`指示失败。 但是，HRESULT 为成功，在`hrStatus`仅指示已成功加载类的第一部分。  
  
## <a name="requirements"></a>惠?  
 **平台：**请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **头文件：** CorProf.idl、CorProf.h  
  
 **库：** CorGuids.lib  
  
 **.NET framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [ICorProfilerCallback 接口](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)  
 [ClassLoadStarted 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-classloadstarted-method.md)
