---
title: WSUS를 사용 하지 않는 월간 델타 업데이트 ISV 지원
description: WSUS (Windows Server Update Service) 토픽-ISV (독립 소프트웨어 공급 업체)에서 WSUS Express 업데이트 배달 대신 매월 델타 업데이트를 일시적으로 사용 하 여 패키지 크기를 줄일 수 있는 방법
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: get-started article
author: sakitong
ms.author: coreyp
manager: dougkim
ms.date: 10/16/2017
ms.openlocfilehash: 9077cb87d1d0f6d59ad037c93f5608d3b698feaa
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868716"
---
# <a name="monthly-delta-update-isv-support-without-wsus"></a>WSUS를 사용 하지 않는 월간 델타 업데이트 ISV 지원

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10

모든 패키지에는 일관성과 단순성을 보장 하기 위해 이전에 릴리스된 모든 수정 프로그램이 포함 되어 있으므로 Windows 10 업데이트 다운로드는 클 수 있습니다.  

버전 7부터 Windows는 [Express](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx#Anchor_2)라는 기능을 사용 하 여 Windows 업데이트 다운로드 크기를 줄일 수 있으며, 소비자 장치는 기본적으로이 기능을 지원 하지만, windows 10 enterprise 장치에는 WINDOWS SERVER UPDATE SERVICES (WSUS)를 사용 해야 합니다. Express의 장점입니다. WSUS를 사용할 수 있는 경우 [Express 업데이트 배달 ISV 지원](express-update-delivery-ISV-support.md)을 참조 하세요. 빠른 업데이트 배달을 사용 하도록 설정 하는 것이 좋습니다. 

현재 WSUS가 설치 되어 있지 않지만 중간에 더 작은 업데이트 패키지 크기가 필요한 경우 월간 델타 업데이트를 사용할 수 있습니다. 델타 업데이트를 사용 하면 패키지 크기를 크게 줄일 수 있지만 WSUS Express 업데이트 배달 만큼 크게 줄일 수는 없습니다. 가능 하면 패키지 크기를 최대한 줄일 수 있는 경우 WSUS Express 업데이트를 배포 하는 것이 좋습니다. 다음은 Windows 10 버전 1607에 대 한 델타, 누적 및 빠른 다운로드 크기를 비교 하는 차트입니다.

![다운로드 크기 비교](../../media/express-update-delivery-isv-support/delta-1.png)

## <a name="what-is-monthly-delta-update"></a>월간 델타 업데이트 란?

매월 보안 업데이트에는 다음과 같은 두 가지 변형이 있습니다. 델타 및 누적.

매월 델타 업데이트는 새로운 기능과 WSUS를 사용 하 여 업데이트 패키지 크기를 줄이는 데 도움이 되지 않는 Isv를 위한 중간 솔루션입니다.

>[!IMPORTANT]
>**델타 업데이트는 Windows 10, 버전 1607 (기념일 업데이트), 버전 1703 (크리에이터 업데이트) 및 버전 1709 (is 크리에이터 업데이트) 서비스에 사용할 수 있습니다.** 버전 1709 이후의 릴리스에서는 증분 업데이트를 계속 활용 하기 위해 [빠른 업데이트 배달](express-update-delivery-ISV-support.md) 기능을 지 원하는 배포 인프라를 구현 해야 합니다.

월간 델타 업데이트를 사용 하 여 패키지는 한 달의 업데이트만 포함 합니다. 월별 누적은 업데이트 릴리스 까지의 모든 업데이트를 포함 하 여 매월 증가 하는 파일을 만듭니다. 델타 및 월별 업데이트는 매월 두 번째 화요일에 릴리스됩니다. "화요일 업데이트" 라고도 합니다. 다음 표에서는 델타 및 누적 업데이트를 비교 합니다.

|                    | 월간 **델타** 업데이트                                                                                                                                                                                                       | 월별 **누적** 업데이트                                                                                                                                                                                             |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **범위**          | **해당 월에 대 한 새로운 수정 내용만** 포함 된 단일 업데이트                                                                                                                                                                           | 해당 월 및 모든 이전 월에 대 한 모든 새 수정 사항이 포함 된 단일 업데이트                                                                                                                                                   |
| **응용 프로그램**    | 이전 달의 업데이트를 적용 한 경우에만 적용할 수 있습니다 (누적 또는 델타).                                                                                                                                           | 언제 든 지 적용할 수 있습니다.                                                                                                                                                                                                |
| **못함**       | 다른 도구나 프로세스와 함께 사용 하기 위해 다운로드할 수 있는 **Windows 업데이트 카탈로그에만 게시** 됩니다. Windows 업데이트에 연결 된 Pc에는 제공 되지 않음                                                         | Windows 업데이트 (모든 소비자 Pc가 설치 되는 경우), WSUS 및 Windows 업데이트 카탈로그에 게시 됨                                                                                                                |

델타와 누적은 동일한 분류 및 릴리스와 함께 동일한 KB 번호를 사용 합니다. 업데이트는 카탈로그의 업데이트 제목 또는 msu 이름으로 구분할 수 있습니다.

-  2017-02 *\*\** x64 기반 시스템용 Windows 10 버전 1607에 대 한 델타 업데이트 (KB1234567)
-  2017-02 *\*\** x86 기반 시스템용 Windows 10 버전 1607 누적 업데이트 (KB1234567) (영문)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      

### <a name="when-to-use-monthly-delta-update"></a>월간 델타 업데이트를 사용 하는 경우

클라이언트 장치에 대 한 업데이트 크기가 중요 한 경우 이전 월 업데이트를 포함 하는 장치에서 델타 업데이트를 사용 하는 것이 좋으며,이 경우에는 지연 된 장치에 대 한 누적 업데이트를 사용 하는 것이 좋습니다. 이러한 방식으로 모든 장치는 최신 상태로 만들기 위해 단일 업데이트만 필요 합니다. 이를 위해서는 전반적인 업데이트 관리 프로세스를 약간 조정 해야 합니다 .이 경우에는 조직에서 장치를 최신 상태로 유지 하는 방법에 따라 다른 업데이트를 배포 해야 합니다.

![다운로드 크기 비교](../../media/express-update-delivery-isv-support/delta-2.png)

### <a name="prevent-deployment-of-delta-and-cumulative-updates-in-the-same-month"></a>같은 달에 델타 및 누적 업데이트 배포 방지

델타 업데이트와 누적 업데이트를 동시에 사용할 수 있으므로 동일한 달에 두 업데이트를 모두 배포 하는 경우 발생 하는 상황을 이해 하는 것이 중요 합니다.

동일한 버전의 델타 및 누적 업데이트를 승인 하 고 배포 하는 경우에는 둘 다 PC로 다운로드 되기 때문에 추가 네트워크 트래픽만 생성할 수 있지만, 다시 시작한 후에는 컴퓨터를 Windows로 다시 부팅할 수 없습니다.

델타 및 누적 업데이트가 실수로 설치 되 고 컴퓨터가 더 이상 부팅 되지 않는 경우 다음 단계를 수행 하 여 복구할 수 있습니다.

1. WinRE 명령 프롬프트로 부팅
2. 보류 중 상태인 패키지 나열:

    `x:\windows\system32\dism.exe /image:<drive letter for windows directory> /Get-Packages >> <path to text file>`
 
    > **예**:` x:\windows\system32\dism.exe /image:c:\ /Get-Packages >> c:\temp\packages.txt`
 
3. **수신 패키지**를 파이프 한 텍스트 파일을 엽니다. 설치 보류 중인 패치가 표시 되는 경우 각 패키지 이름에 대해 **제거 패키지** 를 실행 합니다.
 
   `dism.exe /image:<drive letter for windows directory> /remove-package /packagename:<package name>`
 
    > **예**:`x:\windows\system32\dism.exe /image:c:\ /remove-package /packagename:Package_for_KB4014329~31bf3856ad364e35~amd64~~10.0.1.0`
 
    >[!NOTE]
    >제거 보류 중인 패치는 제거 하지 마십시오.

>[!IMPORTANT]
>**델타 업데이트는 Windows 10, 버전 1607 (기념일 업데이트), 버전 1703 (크리에이터 업데이트) 및 버전 1709 (is 크리에이터 업데이트) 서비스에 사용할 수 있습니다.** 버전 1709 이후의 릴리스에서는 증분 업데이트를 계속 활용 하기 위해 [빠른 업데이트 배달](express-update-delivery-ISV-support.md) 기능을 지 원하는 배포 인프라를 구현 해야 합니다.
