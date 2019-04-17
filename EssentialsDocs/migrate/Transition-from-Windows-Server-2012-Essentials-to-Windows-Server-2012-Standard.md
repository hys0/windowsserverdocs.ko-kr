---
title: "Windows Server 2012 표준 Windows Server Essentials에서 전환"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 51bcf124-c215-4e9d-9fa8-a90fa2c2fa22
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d2005b72adede72b718fa5b49b93435f5fbac1bd
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="transition-from-windows-server-essentials-to-windows-server-2012-standard"></a>Windows Server 2012 표준 Windows Server Essentials에서 전환

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

 ® 2012 Windows Server Essentials 25 명의 사용자와 장치 50까지 지원 합니다. 비즈니스 요구 제한을 초과 하는 경우 Windows Server 2012 표준 라이선스 호환 되도록 하는 현재 위치에서 라이선스 전환 Windows Server Essentials에서 수행할 수 있습니다.  
  
## <a name="how-the-transition-affects-user-and-device-limits"></a>전환을 사용자와 디바이스에 영향 제한  
 Windows Server 2012 표준 모드로 전환 하면 후 사용자 계정 및 디바이스 제한, 제거 되지만 (예: 대시보드, 원격 Web Access 및 클라이언트 컴퓨터 백업) Windows Server Essentials에 고유 하 게 포함 된 기능에도 계속 사용할 수 있습니다. 하지만 이러한 기능에 대 한 기술적 제한 사항을 75 사용자 계정 및 75 장치의 최대를 지원합니다. 75 개 이상의 사용자 계정이 나 디바이스를 추가 해야 하는 경우에 Windows Server Essentials 기능을 해제 하 고 기본 Windows Server 2012 표준 도구를 사용 하 여 사용자 계정 및 디바이스를 관리 하 해야 합니다.  
  
> [!IMPORTANT]
>   Windows Server 2012 표준 각 사용자 또는 사용자 환경에서 디바이스에 대 한 클라이언트 Access 라이선스 (CAL)이 필요 합니다. 이 Windows Server Essentials CAL 모델을 사용 하지 않는 모든 Cal와 함께 제공 되지 않는 이며 다릅니다.  Windows Server Essentials에서 Windows Server 2012 표준로 전환 때 (대부분의 고객 사용자 Cal 구매) 귀하의 환경에 대 한 Cal의 종류와 적절 한 수를 구입 해야 합니다.  
  
## <a name="before-the-transition"></a>전환 하기 전에  
  
-   Windows Server Essentials에서 Windows Server 2012 표준로 전환, 하기 전에 서버 데이터를 완전히 백업 해야 합니다.  
  
    > [!IMPORTANT]
    >  서버 전체 백업을 서버에 있었던 전환 이전 상태로 복원할 수 없습니다.  
  
