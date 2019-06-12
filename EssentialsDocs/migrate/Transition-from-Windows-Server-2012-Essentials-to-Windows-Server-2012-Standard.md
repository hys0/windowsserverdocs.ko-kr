---
title: Windows Server Essentials에서 Windows Server 2012 Standard로 전환
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
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
ms.openlocfilehash: 445472822de09263b84821e552c931ca19f14b2b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66432537"
---
# <a name="transition-from-windows-server-essentials-to-windows-server-2012-standard"></a>Windows Server Essentials에서 Windows Server 2012 Standard로 전환

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 Windows Server® 2012 Essentials 사용자 25 명과 장치 50 개까지 지원 합니다. 한도 초과 해야 하는 비즈니스를 하는 경우에 Windows Server 2012 Standard 라이선스 정책을 계속 준수 하는 라이선스를 바로 전환 Windows Server Essentials에서 수행할 수 있습니다.  
  
## <a name="how-the-transition-affects-user-and-device-limits"></a>전환이 사용자 및 장치 제한에 미치는 영향  
 Windows Server 2012 Standard 전환한 후 사용자 계정 및 장치 제한이 제거 되지만 기능 (예: 대시보드, 원격 웹 액세스 및 클라이언트 컴퓨터 백업), Windows Server Essentials에 고유한을 계속 사용할 수 있습니다. 그러나 이러한 기능에는 최대 75개의 사용자 계정과 75대의 장치를 지원하는 기술적 제한이 있습니다. 75 개가 넘는 사용자 계정 또는 장치를 추가 하는 일을 해야 하는 경우에 Windows Server Essentials 기능 해제 하 고 사용자 계정 및 장치를 관리 하려면 Windows Server 2012 Standard 네이티브 도구를 사용 해야 합니다.  
  
> [!IMPORTANT]
>   Windows Server 2012 Standard 각 사용자 또는 사용자 환경에서 장치에 대 한 클라이언트 액세스 라이선스 (CAL) 필요합니다. 이 CAL 모델을 사용 하지 않으며 cal 제공 되지 않는 Windows Server Essentials에서 다릅니다.  Windows Server Essentials에서 Windows Server 2012 Standard 전환 하는, 하는 경우 적절 한 수 고 (대부분의 고객이 사용자 Cal을 구입 하는 데 사용) 환경의 한 유형의 Cal 구입 해야 합니다.  
  
## <a name="before-the-transition"></a>전환하기 전에  
  
-   전환 되기 전에 Windows Server Essentials에서 Windows Server 2012 Standard, 서버 데이터를 완벽 하 게 백업 해야 합니다.  
  
    > [!IMPORTANT]
    >  서버를 전체 백업하지 않으면 전환 이전의 상태로 서버를 복원할 수 없습니다.  
  
-   또한 읽고 Windows Server 2012 Standard 대 한 최종 사용자 사용권 계약 (EULA)을 이해 해야 합니다. EULA를 보려면  
  
    1.  관리자 권한으로 명령 창을 엽니다.  
  
    2.  다음 명령을 실행합니다.  
  
         **dism /online /set-edition:ServerStandard /geteula: eula path**  
  
         여기서 **EULA 경로**는 EULA 파일을 저장할 위치를 나타냅니다(예: C:\ws8std_eula.rtf).  이때 .rtf를 파일 이름 확장명으로 사용해야 합니다.  
  
    3.  파일을 저장한 위치를 열고 열려는 파일을 두 번 클릭합니다.  
  
## <a name="transition-to--windows-server-2012-standard"></a>Windows Server 2012 Standard 전환  
 이러한 두 단계를 Windows Server 2012 Standard, 전체 Windows Server Essentials에서 전환 하기로 결정 했으면 후:  
  
