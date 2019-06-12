---
title: 월별 델타 업데이트 WSUS 없이 ISV 지원
description: WSUS Windows Server Update Service () 항목-하는 방법을 소프트웨어 공급 업체 (ISV) 일시적으로 사용할 수 월간 델타 업데이트 WSUS Express 업데이트 배달 하는 대신 패키지 크기를 줄이기 위해
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
ms.openlocfilehash: 272d3865bbe1a9853f5349c5e878155351525ef0
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439944"
---
# <a name="monthly-delta-update-isv-support-without-wsus"></a>월별 델타 업데이트 WSUS 없이 ISV 지원

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10

Windows 10 업데이트 다운로드는 모든 패키지에는 일관성과 간결성을 위해 이전에 릴리스된 모든 수정 내용이 포함 되어 있으므로 클 수 있습니다.  

버전 7, Windows 라는 기능을 사용 하 여 Windows 업데이트 다운로드의 크기를 줄일 수 있게 되었습니다 [Express](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx#Anchor_2), 및 Windows 10 enterprise 장치 필요 Windows Server Update 소비자 장치를 지원 하지만 기본적으로, Services (WSUS) Express를 활용할 수 있습니다. WSUS를 사용할 수 있는 경우 참조 [Express 업데이트 배달 ISV 지원](express-update-delivery-ISV-support.md)합니다. 사용 하 여 Express 업데이트를 제공 하도록 하는 것이 좋습니다. 

WSUS가 설치 되어, 현재 없는 그동안에서 패키지 크기를 더 작은 업데이트 해야 하지만 경우에 월별 델타 업데이트를 사용할 수 있습니다. 델타 업데이트 하지만 업데이트 배달 WSUS Express와 마찬가지로 심각 하지 않은 패키지 크기를 크게 줄입니다. 가능한 가장 큰 패키지 크기 감소에 대 한 WSUS 빠른 업데이트를 배포 하는 것이 좋습니다. 다음은 Windows 10 버전 1607에 대 한 델타, 누적 및 Express 다운로드 크기를 비교 하는 차트입니다.

![다운로드 크기 비교](../../media/express-update-delivery-isv-support/delta-1.png)

## <a name="what-is-monthly-delta-update"></a>월별 델타 업데이트는 무엇입니까?

월간 보안 업데이트의 두 가지 변형이 있습니다. 델타 및 누적 합니다.

월별 델타 업데이트 새로운 및 WSUS를 줄이는 데 사용할 수 있는 권한이 없는 Isv 위한 중간 솔루션 패키지 크기를 업데이트 합니다.

>[!IMPORTANT]
>**델타 업데이트는 Windows 10, 버전 1607 (1 주년 업데이트), 버전 1703 (크리에이터 스 업데이트) 및 버전 1709 (Fall Creators Update) 서비스에 대해 사용할 수 있습니다.** 버전 1709 이후 릴리스를 지 원하는 배포 인프라를 구현 해야 합니다 [Express 업데이트 배달](express-update-delivery-ISV-support.md) 증분 업데이트를 활용 하 고 계속 합니다.

패키지 델타 월별 업데이트를 사용 하 여 한 달의 업데이트 포함 됩니다. 월별 누적 매월 증가 하는 큰 파일에서 결과 해당 업데이트 릴리스까지 모든 업데이트를 포함 합니다. 각 월 라고도 "업데이트 화요일."의 두 번째 화요일에 델타 및 월별 업데이트를 모두 해제 됩니다. 다음 표에서 델타 및 누적 업데이트를 비교합니다.

|                    | 월별 **델타** 업데이트                                                                                                                                                                                                       | 월별 **누적** 업데이트                                                                                                                                                                                             |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **범위**          | 사용 하 여 단일 업데이트 **해당 월에 대 한 새 수정**                                                                                                                                                                           | 해당 월 및 모든 이전 달에 대 한 모든 새 수정 프로그램을 사용 하 여 단일 업데이트                                                                                                                                                   |
| **응용 프로그램**    | 이전 달의 업데이트 적용 (누적 또는 델타) 경우에 적용할 수                                                                                                                                           | 언제 든 지 적용할 수 있습니다.                                                                                                                                                                                                |
| **배달**       | **Windows 업데이트 카탈로그에만 게시** 다른 도구 또는 프로세스를 사용 하 여 사용 하기 위해 다운로드할 수 있습니다. Windows 업데이트에 연결 된 Pc에 제공 되지 않습니다.                                                         | Windows 업데이트 (모든 소비자 Pc를 설치할 것), WSUS 및 Windows 업데이트 카탈로그에 게시                                                                                                                |

델타 및 누적 같은 분류를 사용 하 여 동일한 KB 수를 포함 하 고 동시 릴리스 합니다. 업데이트는 카탈로그에서 업데이트 제목 또는 msu의 이름으로 구분할 수 있습니다.

- 2017-02 *\***델타 업데이트**\**  x64 기반 시스템 (KB1234567)에 대 한 Windows 10 버전 1607에 대 한
- 2017-02 *\***업데이트할**\**  x86 기반 시스템 (KB1234567)에 대 한 Windows 10 버전 1607에 대 한                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      

### <a name="when-to-use-monthly-delta-update"></a>월별 델타 업데이트를 사용 하는 경우

클라이언트 장치에 업데이트 크기는 중요 한 경우에 이전 월의 업데이트 및 누적 업데이트는 늦는 지 장치에 있는 장치에서 델타 업데이트를 사용 하는 것이 좋습니다. 이 이렇게 하면 모든 장치에 단일 업데이트를 최신 상태로 필요 합니다. 조직에서 장치는 얼마나 최신 상태 인지에 따라 다른 업데이트를 배포 해야 하는 대로 전체 업데이트 관리 프로세스에서 약간의 조정이 필요 합니다.

![다운로드 크기 비교](../../media/express-update-delivery-isv-support/delta-2.png)

### <a name="prevent-deployment-of-delta-and-cumulative-updates-in-the-same-month"></a>같은 달의 델타 및 누적 업데이트의 배포가 진행 되지 않습니다

델타 업데이트 및 누적 업데이트를 사용할 수 있는 동시 이므로 어떻게 되는지 이해 하는 것이 중요 한 달에 두 업데이트를 배포 하는 경우.

승인 하 고 동일한 버전의 델타 및 누적 업데이트를 배포 하면 생성 하지 않습니다만 추가 네트워크 트래픽으로 다시 시작한 후에 Windows 컴퓨터를 다시 부팅 하는 일을 할 수 있지만 둘 다에 PC에 다운로드 됩니다.

Delta 및 누적 업데이트는 실수로 설치 하 고 컴퓨터가 더 이상 부팅을 실행 하는 경우 다음 단계를 사용 하 여 복구할 수 없습니다.

1. WinRE 명령 프롬프트에 부팅
2. 보류 중 상태에서 패키지를 나열 합니다.

    `x:\windows\system32\dism.exe /image:<drive letter for windows directory> /Get-Packages >> <path to text file>`
 
    > **예제**: ` x:\windows\system32\dism.exe /image:c:\ /Get-Packages >> c:\temp\packages.txt`
 
3. 파이프는 텍스트 파일을 엽니다 **get 패키지**합니다. 패치 보류 중인 설치를 표시 하는 경우 실행할 **제거 패키지** 각 패키지 이름에 대 한 합니다.
 
   `dism.exe /image:<drive letter for windows directory> /remove-package /packagename:<package name>`
 
    > **예제**: `x:\windows\system32\dism.exe /image:c:\ /remove-package /packagename:Package_for_KB4014329~31bf3856ad364e35~amd64~~10.0.1.0`
 
    >[!NOTE]
    >제거 하지 마십시오 패치 보류 제거 합니다.

>[!IMPORTANT]
>**델타 업데이트는 Windows 10, 버전 1607 (1 주년 업데이트), 버전 1703 (크리에이터 스 업데이트) 및 버전 1709 (Fall Creators Update) 서비스에 대해 사용할 수 있습니다.** 버전 1709 이후 릴리스를 지 원하는 배포 인프라를 구현 해야 합니다 [Express 업데이트 배달](express-update-delivery-ISV-support.md) 증분 업데이트를 활용 하 고 계속 합니다.
