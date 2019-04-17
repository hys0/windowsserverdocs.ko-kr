---
ms.assetid: 73897497-b189-4305-b234-e057ffda163a
title: "도메인 이름 지정 하는 방법"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0d5ec9b76798f21503f650527a7961cff0b592b4
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="assigning-domain-names"></a>도메인 이름 지정 하는 방법

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

요금제에 모든 도메인에 이름을 지정 해야 있습니다. Active Directory DS (도메인 서비스 AD) 도메인 두 가지 유형의 이름: 시스템 DNS (도메인 이름) 이름과 NetBIOS 이름입니다. 일반적으로 두 이름이 최종 사용자에 게 표시 됩니다. DNS 이름을 Active Directory 도메인 접두사와 접미사 두 부분으로 포함 됩니다. 도메인 이름을 만들 때 DNS 접두사 먼저 확인 합니다. 첫 번째 레이블이 DNS 도메인 이름입니다. 숲 루트 도메인의 이름을 선택 접미사 결정 됩니다. 다음 표에서 접두사 규칙 DNS 이름에 이름을 지정 합니다.  
  
|규칙|설명|  
|--------|---------------|  
|오래 된 것일 가능성이 있는 접두사를 선택 합니다.|이름을 제품군 또는 나중에 변경할 수 있는 운영 체제 등 사용 하지 마십시오. 지리 명을 사용 하는 것이 좋습니다.|  
|표준 문자만 인터넷 포함 된 접두사를 선택 합니다.|A Z, z 한 0-9, 하 고 (-) 있지만 완전히 숫자 되지 않습니다.|  
|15 문자가 포함 이하의 접두사에 있습니다.|접두사 길이 15 자 이하로 선택 하면 NetBIOS 이름은 접두사와 동일 합니다.|  
  
자세한 내용은 참조 명명 규칙 컴퓨터에서 도메인, 사이트 및 Ou에 대 한 Active directory에서 ([https://go.microsoft.com/fwlink/?LinkId=106629](https://go.microsoft.com/fwlink/?LinkId=106629)).  
  
> [!NOTE]  
>  Windows Server 2008 및 Windows Server 2003 Dcpromo.exe 단일 레이블 DNS 도메인 이름 만들 수 있도록, 있지만 몇 가지 이유로 도메인에 대 한 단일 레이블 DNS 이름의 사용 하지 해야 합니다. Windows Server 2008 r 2에 Dcpromo.exe은 도메인에 대 한 단일 레이블 DNS 이름을 만들 수 없습니다. 자세한 내용은 참조 [https://go.microsoft.com/fwlink/?LinkId=92467 합니다.](https://go.microsoft.com/fwlink/?LinkId=92467)   
  
현재 NetBIOS 이름을 도메인의 나타낼 영역 적합 하지 않은 규칙 명명 접두사 만족 하지 못한 경우 새 접두사를 선택 합니다. 이 경우 도메인 NetBIOS 이름을 도메인의 DNS 접두사 다릅니다.  
  
배포 하는 각 새로운 도메인 이름 지정 규칙 접두사 충족 하는 지역에 대 한 적절 한 접두사를 선택 합니다. 도메인의 NetBIOS 이름 DNS 접두사와 동일 하는 것이 좋습니다.  
  
DNS 접두사와 NetBIOS 이름을 선택 하 여 숲 속의 각 도메인 기록 합니다. 새롭고 업그레이드 도메인에 대 한 계획을 문서를 작성 하는 "도메인 계획" 워크시트 DNS 및 NetBIOS 이름 정보를 추가할 수 있습니다. 다운로드 Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip 작업 보조 기능에 대 한 Windows Server 2003 Deployment Kit에서 ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)) "도메인 계획" (DSSLOGI_5.doc).  
  


