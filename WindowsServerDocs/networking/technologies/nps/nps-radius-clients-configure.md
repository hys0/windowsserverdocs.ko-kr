---
title: RADIUS 클라이언트 구성
description: 이 항목에서는 Windows Server 2016에서 네트워크 정책 서버에 대 한 RADIUS 클라이언트를 구성 하는 방법에 대 한 정보를 제공 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: cde37849-ce79-4c26-aa14-cd0ef31cae18
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 851bdb0677a17567f81a2c331baad595fe40436a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839494"
---
# <a name="configure-radius-clients"></a>RADIUS 클라이언트 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 네트워크 액세스 서버를 NPS에서 RADIUS 클라이언트로 구성에 사용할 수 있습니다.

새 네트워크 액세스 서버를 추가 하는 경우 \(VPN 서버, 스위치 또는 전화 접속 서버 인증 무선 액세스 지점\) 네트워크에 서버를 NPS에서 RADIUS 클라이언트로 추가 하며 통신 하도록 RADIUS 클라이언트 구성 NPS 합니다.

>[!IMPORTANT]
>클라이언트 컴퓨터 및 장치를 랩톱, 태블릿, 휴대폰 및 클라이언트 운영 체제를 실행 하는 다른 컴퓨터와 같은 RADIUS 클라이언트가 아닙니다. RADIUS 클라이언트는 네트워크 액세스 서버-무선 액세스 지점과 같은 802.1 X 가능 스위치, 가상 개인 네트워크 (VPN) 서버 및 전화 접속 서버-네트워크 정책과 같은 RADIUS 서버와 통신 하는 RADIUS 프로토콜을 사용 하기 때문에 서버 \(NPS\) 서버.

이 단계에 NPS가 프록시를 NPS에 구성 된 원격 RADIUS 서버 그룹의 멤버인 경우 필요한 이기도 합니다. 이 경우에 NPS 프록시에이 작업의 단계를 수행 하는 것 외에도 다음을 수행 해야 합니다.

- NPS 프록시에서 NPS를 포함 하는 원격 RADIUS 서버 그룹을 구성 합니다.
- 원격 NPS에서 RADIUS 클라이언트로 NPS 프록시를 구성 합니다.

이 항목의 절차를 수행 하려면 네트워크 액세스 서버를 하나 이상 있어야 \(VPN 서버, 스위치 또는 전화 접속 서버 인증 무선 액세스 지점\) 또는 NPS 프록시 네트워크에 물리적으로 설치 합니다.

## <a name="configure-the-network-access-server"></a>네트워크 액세스 서버 구성

NPS와 함께 사용 하 여에 대 한 네트워크 액세스 서버를 구성 하려면이 절차를 따르십시오. RADIUS 클라이언트와 네트워크 액세스 서버 (Nas)를 배포 하면는 Nas 클라이언트로 구성 된 위치 NPSs 통신할 클라이언트를 구성 해야 합니다.

이 절차는 사용 하 여 구성에 Nas; 설정에 대 한 일반적인 지침을 제공 네트워크에서 배포 하는 장치를 구성 하는 방법에 대 한 특정 내용은 NAS 제품 설명서를 참조 하세요.

### <a name="to-configure-the-network-access-server"></a>네트워크 액세스 서버를 구성 하려면

