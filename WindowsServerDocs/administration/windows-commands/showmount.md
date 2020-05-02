---
title: showmount
description: 탑재 된 디렉터리를 표시 하는 showmount에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a6dd562e-e3bd-4ee6-be3b-6d29e29fd20e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 60057c154e7a646d14a0e57d5cf4cd72d0f90876
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721810"
---
# <a name="showmount"></a>showmount

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사용할 수 있습니다 **showmount** 탑재 된 디렉터리를 표시 합니다.  
  
## <a name="syntax"></a>구문  
```
showmount {-e|-a|-d} <Server>  
```

## <a name="description"></a>Description  
**showmount** 명령\-로 지정 된 컴퓨터에서 NFS 용 서버에서 내보낸 마운트된 파일 시스템에 대 한 정보를 표시 하는 명령줄 유틸리티 *서버*합니다. 경우 *서버* 를 제공 하지 않으면 **showmount** 있는 컴퓨터에 대 한 정보를 표시는 **showmount** 명령을 실행 합니다.  
  
다음 옵션 중 하나를 제공 해야 합니다.  
  
- e-서버에서 내보낸 모든 파일 시스템을 표시 합니다. ** \-**  
- a-모든 네트워크 파일 시스템 \(NFS\) 클라이언트와 각 서버에서 탑재 된 디렉터리를 표시 합니다. ** \-**  
- d-서버에서 현재 NFS 클라이언트에 탑재 된 모든 디렉터리를 표시 합니다. ** \-**  
  
## <a name="see-also"></a>참고 항목  
[네트워크 파일 시스템 서비스 명령 참조](services-for-network-file-system-command-reference.md)  