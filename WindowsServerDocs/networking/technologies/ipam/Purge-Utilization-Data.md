---
title: 사용률 데이터 제거
description: 이 항목은 Windows Server 2016의 IPAM (IP 주소 관리) 관리 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45cada9e-69b9-43df-b6f5-6d3942435809
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9e1db31e4d2d714c358f2a67c2165aef91b314ba
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405607"
---
# <a name="purge-utilization-data"></a>사용률 데이터 제거

>적용 대상: Windows Server(반기 채널), Windows Server 2016

IPAM 데이터베이스에서 사용률 데이터를 삭제 하는 방법에 알아보려면이 항목을 사용할 수 있습니다.  

멤버 여야 **IPAM 관리자**, 로컬 컴퓨터 **관리자** 이 절차를 수행 하려면 그룹 또는 이와 동등한 합니다.

## <a name="to-purge-the-ipam-database"></a>IPAM 데이터베이스를 제거 하려면  
1. 서버 관리자를 열고 IPAM 클라이언트 인터페이스를 찾습니다.
2. 다음 위치 중 하나를 찾아봅니다. Ip **주소 블록**, **ip 주소 인벤토리**또는 **ip 주소 범위 그룹**  
3. 클릭 **작업**, 를 클릭 하 고 **사용률 데이터를 제거**합니다. **사용률 데이터 지우기** 대화 상자가 열립니다.
4. **모든 사용률을 제거 또는 그 이전에 데이터**, 클릭 **날짜 선택**합니다.
5. 와 모두에서 날짜 이전에 모든 데이터베이스 레코드를 삭제 하려는 날짜를 선택 합니다.
6. **확인**을 클릭합니다. IPAM 사용자가 지정한 모든 레코드를 삭제 합니다.