-   또한,을 읽고 이해 (EULA (최종 사용자 사용권 계약) Windows Server 2012 표준 용 있는지 확인 합니다. EULA 보려면:  
  
    1.  관리자 권한으로 명령 창 열기  
  
    2.  다음 명령을 실행 합니다.  
  
         **Dism /online//set-edition: ServerStandard /geteula: eula 경로**  
  
         여기서 **eula 경로** EULA 파일을 저장 하려는 위치를 나타냅니다. 예를 들어, C:\ws8std_eula.rtf 합니다.  파일 이름 확장명.rtf 사용 해야 합니다.  
  
    3.  파일을 저장할 위치를 연 다음 열려는 파일을 두 번 클릭 합니다.  
  
## <a name="transition-to--windows-server-2012-standard"></a>Windows Server 2012 표준 모드로 전환  
 다음 두 단계 Windows Server 2012 표준을 전체 Windows Server Essentials에서 전환 하기로 했습니다 한 후:  
  
1.  Windows Server 2012 표준 및 있는 적절 한 수의 사용자 환경에 대 한 클라이언트 액세스 라이선스 사용자 및/또는 디바이스에 대 한 라이선스를 구입 합니다.  
  
     배포자, 정품 판매점에서 또는의 도움으로 Windows Server 2012 표준에 대 한 라이선스를 구입할 수는 [Microsoft 파트너](https://pinpoint.microsoft.com/SelectCulture.aspx)합니다.  
  
    > [!NOTE]
    >  Windows Server 2012 표준 처음 구입 하 고 여 다운 그레이드 권한 Windows Server Essentials를 설치 하면 두 가상 인스턴스 중 하나를 수행 하는 경우 추가 물품을 구매할 필요는 없습니다.  
    >   
    >  Windows Server 2012 표준 볼륨 라이선싱 채널을 통해 구입한 경우 Windows Server 2012 표준에서 라이선스 서비스 센터 VLSC (볼륨)에 대 한 ISO 이미지 및 제품 키를 다운로드할 수 있습니다.  
    >   
    >  다른 모든 채널의 Windows Server 2012 표준를 구매한 경우 용 다운로드할 수 ISO 이미지 및 필요한 평가 제품 키가에서 Windows Server Essentials의 [TechNet 평가 센터](https://technet.microsoft.com/evalcenter/jj659306.aspx)합니다. 다음 단계에 설명 된 대로 전환을 수행 완벽 하 게 사용이 허가 되 고 지원 되는 제품 평가 제품을 변환 됩니다.  
  
2.  Windows PowerShell을 관리자 권한으로를 연 다음 명령을 실행 합니다.  
  
     **dism /online//set-edition: ServerStandard /accepteula /productkey:***제품 키*  
  
     여기서 *제품 키* 은 Windows Server 2012 표준 복제품에 대 한 제품 키.  
  
     서버 전환 프로세스를 완료 하려면 다시 시작 합니다.  
  
 전환 된 후 Windows Server Essentials 기능 서버에 남아 있으며까지 75 사용자와 75 장치에 대 한 지원 됩니다. 이러한 제한의 초과 하는 경우 기본 Windows Server 2012 표준 도구를 사용 하 여 사용자 계정 및 디바이스를 관리 하 해야 합니다.  
  
 또한 Windows Server 2012 표준 모드로 전환 하면 후 Windows Server Essentials의 미디어 기능 사용할 수 없게 됩니다. 미디어 기능 원격 Web Access 및 대시보드에서 미디어 설정이 포함 됩니다.  
  
## <a name="turn-off--windows-server-essentials-features"></a>Windows Server Essentials 기능을 끄려면  
 서버 관리 하 고 Windows Server Essentials 대시보드 또는 기타 부가 가치 이며 기능을 더 이상 해야 하는 경우에 기능을 해제 하 고 서버에서 제거 수 없습니다.  
  
 **Windows Server Essentials 기능 마법사 끄기** 기능을 제거 하는 데 도움이 됩니다. 또한 Windows Server Essentials 서버 소프트웨어에 의해 만든 파일 서버를 청소 합니다.  서버를 다시 시작한 후 다른 시작 되는 동안 일부 청소 작업 즉시 수행 됩니다.  
  
 **Windows Server Essentials 기능 마법사 끄기** 마법사를 완료 하려면 먼저 모든 추가 기능을 수동으로 제거 하는 해야 합니다. 설치 된 추가 기능 목록을 보고 이러한, 대시보드에 응용 프로그램 페이지를 엽니다. 마법사가 설치 된 추가 기능을 감지 하 고 제거 하 라는 메시지가 표시 되는 경우 알립니다.  
  
 **Windows Server Essentials 기능 마법사 끄기** Windows Server Essentials 기능을 해제 한 후 컴퓨터 클라이언트에 대 한 백업 파일을 유지할지 여부를 선택할 수 있습니다.  
  
 두 가지 방법으로 실행 하 고 **Windows Server Essentials 기능 마법사 끄기** 대시보드에서:  
  
#### <a name="from-the-alert"></a>알림을에서  
  
1.  대시보드에서 경고 뷰어를 엽니다.  
  
2.  구성 목록에서 전환 후 Windows Server Essentials 기능을 해제 하면에 대 한 정보를 보고 경고를 선택 합니다.  
  
3.  알림을 클릭 **Windows Server Essentials 기능 끄기**합니다.  
  
#### <a name="from-the-get-help-and-support-pane"></a>도움말 및 지원 창에서  
  
1.  홈페이지, 클릭 도움말 및 지원 합니다.  
  
2.  클릭 **Windows Server Essentials 기능 마법사 끄기**합니다.  
  
 몇 가지 작업 수행한 수는 **Windows Server Essentials 기능 마법사 끄기** 성공적으로 완료 되지 것입니다. 경우에 따라이 실행에서 대시보드를 방지할 수 있습니다. 이 문제가 발생 하는 경우 해당 파일을 실행 하 여 수동으로 마법사를 시작할 수 있습니다.  
  
 **%systemdrive%\Program Files\Windows Server\Bin\TurnOffFeaturesWizard.exe**  
  
## <a name="see-also"></a>참조 하십시오  
  

-   [Windows Server 2012 r 2 표준 모드로 전환](Transition-from-Windows-Server-2012-R2-Essentials-to-Windows-Server-2012-R2-Standard.md)  
  
-   [Windows Server essentials 서버 데이터 마이그레이션](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Windows Server 2012 r 2 표준 모드로 전환](../migrate/Transition-from-Windows-Server-2012-R2-Essentials-to-Windows-Server-2012-R2-Standard.md)  
  
-   [Windows Server essentials 서버 데이터 마이그레이션](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

