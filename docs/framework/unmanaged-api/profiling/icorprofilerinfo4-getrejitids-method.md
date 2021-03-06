---
title: "ICorProfilerInfo4::GetReJITIDs 方法"
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
- ICorProfilerInfo4.GetReJITIDs
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4::GetReJITIDs
helpviewer_keywords:
- GetReJITIDs method, ICorProfilerInfo4 interface [.NET Framework profiling]
- ICorProfilerInfo4::GetReJITIDs method [.NET Framework profiling]
ms.assetid: 634ac28c-a5b7-4fc3-af84-256c24ca8177
topic_type:
- apiref
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: fb1e507bea6f52e4959f241f1507807a76c0ec5a
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2017
---
# <a name="icorprofilerinfo4getrejitids-method"></a>ICorProfilerInfo4::GetReJITIDs 方法
返回一个标识 JIT 重新编译的所有版本的指定的函数仍分配的 Id 数组。 这包括已随后还原但尚未释放 （例如，应用程序域时包含已还原的函数仍在使用） 的函数的 JIT 重新编译的版本。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT GetReJITIDs (  
     [in]  FunctionID          functionId,  
     [in]  ULONG               cReJitIds,  
     [out] ULONG *             pcReJitIds,  
     [out, size_is(cReJitIds), length_is(*pcReJitIds)]   ReJITID        reJitIds[]);  
```  
  
#### <a name="parameters"></a>参数  
 `functionId`  
 [in]`FunctionID`的枚举版本的函数实例。  
  
 `cReJitIds`  
 [in]在中分配的 JIT 重新编译的 Id 数`reJitIds`数组。  
  
 `pcReJitIds`  
 [out]JIT 重新编译的 Id 的实际数。  
  
 `reJitIds`  
 [out]调用方分配的数组将包含指定的函数的 JIT 重新编译 Id。  
  
## <a name="remarks"></a>备注  
 `GetReJITIDs`枚举给定的函数实例的活动的 JIT 重新编译 Id。 它遵循相同的使用情况模式与其他`ICorProfilerInfo`接受调用方分配的缓冲区的函数。  
  
## <a name="requirements"></a>惠?  
 **平台：**请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **头文件：** CorProf.idl、CorProf.h  
  
 **库：** CorGuids.lib  
  
 **.NET framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [ICorProfilerInfo4 接口](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-interface.md)  
 [Profiling 接口](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)  
 [分析](../../../../docs/framework/unmanaged-api/profiling/index.md)