1. Windows Server 2012 Standard 및 적절 한 개수의 사용자 환경에 대 한 클라이언트 액세스 라이선스 사용자 및/또는 장치에 대 한 라이선스를 구입 합니다.  
  
    소매점, 배포자에서에서 또는 사용 하 여 Windows Server 2012 Standard 대 한 라이선스를 구입할 수 있습니다는 [Microsoft 파트너](https://pinpoint.microsoft.com/SelectCulture.aspx)합니다.  
  
   > [!NOTE]
   >  처음에 Windows Server 2012 Standard 구입 하 고 Windows Server Essentials를 설치 하는 두 가상 인스턴스 중 하나를 다운 그레이드 권한을 아무것도 구입할 필요가 없습니다.  
   >   
   >  볼륨 라이선스 채널을 통해 Windows Server 2012 Standard 구매 하는 경우 Windows Server 2012 Standard에서 볼륨 라이선스 서비스 센터 (VLSC)에 대 한 ISO 이미지 및 제품 키를 다운로드할 수 있습니다.  
   >   
   >  그 외 다른 채널에서 Windows Server 2012 Standard 구입 하는 경우 다운로드할 수는 ISO 이미지 및 평가판 제품 키에서 Windows Server Essentials에 대 한 합니다 [TechNet Evaluation Center](https://technet.microsoft.com/evalcenter/jj659306.aspx)합니다. 다음 단계에 설명된 대로 전환을 수행하면 평가판 제품이 완전히 지원되는 라이선스 제품으로 전환됩니다.  
  
2. 관리자 권한으로 Windows PowerShell을 열고 다음 명령을 실행합니다.  
  
    **dism /online /set-edition:ServerStandard /accepteula /productkey:** *제품 키*  
  
    여기서 *제품 키* 은 Windows Server 2012 Standard 정품 제품 키입니다.  
  
    전환 프로세스를 완료하기 위해 서버가 다시 시작됩니다.  
  
   전환 후 Windows Server Essentials 서버에 남아 기능과 최대 75 명의 사용자와 75 대의 장치에 대해 지원 됩니다. 이러한 제한 중 하나를 초과 하는 경우에 사용자 계정 및 장치를 관리 하려면 Windows Server 2012 Standard 네이티브 도구를 사용 해야 합니다.  
  
   또한 Windows Server 2012 Standard 전환한 후 Windows Server Essentials의 미디어 기능을 사용할 수 없게 됩니다. 여기에는 원격 웹 액세스의 미디어 기능과 대시보드의 미디어 설정이 포함됩니다.  
  
## <a name="turn-off--windows-server-essentials-features"></a>Windows Server Essentials 기능 해제  
 서버를 관리 하는 Windows Server Essentials 대시보드를 또는 다른 부가 기능이 더 이상 필요한 경우에 기능을 해제 하 고 서버에서 제거할 수 없습니다.  
  
 합니다 **Windows Server Essentials 기능 해제 마법사** 기능을 제거 하는 데 도움이 됩니다. 또한 Windows Server Essentials 서버 소프트웨어에 의해 생성 된 파일 서버를 정리 합니다.  이러한 정리 작업에는 즉시 수행되는 작업과 서버가 다시 시작된 후에 시작되는 작업이 있습니다.  
  
 합니다 **Windows Server Essentials 기능 해제 마법사** 마법사를 완료 하려면 먼저 모든 추가 기능을 수동으로 제거 하는 필요 합니다. 설치된 추가 기능 목록을 보려면 대시보드에서 응용 프로그램 페이지를 엽니다. 마법사에서 설치된 추가 기능을 검색한 경우 경고 메시지와 함께 추가 기능을 제거할지 묻는 메시지가 표시됩니다.  
  
 합니다 **Windows Server Essentials 기능 해제 마법사** Windows Server Essentials 기능 해제 한 후 컴퓨터 클라이언트에 대 한 백업 파일을 유지할지 여부를 선택할 수 있습니다.  
  
 두 가지 방법으로 실행 하는 **Windows Server Essentials 기능 해제 마법사** 대시보드에서:  
  
#### <a name="from-the-alert"></a>경고에서  
  
1.  대시보드에서 경고 뷰어를 엽니다.  
  
2.  구성 목록에서 전환 후 Windows Server Essentials 기능 해제에 대 한 정보를 보고 하는 경고를 선택 합니다.  
  
3.  경고를 클릭 **Windows Server Essentials 기능 해제**합니다.  
  
#### <a name="from-the-get-help-and-support-pane"></a>도움말 및 지원 창에서  
  
1. 홈 페이지에서 도움말 및 지원을 클릭합니다.  
  
2. 클릭 **Windows Server Essentials 기능 해제 마법사**합니다.  
  
   수행한 일부 작업이 불가능 합니다 **Windows Server Essentials 기능 해제 마법사** 성공적으로 완료 되지 것입니다. 이로 인해 대시보드가 실행되지 않을 수 있습니다. 이 경우 다음 파일을 실행하여 마법사를 수동으로 시작할 수 있습니다.  
  
   **%systemdrive%\Program Files\Windows Server\Bin\TurnOffFeaturesWizard.exe**  
  
## <a name="see-also"></a>참조  
  

-   [Windows Server 2012 R2 Standard로 전환](Transition-from-Windows-Server-2012-R2-Essentials-to-Windows-Server-2012-R2-Standard.md)  
  
-   [Windows Server Essentials로 서버 데이터 마이그레이션](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Windows Server 2012 R2 Standard로 전환](../migrate/Transition-from-Windows-Server-2012-R2-Essentials-to-Windows-Server-2012-R2-Standard.md)  
  
-   [Windows Server Essentials로 서버 데이터 마이그레이션](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

