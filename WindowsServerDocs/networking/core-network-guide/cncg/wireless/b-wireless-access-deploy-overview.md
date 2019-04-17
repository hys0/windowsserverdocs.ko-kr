---
title: 무선 액세스 배포 개요
description: 이 항목은 Windows Server 2016 네트워킹 가이드 "배포 암호 기반 802.1 X 인증 된 무선 액세스"
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 29ae0f54-f045-465a-a08e-5867979345f2
author: shortpatti
ms.author: pashort
ms.openlocfilehash: 11d87254d8819606a06acedd407bb2e09a45cb60
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="wireless-access-deployment-overview"></a>무선 액세스 배포 개요

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

다음 그림 802.1 X를 배포 하는 데 필요한 구성 요소 인증 PEAP\ 기능 MS\ 기능을 제공 v 2 무선 액세스 보여 줍니다.  

![802.1 X 배포 Infrastructure 개요](../../../media/8021X-Deploy-Overview/8021X-Deploy-Overview.jpg)

## <a name="wireless-access-deployment-components"></a>무선 액세스 배포 구성 요소
다음 infrastructure 무선 액세스 배포용이 필요 합니다.

### <a name="8021x-capable-wireless-access-points"></a>802.1X\-지원 무선 액세스 포인트
로컬 영역 무선 네트워크를 지 원하는 필요한 네트워크 infrastructure 서비스 장소에는, 한 후 무선 Ap 위치에 대 한 디자인 프로세스를 시작할 수 있습니다. 무선 AP 배포 디자인 프로세스는 다음이 단계를 수행합니다.

- 무선 사용자에 대 한 보상 영역을 확인 합니다. 하는 동안 범위를 영역을 식별 건물 외부 무선 서비스를 제공 하려는 여부를 확인 하 고 어디에 있는지 확인 특별히 외부 영역 합니다.

- 적절 한 범위를 배포 하는 무선 개수 Ap 확인 합니다.

- 무선 Ap 위치를 결정 합니다.

- 무선 앱에는 채널 빈도 선택 합니다.

### <a name="active-directory-domain-services"></a>Active Directory Domain Services
다음 AD DS 요소가 무선 액세스 설치 해야 합니다.

#### <a name="users-and-computers"></a>사용자와 컴퓨터

및 사용 하 여 Active Directory 사용자의 snap\ 컴퓨터 사용자 계정을 만들고 관리 하 고 각 도메인 구성원을 무선 액세스 권한을 부여할 원하는 포함 된 무선 보안 그룹을 만들 수 있습니다.

#### <a name="wireless-network-ieee-80211-policies"></a>무선 네트워크 \ (IEEE 802.11\) 정책

무선 네트워크를 사용할 수 있는 \ (IEEE 802.11\) 네트워크에 액세스 하려고 할 때 무선 컴퓨터에 적용 되는 정책 구성 하려면 그룹 정책 관리 정책 확장 합니다.

그룹 정책 관리 편집기에서 때 하면 right\ 클릭 **무선 네트워크 \ (IEEE 802.11\) 정책**, 유형의 만든 무선 정책에 대 한 다음 두 가지 옵션을 사용할 수 있습니다.

- **이후 릴리스 및 Windows Vista에 대 한 무선 네트워크 정책 새로 만들기**

- **Windows XP 정책 새로 만들기**

>[!TIP]
>새 무선 네트워크 정책, 구성 이름과 정책 설명을 변경할 수 있는 옵션이 있는 합니다. 정책 이름 변경 하면 변경에 반영 되는 **세부 정보** 창 그룹 정책 관리 편집기의 및 제목 표시줄 무선 네트워크 정책 대화 상자에서 합니다. 사용자 이름을 바꾸려면 어떻게 정책에 관계 없이 새로운 XP 무선 정책 항상 나열 됩니다 그룹 정책 관리 편집기에와 **종류** 표시 **XP**합니다. 다른 정책으로 나열 된는 **종류** 표시 **Vista 하 고 나중에 릴리스**합니다.  

Windows Vista에 대 한 무선 네트워크 정책 및 나중에 릴리스 구성 우선 순위를 지정 하 고 여러 무선 프로필 관리할 수 있습니다. 무선 프로필 연결 및 특정 무선 네트워크에 연결 하는 데 사용 하는 보안 설정 모음입니다. 그룹 정책 무선 클라이언트 컴퓨터에 업데이트에 무선 네트워크 정책 만드는 프로필 무선 네트워크 정책이 적용 되는 무선 클라이언트 컴퓨터 구성에 자동으로 추가 됩니다.

##### <a name="allowing-connections-to-multiple-wireless-networks"></a>여러 개의 무선 네트워크에 연결을 허용

