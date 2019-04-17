---
title: "Windows Server 2012 r 2 표준 Windows Server Essentials에서 전환"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a14689e3-2310-4229-bd3e-dafc0e739e02
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d371e24b17310c0687666185f56fe07a135ff91f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="transition-from-windows-server-essentials-to-windows-server-2012-r2-standard"></a>Windows Server 2012 r 2 표준 Windows Server Essentials에서 전환

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

Windows Server 2016 쉽게 클라우드 컴퓨팅로 전환 하는 새로운 기술 소개 하는 동안 현재 작업을 지 원하는 클라우드 운영 체제입니다. Windows Server 2016 콘텐츠 준비 하는 데 도움이 됩니다.

 Windows Server Essentials 25 명의 사용자와 장치 50까지 지원합니다. 비즈니스 요구 제한을 초과 하는 경우 Windows Server 2012 r 2 표준 라이선스 호환 되도록 하는 현재 위치에서 라이선스 전환 Windows Server Essentials에서 수행할 수 있습니다.  
  
 Windows Server 2012 r 2 표준 모드로 전환 하면 후 사용자 계정 및 디바이스 제한, 제거 되지만 (예: 대시보드, 원격 Web Access 및 클라이언트 컴퓨터 백업) Windows Server Essentials에 고유 하 게 포함 된 기능에도 계속 사용할 수 있습니다. 하지만 이러한 기능에 대 한 기술적 제한 사항을 최대 100 사용자 계정 및 200 장치를 지원합니다. 75 최대 디바이스를 백업 클라이언트 컴퓨터 백업 기능을 지원 합니다.  
  
> [!IMPORTANT]
>   Windows Server 2012 r 2 표준 각 사용자 또는 사용자 환경에서 디바이스에 대 한 클라이언트 액세스 라이선스 CAL ()를 필요합니다. 이 Windows Server Essentials CAL 모델을 사용 하지 않는 모든 Cal와 함께 제공 되지 않는 이며 다릅니다. Windows Server Essentials에서 Windows Server 2012 r 2 표준로 전환 때 (대부분의 고객 사용자 Cal 구매) 귀하의 환경에 대 한 Cal의 종류와 적절 한 수를 구입 해야 합니다.  
  
## <a name="before-the-transition"></a>전환 하기 전에  
  
-   Windows Server Essentials에서 Windows Server 2012 r 2 표준로 전환, 하기 전에 서버 데이터를 완전히 백업 해야 합니다.  
  
    > [!IMPORTANT]
    >  서버 전체 백업을 서버에 있었던 전환 이전 상태로 복원할 수 없습니다.  
  
-   또한,을 읽고 이해 (EULA (최종 사용자 사용권 계약) Windows Server 2012 r 2 표준 용 있는지 확인 합니다. EULA 보려면:  
  
    1.  관리자 권한으로 명령 창 열기  
  
    2.  다음 명령을 실행 합니다.  
  
         **dism /online//set-edition: ServerStandard /geteula:***eula 경로* (여기서 *eula 경로* EULA 파일, 저장 하려는 위치를 나타내는 예: C:\ws8std_eula.rtf). 파일 이름 확장명.rtf 사용 해야 합니다.  
  
    3.  파일을 저장할 위치를 연 다음 열려는 파일을 두 번 클릭 합니다.  
  
## <a name="transition-to--windows-server-2012-r2-standard"></a>Windows Server 2012 r 2 표준 모드로 전환  
 다음 두 단계를 Windows Server 2012 r 2 표준을 전체 Windows Server Essentials에서 전환 하기로 했습니다 한 후:  
  
1.  Windows Server 2012 r 2 표준 및 적절 한 수의 사용자 및/또는 귀하의 환경에 대 한 클라이언트 액세스 라이선스 장치에 대 한 라이선스를 구입 합니다.  
  
     배포자, 정품 판매점에서 또는의 도움으로 Windows Server 2012 r 2 표준에 대 한 라이선스를 구입할 수는 [Microsoft 파트너](https://pinpoint.microsoft.com/SelectCulture.aspx)합니다.  
  
    > [!NOTE]
    >  Windows Server 2012 r 2 표준 처음 구입 하 고 여 다운 그레이드 권한 Windows Server Essentials를 설치 하면 두 가상 인스턴스 중 하나를 수행 하는 경우 추가 물품을 구매할 필요는 없습니다.  
    >   
    >  Windows Server 2012 r 2 표준 볼륨 라이선싱 채널을 통해 구입한 경우 Windows Server 2012 r 2 표준에서 라이선스 서비스 센터 VLSC (볼륨) 용 ISO 이미지 및 제품 키를 다운로드할 수 있습니다.  
    >   
    >  Windows Server Essentials의 용 ISO 이미지와 평가 제품 키를 구매한 경우 Windows Server 2012 r 2 표준에서 다른 채널을 다운로드할 수 있습니다의 [TechNet 평가 센터](https://technet.microsoft.com/evalcenter/jj659306.aspx)합니다. 다음 단계에 설명 된 대로 전환을 수행 완벽 하 게 사용이 허가 되 고 지원 되는 제품 평가 제품을 변환 됩니다.  
  
2.  Windows PowerShell을 관리자 권한으로 열고 다음 명령을 실행 합니다.  
  
     **dism /online//set-edition: ServerStandard /accepteula /productkey:***제품 키* (여기서 *제품 키* 은 Windows Server 2012 r 2 표준 복제품에 대 한 제품 키).  
  
     서버 전환 프로세스를 완료 하려면 다시 시작 합니다.  
  
 전환 된 후 Windows Server Essentials 기능 서버에 남아 있으며 최대 100 사용자 및 200 장치에 대 한 지원 됩니다.  
  
## <a name="see-also"></a>참조 하십시오  
  

-   [Windows Server essentials 서버 데이터 마이그레이션](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Windows Server essentials 서버 데이터 마이그레이션](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

