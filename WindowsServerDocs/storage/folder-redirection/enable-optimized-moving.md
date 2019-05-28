---
title: 리디렉션된 폴더의 최적화 된 이동 사용
description: 리디렉션된 폴더의 최적화 된 이동 새 파일 공유를 수행 하는 방법.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7bdf30a4f721568add4e7902245da2a803b72db1
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65475864"
---
# <a name="enable-optimized-moves-of-redirected-folders"></a>리디렉션된 폴더의 최적화 된 이동 사용

>적용 대상: Windows 10, Windows 8, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server (반기 채널)

이 항목에서는 리디렉션된 폴더 (폴더 리디렉션) 새 파일 공유에 최적화 된 이동 하는 수행 하는 방법을 설명 합니다. 캐시 된 콘텐츠를 모든 지연 없이 로컬 오프 라인 파일 캐시에서 이름이 단순히 관리자로 리디렉션된 폴더를 호스트 하는 파일 공유를 이동 하 고 그룹 정책에서 리디렉션된 폴더의 대상 경로 업데이트 하는 경우이 정책 설정을 사용 하도록 설정 하면 또는 사용자에 대 한 잠재적인 데이터 손실입니다.

이전에 지연 된 로그인을 일으키는 리디렉션된 폴더에서 그룹 정책에서는 영향을 받는 사용자의 다음 번 로그인 시 파일을 복사 하는 클라이언트 컴퓨터의 대상 경로 관리자 변경할 수 없습니다. 또는 관리자는 파일 공유를 이동 하 고 그룹 정책에서 리디렉션된 폴더의 대상 경로 업데이트 수 없습니다. 그러나 이동 후 이동의 시작과 첫 번째 동기화 사이는 클라이언트 컴퓨터에 로컬로 만든 변경 내용을 손실 됩니다.

## <a name="prerequisites"></a>사전 요구 사항

최적화 된 이동에 다음 요구 사항이 있습니다.

- 폴더 리디렉션 설정 해야 합니다. 자세한 내용은 참조 [오프 라인 파일을 사용 하 여 폴더 리디렉션 배포](deploy-folder-redirection.md)합니다.
- 클라이언트 컴퓨터는 Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 또는 Windows Server (반기 채널) 실행 해야 합니다.

## <a name="step-1-enable-optimized-move-in-group-policy"></a>1단계: 그룹 정책에 최적화 된 이동을 사용합니다

폴더 리디렉션 데이터 재배치를 최적화 하려면 그룹 정책을 사용 하도록 설정 하려면 사용 합니다 **최적화 사용 폴더 리디렉션 서버 경로 변경 시 오프 라인 파일 캐시에서 콘텐츠 이동** 적절 한 그룹 정책에 대 한 정책 설정 개체 (GPO)입니다. 이 정책 설정을 구성 **사용 안 함** 또는 **구성 되지 않은** 하면 클라이언트가 새 위치로 모든 폴더 리디렉션 콘텐츠를 복사한 다음 경우 이전 위치에서 콘텐츠를 삭제 합니다 서버 경로 변경 합니다.

리디렉션된 폴더의 최적화 된 이동을 사용 하는 방법을 다음과 같습니다.

1. 폴더 리디렉션 설정에 대해 만든 GPO를 마우스 오른쪽 단추로 클릭 그룹 정책 관리에서 (예를 들어 **폴더 리디렉션 및 Roaming User Profiles Settings**)를 선택한 후 **편집**.
2. 아래 **사용자 구성**, 이동할 **정책을**, 한 다음 **관리 템플릿**, 다음 **시스템**, 다음  **폴더 리디렉션**합니다.
3. 마우스 오른쪽 단추로 클릭 **최적화 사용 폴더 리디렉션 서버 경로 변경 시 오프 라인 파일 캐시에서 콘텐츠 이동**를 선택한 후 **편집**합니다.
4. 선택 **Enabled**를 선택한 후 **확인**합니다.

## <a name="step-2-relocate-the-file-share-for-redirected-folders"></a>2단계: 리디렉션된 폴더에 대 한 파일 공유 위치 변경