조직의 실제 위치 간에 이동 무선 클라이언트를 사용 하는 경우와 같이 주 office는 지점 사이의 것이 좋습니다 컴퓨터에 둘 이상의 무선 네트워크에 연결할 합니다. 이 경우 각 네트워크에 대 한 특정 연결 및 보안 설정을 포함 하는 무선 프로필을 구성할 수 있습니다.

예를 들어, 회사의 서비스 집합 id 주 회사 office에 대 한 무선 네트워크 \(SSID\) WlanCorp 합니다.

또한 사용자 지점에서에 연결 하려는 무선 네트워크 합니다. 지점에 SSID WlanBranch로 구성 되어 있습니다.

이 시나리오에서 각 네트워크 하 고 컴퓨터 또는 회사 사무실에서 사용 되는 다른 디바이스에 대해 프로필 구성할 수 있습니다 및 지점은 실제로 네트워크 적용 범위 범위 내에 무선 네트워크 중 하나에 연결할 수 있습니다.

##### <a name="mixed-mode-wireless-networks"></a>무선 네트워크 Mixed\ 모드

네트워크에 무선 컴퓨터 및 디바이스를 지 원하는 다른 보안 표준 mixture 가정 또는 합니다. 일부 이전 컴퓨터 경우가 무선 어댑터에 최신 디바이스 강력한 WPA2\ 엔터프라이즈 표준 사용할 수 있지만 WPA\ Enterprise 에서만 사용할 수 있습니다.

동일한 SSID 및 거의 동일 연결 및 보안 설정을 사용 하는 두 가지 프로필 만들 수 있습니다.

한 프로필에 무선 인증 WPA2\ 엔터프라이즈 AES 사용 하도록 설정할 수 있습니다 하 고 다른 윤곽에서 WPA\ 엔터프라이즈 TKIP으로 지정할 수 있습니다.

이 일반적으로 이라고 mixed\ 모드 배포 하 고 컴퓨터의 다양 한 종류 및 무선 기능 동일한 무선 네트워크를 공유할 수 있습니다.

### <a name="network-policy-server-nps"></a>정책 서버 네트워크 \(NPS\)
NPS는 네트워크 연결 요청 인증과 대 한 액세스 정책을 적용을 만들고 수 있습니다.

NPS RADIUS 서버도 사용 하 여에 NPS RADIUS 클라이언트로 무선 액세스 포인트 등 네트워크 액세스 서버를 구성할 수 있습니다. NPS 사용 하 여 액세스 클라이언트 인증 하 고 자녀가 연결 요청을 승인 하는 네트워크 정책 구성할 수도 있습니다.  

### <a name="wireless-client-computers"></a>무선 클라이언트 컴퓨터
이 가이드 함으로써 무선 클라이언트 컴퓨터는 컴퓨터와 IEEE 802.11 무선 네트워크 어댑터는 장착 및 클라이언트 Windows 또는 Windows Server 운영 체제를 실행 하는 다른 디바이스입니다.

#### <a name="server-computers-as-wireless-clients"></a>무선 클라이언트로 서버 컴퓨터

기본적으로 802.11 무선에 대 한 기능은 Windows Server를 실행 하는 컴퓨터에서 사용할 수 없습니다.

서버 운영 체제를 실행 하는 컴퓨터의 무선 연결을 사용 하 여 설치 하 고 해야 무선 LAN \(WLAN\) 사용 서버 관리자에서 Windows PowerShell 또는 역할 추가 및 기능 마법사 중 하나를 사용 하 여 서비스 기능입니다.

설치 하는 경우는 **무선 LAN 서비스** 기능을 새로운 서비스 **WLAN 자동 구성** 에 설치 되어 **서비스**합니다. 설치가 완료 되 면 서버를 다시 시작 해야 합니다.

서버를 다시 시작한 후에 액세스할 수 있습니다 WLAN 자동 구성 클릭할 때 **시작**, **Windows 관리 도구**, 및 **서비스**합니다.

설치 및 서버를 다시 시작 중지 상태로 시작 유형의 서비스는 WLAN 자동 구성 **자동**합니다. 서비스를 시작 하려면 두 번 클릭 **WLAN 자동 구성**합니다. 에 **일반** 탭을 클릭 **시작**을 차례로 클릭 하 고 **확인**합니다.

WLAN 자동 구성 서비스 무선 어댑터 열거 고 무선 연결을 설정 하는 무선 네트워크에 연결 하는 서버 구성 하는 데 필요한를 포함 하는 무선 프로필 관리 합니다.

무선 액세스 배포 개요를 참조 하세요. [무선 액세스 배포 프로세스](c-wireless-access-deploy-process.md)합니다.
