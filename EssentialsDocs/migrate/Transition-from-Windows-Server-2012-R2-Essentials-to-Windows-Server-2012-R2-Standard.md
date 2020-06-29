---
title: Windows Server Essentials에서 Windows Server 2012 R2 Standard로 전환
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: a14689e3-2310-4229-bd3e-dafc0e739e02
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 3902fa53f59b99475f0ae117fd5ac193afeff8a3
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85470238"
---
# <a name="transition-from-windows-server-essentials-to-windows-server-2012-r2-standard"></a>Windows Server Essentials에서 Windows Server 2012 R2 Standard로 전환

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Windows Server 2016은 클라우드 컴퓨팅으로 쉽게 전환할 수 있도록 하는 새로운 기술을 도입 하면서 현재 워크 로드를 지 원하는 클라우드 지원 운영 체제입니다. Windows Server 2016 콘텐츠가 준비 되는 데 도움이 됩니다.

 Windows Server Essentials는 최대 25 명의 사용자와 50 장치를 지원 합니다. 비즈니스 요구 사항이 제한을 초과 하는 경우 Windows Server Essentials에서 Windows Server 2012 R2 Standard로의 내부 라이선스 전환을 수행 하 여 라이선스를 준수할 수 있습니다.

 Windows Server 2012 R2 Standard로 전환한 후에는 사용자 계정 및 장치 제한이 제거 되지만 Windows Server Essentials에 고유한 기능 (예: 대시보드, 원격 웹 액세스 및 클라이언트 컴퓨터 백업)은 계속 사용할 수 있습니다. 그러나 이러한 기능에는 최대 100개의 사용자 계정과 200대의 디바이스를 지원하는 기술적 제한이 있습니다. 클라이언트 컴퓨터 백업 기능은 최대 75대의 디바이스 백업을 지원합니다.

> [!IMPORTANT]
>   Windows Server 2012 R2 Standard에는 사용자 환경의 각 사용자 또는 장치에 대 한 CAL (클라이언트 액세스 라이선스)이 필요 합니다. 이는 CAL 모델을 사용 하지 않으며 Cal이 제공 되지 않는 Windows Server Essentials와는 다릅니다. Windows Server Essentials에서 Windows Server 2012 R2 Standard로 전환 하는 경우 사용자 환경에 적절 한 수와 유형의 Cal을 구입 해야 합니다 (대부분의 고객이 사용자 Cal을 구입).

## <a name="before-the-transition"></a>전환하기 전에

-   Windows Server Essentials에서 Windows Server 2012 R2 Standard로 전환 하기 전에 서버 데이터를 전체 백업 해야 합니다.

    > [!IMPORTANT]
    >  서버를 전체 백업하지 않으면 전환 이전의 상태로 서버를 복원할 수 없습니다.

-   또한 Windows Server 2012 R2 Standard에 대 한 EULA (최종 사용자 사용권 계약)를 읽고 이해 해야 합니다. EULA를 보려면

    1.  관리자 권한으로 명령 창을 엽니다.

    2.  다음 명령을 실행합니다.

         **dism /online /set-edition:ServerStandard /geteula:** *eula 경로* (여기서 *eula 경로* 는 EULA 파일을 저장 하려는 위치를 나타냅니다. 예: C:\ws8std_eula.rtf). 이때 .rtf를 파일 이름 확장명으로 사용해야 합니다.

    3.  파일을 저장한 위치를 열고 열려는 파일을 두 번 클릭합니다.

## <a name="transition-to--windows-server-2012-r2-standard"></a>Windows Server 2012 R2 Standard로 전환
 Windows Server Essentials에서 Windows Server 2012 R2 Standard로 전환 하기로 결정 한 후에는 다음 두 단계를 완료 합니다.

1. Windows Server 2012 R2 Standard 라이선스 및 사용자 환경에 적합 한 수의 사용자 및/또는 장치 클라이언트 액세스 라이선스를 구매 합니다.

    Windows Server 2012 R2 Standard 라이선스는 소매 판매점, 배포자 또는 [Microsoft 파트너](https://pinpoint.microsoft.com/SelectCulture.aspx)의 도움을 통해 구매할 수 있습니다.

   > [!NOTE]
   >  처음에 Windows Server 2012 R2 Standard를 구매 하 고 Windows Server Essentials로 두 가상 인스턴스 중 하나를 설치 하는 다운 그레이드 권한을 실행 한 경우에는 추가 항목을 구매할 필요가 없습니다.
   >
   >  볼륨 라이선스 채널을 통해 Windows Server 2012 R2 Standard를 구매 하는 경우 볼륨 라이선스 서비스 센터 (VLSC)에서 Windows Server 2012 R2 Standard의 ISO 이미지 및 제품 키를 다운로드할 수 있습니다.
   >
   >  다른 채널에서 Windows Server 2012 R2 Standard를 구매 하는 경우 [TechNet Evaluation Center](https://technet.microsoft.com/evalcenter/jj659306.aspx)에서 Windows server Essentials에 대 한 ISO 이미지 및 평가판 제품 키를 다운로드할 수 있습니다. 다음 단계에 설명된 대로 전환을 수행하면 평가판 제품이 완전히 지원되는 라이선스 제품으로 전환됩니다.

2. 관리자 권한으로 Windows PowerShell을 열고 다음 명령을 실행합니다.

    **dism/online/set-edition: serverstandard/accepteula/productkey:** *제품 키* (여기서 *제품 키* 는 Windows Server 2012 R2 Standard 복사본의 제품 키).

    전환 프로세스를 완료하기 위해 서버가 다시 시작됩니다.

   전환 후에는 Windows Server Essentials 기능이 서버에 그대로 유지 되며 최대 100 명의 사용자 및 200 장치에서 지원 됩니다.

## <a name="additional-references"></a>추가 참조


-   [Windows Server Essentials로 서버 데이터 마이그레이션](Migrate-Server-Data-to-Windows-Server-Essentials.md)

