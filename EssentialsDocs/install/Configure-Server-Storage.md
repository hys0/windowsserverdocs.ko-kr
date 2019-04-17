---
title: "서버 저장소 구성"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef7ddcdd-3a74-40ca-9487-c3a6fc5155a5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6de485f6fd46464ba707bc0871f60ac2fec5a1db
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="configure-server-storage"></a>서버 저장소 구성

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

## <a name="sample-hard-disk-configurations"></a>샘플 하드 디스크 구성  
 다음 표에서 제안 샘플 하드 디스크 구성 합니다. 예상치 일반적인 사용 및 기능을 기반으로 있지만 최적 성능에 영향을 주는 문제 해결 하지 않습니다. 모든 종류의 지원 되는 하드 디스크가이 구성 (예: SATA 또는 SCSI)에 대 한 기본 설정 및 고객의 요구에 따라 사용할 수 있습니다.  
  
> [!IMPORTANT]
>   Windows Server Essentials로 c: 볼륨을 설치 해야 하 고 볼륨의 크기 60 g B 이상 이어야 합니다. 운영 체제 디스크에 두 가지 파티션을 만드는 하지 비즈니스 데이터를 저장할 c: (시스템 파티션)를 사용 하는 것이 좋습니다.  
  
|서버 수준|디스크 구성|  
|------------------|------------------------|  
|항목|-실제 디스크 2<br /><br /> 다음을 포함 하 미러 RAID 1 집합으로 구성 다음과 같습니다.<br /><br /> -C: 볼륨? 60 G B<br /><br /> -D: 볼륨? 1000 G B|  
|보통|3 세 실제 디스크<br /><br /> 다음을 포함 하 여 RAID 5 집합으로 구성 다음과 같습니다.<br /><br /> -C: 볼륨? 60 G B<br /><br /> -D: 볼륨? 1500 G B|  
|높은|-5 개 이상의 총 실제 디스크<br /><br /> -RAID 1에서 2 디스크 미러링할 c: 볼륨 포함 된 집합? 100 G B<br /><br /> -다음을 포함 RAID 5 세트에 모든 남은 디스크가 다음과 같습니다.<br /><br /> -D: 볼륨? 1500 G B<br /><br /> -E: 볼륨? 1500 G B|  
  
 이러한 권장 고려해 설치 된 운영 체제의 크기를 평균 크기 서버를 사용 하는 데이터 스토리지와 서버의 수명 주기 동안 예상 되는 데이터 저장소 성장 합니다. 볼륨 단일 실제 디스크에 파티션 또는 별도 실제 디스크에 배치 될 수 있습니다. 고객에 대 한 중요 한 데이터를 저장 하는 서버, 여러 실제 디스크를 사용 하 고 하드웨어 RAID 또는 저장소 공간을 사용 하 여 고객의 데이터를 보호 하는 데 도움이 것이 좋습니다.  
  
## <a name="configuring-your-server-backup"></a>서버 백업 구성  
 서버에 내장 하드 디스크, 뿐만 아니라 백업에 외장형 USB 하드 디스크를 사용 하 여 고객 고려해 야 합니다. 고객 두 개 이상의 외장형 하드 디스크 서버에 데이터를 모두 백업 용량이 부족 한 것이 가장 좋습니다 합니다. 외장형 하드 디스크를 사용 하는 추가 데이터를 보호 하 고 각 밤 고객 디스크 오프 한 걸릴 수 있습니다.  
  
## <a name="partition-configuration"></a>파티션 구성  
 서버에 대 한 초기 구성 하는 동안 클라이언트 컴퓨터 백업 폴더와 공유 폴더를 포함 하는 기본 서버 폴더의 설정에 0 디스크에 가장 큰 데이터 파티션을 만들어집니다.  
  
## <a name="see-also"></a>참조 하십시오  

 [Windows Server Essentials ADK 시작](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)

 [Windows Server Essentials ADK 시작](../install/Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [만들기 및 이미지를 사용자 지정](../install/Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](../install/Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](../install/Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](../install/Testing-the-Customer-Experience.md)

