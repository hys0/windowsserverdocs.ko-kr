---
title: 활용 데이터 지우기
description: 이 항목은 Windows Server 2016에는 IP 주소 관리 (IPAM) 관리 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45cada9e-69b9-43df-b6f5-6d3942435809
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c41be119099aed4867df1bae1a55e2fbaa5c9064
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="purge-utilization-data"></a>활용 데이터 지우기

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 IPAM 데이터베이스의 데이터 사용량을 삭제 하는 방법을 알아보려면 사용할 수 있습니다.  

소속 있어야 **IPAM 관리자**, 로컬 컴퓨터 **관리자** 이 절차를 수행 하는 그룹 또는 오른쪽 단추를 클릭 합니다.

## <a name="to-purge-the-ipam-database"></a>IPAM 데이터베이스를 제거 하기  
1. 서버 관리자를 열고 IPAM 클라이언트 인터페이스를 찾습니다.
2. 다음 위치 중 하나를 찾아: **IP 주소 블록**, **IP 주소 인벤토리**, 또는 **IP 주소 범위 그룹**합니다.  
3. 클릭 **작업**을 차례로 클릭 하 고 **활용도 데이터 지우기**합니다. **활용도 데이터 지우기** 대화 상자를 엽니다.
4. **모든 활용도 지우기 또는 그 이전에 데이터**, 클릭 **날짜를 선택**합니다.
5. 날짜에 및 날짜 전에 모든 데이터베이스 기록이 삭제를 선택 합니다.
6. 클릭 **확인**합니다. IPAM 지정 된 모든 기록이 삭제 됩니다.
