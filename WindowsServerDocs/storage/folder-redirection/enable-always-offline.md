---
title: 파일 액세스에 항상 오프 라인 모드를 사용 하도록 설정
description: 캐시 된 파일 및 리디렉션된 폴더에 빠르게 액세스할 수 있도록 오프 라인 파일의 항상 오프 라인 모드를 사용 하는 방법입니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: ddf6a816e417c2eddff090df8dba841a894a3255
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447676"
---
# <a name="enable-always-offline-mode-for-faster-access-to-files"></a>파일 액세스에 항상 오프 라인 모드를 사용 하도록 설정

>적용 대상: Windows 10, Windows 8, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012, Windows Server 2012 R2 및 Windows (반기 채널)

이 문서에는 캐시 된 파일 및 리디렉션된 폴더에 빠르게 액세스할 수 있도록 오프 라인 파일의 항상 오프 라인 모드를 사용 하는 방법을 설명 합니다. 항상 오프 라인 작업 때문에 사용자는 항상 오프 라인으로 고속 네트워크 연결을 통해 연결 되어 있는 경우 더 낮은 대역폭도 제공 합니다.

## <a name="prerequisites"></a>사전 요구 사항

항상 오프 라인 모드를 사용 하려면 환경의 다음 필수 조건을 충족 해야 합니다.

- 도메인에 가입 된 클라이언트 컴퓨터를 사용 하 여 사용 되는 Active Directory Domain Services (AD DS) 도메인입니다. 포리스트 또는 도메인 기능 수준 요구 사항 또는 스키마 요구 사항이 없는 합니다.
- Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 클라이언트 컴퓨터입니다. (이전 버전의 Windows 실행 하는 클라이언트 컴퓨터는 매우 고속 네트워크 연결에서 온라인 모드로 전환 계속 될 수 있습니다.)
- 설치 하는 그룹 정책 관리 된 컴퓨터입니다.

## <a name="enable-always-offline-mode"></a>항상 오프 라인 모드를 사용 하도록 설정

항상 오프 라인 모드를 사용 하려면 그룹 정책을 사용 하도록 설정 하려면 사용 합니다 **느린 링크 모드 구성** 정책이 설정 되 고 대기 시간으로 설정 **1** (밀리초)입니다. 이렇게 하면 클라이언트 컴퓨터를 자동으로 항상 오프 라인 모드를 사용 하도록 Windows 8 또는 Windows Server 2012를 실행 합니다.

>[!NOTE]
>Windows 7을 실행 하는 컴퓨터를 Windows Vista, Windows Server 2008 R2 또는 Windows Server 2008 계속 될 수 있습니다 온라인 모드로 전환 하는 네트워크 연결의 대기 시간이 1 밀리초 아래로 떨어질 경우.

1. 오픈 **그룹 정책 관리**합니다.
2. 필요에 따라 오프 라인 파일 설정에 대 한 새 그룹 정책 개체 (GPO)를 만들려면 적절 한 도메인 또는 조직 구성 단위 (OU)를 마우스 오른쪽 단추로 클릭 하 고 선택한 **이 도메인에서 GPO를 만들어 여기에 연결**합니다.
3. 콘솔 트리에서 오프 라인 파일 설정을 구성 하 고 선택한 GPO를 마우스 오른쪽 단추로 **편집**합니다. 합니다 **그룹 정책 관리 편집기** 나타납니다.
4. 콘솔 트리에서 아래 **컴퓨터 구성**, 확장 **정책을**, 확장 **관리 템플릿**를 확장 하 고 **네트워크**, 확장 **오프 라인 파일**합니다.
5. 마우스 오른쪽 단추로 클릭 **느린 링크 모드 구성**를 선택한 후 **편집**합니다. 합니다 **느린 링크 모드 구성** 창이 표시 됩니다.
6. **사용**을 선택합니다.
7. 에 **옵션** 상자에서 **표시**합니다. 합니다 **내용 표시 창** 나타납니다.
8. 에 **값 이름** 상자에서 항상 오프 라인 모드를 사용 하도록 설정 하려는 파일 공유를 지정 합니다.
9. 모든 파일 공유에 항상 오프 라인 모드를 사용 하려면 입력 * *\\* * * 합니다.
10. 에 **값** 상자에 입력 합니다 **대기 시간 = 1** 대기 시간 임계값을 1 밀리초로 설정 하 여 선택한 **확인**합니다.

>[!NOTE]
>기본적으로 항상 오프 라인 모드에 있을 때 Windows 파일 동기화는 백그라운드에서 오프 라인 파일 캐시에 2 시간 마다. 이 값을 변경 하려면 사용 합니다 **Configure Background Sync** 정책 설정 합니다.

## <a name="more-information"></a>자세한 정보

* [폴더 리디렉션, 오프 라인 파일 및 로밍 사용자 프로필 개요](folder-redirection-rup-overview.md)
* [오프 라인 파일을 사용 하 여 폴더 리디렉션 배포](deploy-folder-redirection.md)