폴더 리디렉션 사용자를 포함 하는 파일 공유를 이동할 때 가져오기 폴더 제대로 재배치 됩니다 있도록 예방 조치를 수행 합니다.

>[!IMPORTANT]
>사용자 파일에 있으면 사용 하거나 이동, 전체 파일 상태 유지 되지 않는 경우 동기화 충돌 오프 라인 파일 또는 데이터 손실이에서 생성 된 네트워크를 통해 파일이 복사 되는 대로 사용자 성능 저하를 경험할 수 있습니다.

1. 사용자에 게 알림 미리 리디렉션된 폴더에 호스팅하는 서버 변경 되며 다음 작업을 수행 하는 것이 좋습니다.

      - 오프 라인 파일 캐시의 내용을 동기화 하 고 충돌을 해결 합니다.
      - 관리자 권한 명령 프롬프트를 열고를 입력 **GpUpdate /Target:User /Force**, 그런 다음 로그 아웃 하 고 최신 그룹 정책 설정을 클라이언트 컴퓨터에 적용 되는지 확인 하려면 다시 로그인

        >[!NOTE]
        >기본적으로 클라이언트 컴퓨터 그룹 정책을 업데이트 90 분 마다 있도록 허용 하는 경우 충분 한 시간 클라이언트에 대 한 업데이트 된 정책을 수신 하는 컴퓨터를 사용 하도록 요청 필요가 없습니다 **GpUpdate**합니다.
2. 파일 공유의 파일이 사용에서 되는지 확인 하는 서버에서 파일 공유를 제거 합니다. 서버 관리자에서 수행 하는 **공유** 페이지 File and Storage Services의 적절 한 파일 공유를 마우스 오른쪽 단추로 클릭 한 다음 선택 **제거**합니다.

    이동이 완료 하 고 그룹 정책에서 업데이트 된 폴더 리디렉션 설정의 받을 때까지 오프 라인 파일을 사용 하 여 오프 라인으로 작업 합니다.

3. 백업 권한을 가진 계정을 사용 하는 백업과 같은 파일 타임 스탬프를 유지 하는 메서드를 사용 하 여 새 위치로 파일 공유의 콘텐츠를 이동 및 유틸리티를 복원 합니다. 사용 하는 **Robocopy** 명령을 관리자 권한 명령 프롬프트를 열고 다음 명령을 입력 위치 ```<Source>``` 는 파일 공유의 현재 위치 및 ```<Destination>``` 는 새 위치:

    ```PowerShell
    Robocopy /B <Source> <Destination> /Copyall /MIR /EFSRAW
    ```

    >[!NOTE]
    >합니다 **Xcopy** 명령을 모든 파일 상태를 유지 하지 않습니다.
4. 이동 하려는 각 리디렉션된 폴더에 대 한 대상 폴더 위치를 업데이트 하는 폴더 리디렉션 정책 설정을 편집 합니다. 자세한 내용은 참조의 4 단계 [오프 라인 파일을 사용 하 여 폴더 리디렉션 배포](deploy-folder-redirection.md)합니다.
5. 리디렉션된 폴더에 호스팅하는 서버 변경 하 고 사용 해야 하는 사용자에 게 알리는 합니다 **GpUpdate /Target:User /Force** 명령을 다음 다시 로그 아웃 하 고 업데이트 된 구성을 가져오고 적절 한 파일을 다시 시작에 다시 로그인 동기화 합니다.

    사용자는 모든 컴퓨터에 최소 한 번에 로그온 데이터 각 오프 라인 파일 캐시에 재배치 제대로 확인 합니다.

## <a name="more-information"></a>자세한 정보

* [오프 라인 파일을 사용 하 여 폴더 리디렉션 배포](deploy-folder-redirection.md)
* [로밍 사용자 프로필 배포](deploy-roaming-user-profiles.md)
* [폴더 리디렉션, 오프 라인 파일 및 로밍 사용자 프로필 개요](folder-redirection-rup-overview.md)