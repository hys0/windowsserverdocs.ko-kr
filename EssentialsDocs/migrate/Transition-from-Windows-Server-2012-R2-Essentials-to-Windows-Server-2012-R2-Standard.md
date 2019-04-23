---
title: Windows Server Essentials에서 Windows Server 2012 R2 Standard로 전환
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840084"
---
# <a name="transition-from-windows-server-essentials-to-windows-server-2012-r2-standard"></a>Windows Server Essentials에서 Windows Server 2012 R2 Standard로 전환

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Windows Server 2016은 클라우드 컴퓨팅으로 전환할 수 있도록 하는 새로운 기술을 소개 하는 동안 현재 워크 로드를 지 원하는 클라우드 사용 준비가 된 운영 체제입니다. Windows Server 2016 콘텐츠를 준비 하는 데 도움이 됩니다.

 Windows Server Essentials 사용자 25 명과 장치 50 개까지 지원합니다. 한도 초과 해야 하는 비즈니스를 하는 경우 Windows Server 2012 R2 Standard로 라이선스 정책을 계속 준수 하는 라이선스를 바로 전환 Windows Server Essentials에서 수행할 수 있습니다.  
  
 Windows Server 2012 R2 Standard로 전환한 후에 사용자 계정 및 장치 제한이 제거 되지만 기능 (예: 대시보드, 원격 웹 액세스 및 클라이언트 컴퓨터 백업) Windows Server Essentials에 고유한을 계속 사용할 수 있습니다. 그러나 이러한 기능에는 최대 100개의 사용자 계정과 200대의 장치를 지원하는 기술적 제한이 있습니다. 클라이언트 컴퓨터 백업 기능은 최대 75대의 장치 백업을 지원합니다.  
  
> [!IMPORTANT]
>   Windows Server 2012 R2 Standard에 각 사용자 또는 사용자 환경에서 장치에 대 한 클라이언트 액세스 라이선스 (CAL) 필요합니다. 이 CAL 모델을 사용 하지 않으며 cal 제공 되지 않는 Windows Server Essentials에서 다릅니다. Windows Server Essentials에서 Windows Server 2012 R2 Standard로 전환 하는, 하는 경우 적절 한 수 고 (대부분의 고객이 사용자 Cal을 구입 하는 데 사용) 환경의 한 유형의 Cal 구입 해야 합니다.  
  
## <a name="before-the-transition"></a>전환하기 전에  
  
-   전환 되기 전에 Windows Server Essentials에서 Windows Server 2012 R2 Standard, 서버 데이터를 완벽 하 게 백업 해야 합니다.  
  
    > [!IMPORTANT]
    >  서버를 전체 백업하지 않으면 전환 이전의 상태로 서버를 복원할 수 없습니다.  
  
-   또한 읽고 Windows Server 2012 R2 Standard에 대 한 최종 사용자 사용권 계약 (EULA)을 이해 해야 합니다. EULA를 보려면  
  
    1.  관리자 권한으로 명령 창을 엽니다.  
  
    2.  다음 명령을 실행합니다.  
  
         **dism /online-/set-edition: ServerStandard /geteula:** *eula 경로* (여기서 *eula 경로* EULA 파일을 저장 하려는 위치를 나타내는 예를 들어: C:\ws8std_eula.rtf). 이때 .rtf를 파일 이름 확장명으로 사용해야 합니다.  
  
    3.  파일을 저장한 위치를 열고 열려는 파일을 두 번 클릭합니다.  
  
## <a name="transition-to--windows-server-2012-r2-standard"></a>Windows Server 2012 R2 Standard로 전환  
 이러한 두 단계를 Windows Server 2012 R2 Standard, 전체 Windows Server Essentials에서 전환 하기로 결정 했으면 후:  
  
1.  Windows Server 2012 R2 Standard 및 적절 한 개수의 사용자 및/또는 사용자 환경에 대 한 클라이언트 액세스 라이선스에 대 한 라이선스를 구입 합니다.  
  
     소매점, 배포자에서에서 또는 사용 하 여 Windows Server 2012 R2 Standard에 대 한 라이선스를 구입할 수 있습니다는 [Microsoft 파트너](https://pinpoint.microsoft.com/SelectCulture.aspx)합니다.  
  
    > [!NOTE]
    >  처음에 Windows Server 2012 R2 Standard를 구입 하 고 Windows Server Essentials를 설치 하는 두 가상 인스턴스 중 하나를 다운 그레이드 권한을 아무것도 구입할 필요가 없습니다.  
    >   
    >  볼륨 라이선스 채널을 통해 Windows Server 2012 R2 Standard을 구매 하는 경우 Windows Server 2012 R2 Standard에서 볼륨 라이선스 서비스 센터 (VLSC)에 대 한 ISO 이미지 및 제품 키를 다운로드할 수 있습니다.  
    >   
    >  Windows Server Essentials에 대 한 ISO 이미지 및 평가판 제품 키를 다른 채널에서 Windows Server 2012 R2 Standard을 구매 하는 경우 다운로드할 수 있습니다 합니다 [TechNet Evaluation Center](https://technet.microsoft.com/evalcenter/jj659306.aspx)합니다. 다음 단계에 설명된 대로 전환을 수행하면 평가판 제품이 완전히 지원되는 라이선스 제품으로 전환됩니다.  
  
2.  관리자 권한으로 Windows PowerShell을 열고 다음 명령을 실행합니다.  
  
     **dism /online /set-edition:ServerStandard /accepteula /productkey:** *제품 키* (여기서 *제품 키* 은 Windows Server 2012 R2 Standard의 정품 제품 키).  
  
     전환 프로세스를 완료하기 위해 서버가 다시 시작됩니다.  
  
 전환 후 Windows Server Essentials 서버에 남아 기능과 최대 100 명의 사용자와 200 대의 장치에 대해 지원 됩니다.  
  
## <a name="see-also"></a>참조  
  

-   [Windows Server Essentials로 서버 데이터 마이그레이션](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Windows Server Essentials로 서버 데이터 마이그레이션](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

