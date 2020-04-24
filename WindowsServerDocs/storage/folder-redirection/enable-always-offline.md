---
title: 파일에 더 빠르게 액세스할 수 있도록 항상 오프라인 모드 사용
description: 오프라인 파일의 항상 오프라인 모드를 사용하여 캐시된 파일과 리디렉션된 폴더에 더 빠르게 액세스할 수 있도록 하는 방법입니다.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 389fdd26a7e1d9824f1eaf0136a544547f08eb05
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "71401959"
---
# <a name="enable-always-offline-mode-for-faster-access-to-files"></a>파일에 더 빠르게 액세스할 수 있도록 항상 오프라인 모드 사용

>적용 대상: Windows 10, Windows 8, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012, Windows Server 2012 R2 및 Window(반기 채널)

이 문서에서는 오프라인 파일의 항상 오프라인 모드를 사용하여 캐시된 파일과 리디렉션된 폴더에 더 빠르게 액세스할 수 있도록 하는 방법을 설명합니다. 사용자는 고속 네트워크 연결을 통해 연결된 경우에도 항상 오프라인으로 작업하므로 항상 오프라인은 낮은 대역폭 사용량을 제공합니다.

## <a name="prerequisites"></a>필수 구성 요소

항상 오프라인 모드를 활성화하려면 사용자 환경이 다음 필수 조건을 충족해야 합니다.

- 클라이언트 컴퓨터가 도메인에 가입된 AD DS(Active Directory Domain Services) 도메인 포리스트 또는 도메인 기능 수준 요구 사항 또는 스키마 요구 사항은 없습니다.
- Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행하는 클라이언트 컴퓨터 (이전 버전의 Windows를 실행하는 클라이언트 컴퓨터는 고속 네트워크 연결에서 온라인 모드로 계속해서 전환될 수 있습니다.)
- 그룹 정책 관리가 설치된 컴퓨터

## <a name="enable-always-offline-mode"></a>항상 오프라인 모드 사용

항상 오프라인 모드를 사용하도록 설정하려면 그룹 정책을 사용하여 **저속 링크 모드 구성** 정책 설정을 사용하도록 설정하고 대기 시간을 **1**(밀리초)로 설정합니다. 이렇게 하면 Windows 8 또는 Windows Server 2012를 실행하는 클라이언트 컴퓨터에서 항상 오프라인 모드를 자동으로 사용할 수 있습니다.

>[!NOTE]
>네트워크 연결 대기 시간이 1밀리초 미만으로 떨어지면 Windows 7, Windows Vista, Windows Server 2008 R2 또는 Windows Server 2008을 실행하는 컴퓨터가 온라인 모드로 계속해서 전환될 수 있습니다.

1. **그룹 정책 관리**를 엽니다.
2. 필요에 따라 오프라인 파일 설정에 대한 새 GPO(그룹 정책 개체)를 만들려면 적절한 도메인 또는 OU(조직 구성 단위)를 마우스 오른쪽 단추로 클릭한 다음, **이 도메인에서 GPO 만들기 및 여기에서 연결**을 선택합니다.
3. 콘솔 트리에서 오프라인 파일 설정을 구성하려는 GPO를 마우스 오른쪽 단추로 클릭한 다음, **편집**을 선택합니다. **그룹 정책 관리 편집기**가 표시됩니다.
4. 콘솔 트리의 **컴퓨터 구성**에서 **정책**, **관리 템플릿**, **네트워크**, **오프라인 파일**을 차례로 확장합니다.
5. **저속 링크 모드 구성**을 마우스 오른쪽 단추로 클릭한 다음, **편집**을 선택합니다. **저속 링크 모드 구성** 창이 표시됩니다.
6. **사용**을 선택합니다.
7. **옵션** 상자에서 **표시**를 선택합니다. **내용 표시 창**이 표시됩니다.
8. **값 이름** 상자에서 항상 오프라인 모드를 사용하도록 설정할 파일 공유를 지정합니다.
9. 모든 파일 공유에서 항상 오프라인 모드를 사용하도록 설정하려면 **\*** 를 입력합니다.
10. **값** 상자에 **대기 시간 = 1**을 입력하여 대기 시간 임계값을 1밀리초로 설정한 다음, **확인**을 선택합니다.

>[!NOTE]
>기본적으로 항상 오프라인 모드에서 Windows는 2시간마다 백그라운드에서 오프라인 파일 캐시의 파일을 동기화합니다. 이 값을 변경하려면 **백그라운드 동기화 구성** 정책 설정을 사용합니다.

## <a name="more-information"></a>자세한 정보

* [폴더 리디렉션, 오프라인 파일 및 로밍 사용자 프로필 개요](folder-redirection-rup-overview.md)
* [오프라인 파일을 사용한 폴더 리디렉션 배포](deploy-folder-redirection.md)