1. NAS를에서 **RADIUS 설정을**를 선택 **RADIUS 인증** 사용자 데이터 그램 프로토콜 (UDP) 포트에서 **1812** 및 **RADIUS 계정을**UDP 포트로 **1813**합니다.
2. **authentication** 또는 **RADIUS 서버**, IP 주소 또는 정규화 된 도메인 이름 (FQDN)으로 NAS의 요구 사항에 따라에 NPS를 지정 합니다. 
3. **비밀** 하거나 **공유 비밀**, 강력한 암호를 입력 합니다. NPS에서 RADIUS 클라이언트로 NAS를 구성한 경우에 같은 암호를 잊지 말고 하므로 사용 합니다.
4. 사용할 경우 PEAP 또는 EAP 인증 방법으로, NAS EAP 인증을 사용 하도록 구성 합니다.
5. 무선 액세스 지점에 구성 하는 경우 **SSID**, 서비스 설정 식별자를 지정 \(SSID\)는 네트워크 이름으로 사용 되는 영숫자 문자열입니다. 이 이름은 무선 클라이언트 액세스 지점이 브로드캐스트 고 무선 사용자 신뢰할 수 있는 사용자에 게 표시 \(Wi-fi\) 핫스폿 합니다.
6. 무선 액세스 지점을 구성 하는 경우 **802.1 X 및 WPA**를 사용 하도록 설정 **IEEE 802.1x 인증** PEAP-2(MS-CHAP v2, PEAP-TLS 또는 EAP-TLS를 배포 하려는 경우.

## <a name="add-the-network-access-server-as-a-radius-client-in-nps"></a>네트워크 액세스 서버를 NPS에서 RADIUS 클라이언트로 추가

이 절차를 사용 하 여 네트워크 액세스 서버를 NPS에서 RADIUS 클라이언트로 추가 합니다. NPS 콘솔을 사용 하 여 RADIUS 클라이언트와 NAS를 구성 하려면이 절차를 사용할 수 있습니다.

이 절차를 완료 하려면의 구성원 이어야는 **관리자** 그룹입니다.

### <a name="to-add-a-network-access-server-as-a-radius-client-in-nps"></a>네트워크 액세스 서버를 NPS에서 RADIUS 클라이언트로 추가 하려면

1. NPS를 서버 관리자에서 클릭 **도구**를 클릭 하 고 **네트워크 정책 서버**합니다. NPS 콘솔이 열립니다.
2. NPS 콘솔을 두 번 클릭 **RADIUS 클라이언트 및 서버**합니다. 마우스 오른쪽 단추로 클릭 **RADIUS 클라이언트**를 클릭 하 고 **새 RADIUS 클라이언트**합니다. 
3. **새 RADIUS 클라이언트**, 있는지는 **이 RADIUS 클라이언트를 사용 하도록 설정** 확인란을 선택 합니다.
4. **새 RADIUS 클라이언트**의 **이름을**, NAS에 대 한 표시 이름을 입력 합니다. **주소 (IP 또는 DNS)**, NAS IP 주소 또는 정규화 된 도메인 이름 (FQDN)을 입력 합니다. FQDN을 입력 하는 경우 클릭 **확인** 이름을 올바르고 유효한 IP 주소로 매핑합니다 있는지를 확인 하려는 경우. 
5. **새 RADIUS 클라이언트**의 **공급 업체**, NAS 제조업체의 이름을 지정 합니다. NAS 제조업체의 이름을 정확히 알지 못하는 경우 선택 **RADIUS 표준**합니다.
6. **새 RADIUS 클라이언트**의 **공유 비밀**, 다음 중 하나를 수행 합니다.
    - 했는지 **수동** 을 선택 하면 선택한 다음 **공유 비밀**, NAS에도 입력 하는 강력한 암호를 입력 합니다. 공유 암호를 다시 입력 **공유 암호 확인**합니다.
    - 선택 **생성**를 클릭 하 고 **생성** 공유 암호를 자동으로 생성 합니다. NPS와 통신할 수 있도록 NAS에 구성에 대 한 생성 된 공유 암호를 저장 합니다.
7. **새 RADIUS 클라이언트**의 **추가 옵션**EAP 및 PEAP 이외의 모든 인증 방법을 사용 하는 경우에 해당 하는 NAS 지원 메시지 인증자 특성을 사용 하는 경우 선택 **액세스 요청 메시지의 메시지 인증자 특성 있어야 합니다.** 합니다.
8. **확인**을 클릭합니다. 해당 하는 NAS NPS에 구성 된 RADIUS 클라이언트의 목록에 나타납니다.

## <a name="configure-radius-clients-by-ip-address-range-in-windows-server-2016-datacenter"></a>Windows Server 2016 Datacenter의 IP 주소 범위에서 RADIUS 클라이언트 구성

Windows Server 2016 Datacenter를 실행 하는 경우에 IP 주소 범위로 NPS에서 RADIUS 클라이언트를 구성할 수 있습니다. 이 옵션을 사용 하면 각 RADIUS 클라이언트를 개별적으로 추가 하는 대신 한 번에 많은 수의 RADIUS 클라이언트 (예: 무선 액세스 지점) NPS 콘솔에 추가할 수 있습니다.

Windows Server 2016 Standard에 NPS를 실행 하는 경우 IP 주소 범위에서 RADIUS 클라이언트를 구성할 수 없습니다.

동일한 IP 주소 범위에서 IP 주소를 사용 하 여 모든 구성 된 RADIUS 클라이언트와 네트워크 액세스 서버 (Nas)의 그룹을 추가 하려면이 절차를 따르십시오.

모든 범위에서 RADIUS 클라이언트에는 동일한 구성 및 공유 암호를 사용 해야 합니다.

이 절차를 완료 하려면의 구성원 이어야는 **관리자** 그룹입니다.

### <a name="to-set-up-radius-clients-by-ip-address-range"></a>RADIUS 클라이언트 IP 주소 범위 설정

1. NPS를 서버 관리자에서 클릭 **도구**를 클릭 하 고 **네트워크 정책 서버**합니다. NPS 콘솔이 열립니다.
2. NPS 콘솔을 두 번 클릭 **RADIUS 클라이언트 및 서버**합니다. 마우스 오른쪽 단추로 클릭 **RADIUS 클라이언트**를 클릭 하 고 **새 RADIUS 클라이언트**합니다.
3. **새 RADIUS 클라이언트**의 **이름을**, Nas의 컬렉션에 대 한 표시 이름을 입력 합니다.
4. **주소 \(IP 또는 DNS\)**, Classless Inter-domain Routing를 사용 하 여 RADIUS 클라이언트에 대 한 IP 주소 범위 입력 \(CIDR\) 표기법입니다. Nas의 IP 주소 범위 10.10.0.0 인 경우 입력 하는 예를 들어 **10.10.0.0/16**합니다.
5. **새 RADIUS 클라이언트**의 **공급 업체**, NAS 제조업체의 이름을 지정 합니다. NAS 제조업체의 이름을 정확히 알지 못하는 경우 선택 **RADIUS 표준**합니다.
6. **새 RADIUS 클라이언트**의 **공유 비밀**, 다음 중 하나를 수행 합니다.
    - 했는지 **수동** 을 선택 하면 선택한 다음 **공유 비밀**, NAS에도 입력 하는 강력한 암호를 입력 합니다. 공유 암호를 다시 입력 **공유 암호 확인**합니다.
    - 선택 **생성**를 클릭 하 고 **생성** 공유 암호를 자동으로 생성 합니다. NPS와 통신할 수 있도록 NAS에 구성에 대 한 생성 된 공유 암호를 저장 합니다.
7. **새 RADIUS 클라이언트**의 **추가 옵션**EAP 및 PEAP 이외의 모든 인증 방법을 사용 하 고 모든 프로그램 Nas 지원 메시지 인증자 특성을 사용 하는 경우 선택 경우, **액세스 요청 메시지의 메시지 인증자 특성 있어야 합니다.** 합니다.
8. **확인**을 클릭합니다. 프로그램 Nas NPS에 구성 된 RADIUS 클라이언트의 목록에 표시 합니다.

자세한 내용은 [RADIUS 클라이언트](nps-radius-clients.md)합니다.

NPS에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 (NPS 서버)](nps-top.md)합니다.