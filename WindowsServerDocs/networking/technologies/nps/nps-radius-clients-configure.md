---
title: 구성 RADIUS 클라이언트
description: 이 항목에서는 RADIUS 클라이언트 네트워크 정책 서버 Windows Server 2016에 대 한 구성에 대 한 정보를 제공 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: cde37849-ce79-4c26-aa14-cd0ef31cae18
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9af3189199c8282394ca34f181a90b4290c55044
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="configure-radius-clients"></a>구성 RADIUS 클라이언트

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

네트워크 액세스 서버에서 NPS RADIUS 클라이언트로 구성 하려면이 항목을 사용할 수 있습니다.

새 네트워크 액세스 서버를 추가할 때 \ (VPN 서버의 무선 액세스 포인트, 스위치를 또는 전화 접속 server\ 인증), 네트워크, NPS RADIUS 클라이언트로 서버를 추가 하 고 다음 구성 해야 RADIUS 클라이언트 NPS 서버와 통신 하도록 합니다.

>[!IMPORTANT]
>클라이언트 컴퓨터와 노트북 컴퓨터, 태블릿, 휴대폰 및 클라이언트 운영 체제를 실행 하는 다른 컴퓨터 등의 디바이스 RADIUS 클라이언트 되지 않습니다. RADIUS 클라이언트는 무선 액세스 포인트 등 네트워크 액세스 서버-802.1 X 지원 전환, 가상 개인 네트워크 (VPN) 서버, 및 전화 접속 서버-네트워크 정책 서버 \(NPS\) 서버 등 RADIUS 서버와 통신 하도록 RADIUS 프로토콜을 사용 하기 때문입니다.

이 단계는 NPS 서버 NPS 프록시에서 구성 된 원격 RADIUS 서버 그룹의 회원 경우에 필요 합니다. 이 작업 NPS 프록시의 단계를 수행 하는 것 외에도이 경우 다음을 수행 해야 합니다.

- NPS 프록시 NPS 서버를 포함 하 여 원격 RADIUS 서버 그룹을 구성 합니다.
- 원격 NPS 서버에 프록시 NPS RADIUS 클라이언트로 구성 합니다.

이 항목에서 절차를 수행 하려면 하나 이상의 네트워크 액세스 서버 있어야 \ (VPN 서버의 무선 액세스 포인트, 스위치를 또는 전화 접속 server\ 인증) 또는 NPS 프록시 실제로 네트워크에 설치 되어 있습니다.

## <a name="configure-the-network-access-server"></a>네트워크 액세스 서버 구성

이 절차를 사용 하 여 네트워크 액세스 서버를 사용할 수 있도록 NPS 구성 합니다. 네트워크 Nas 액세스 서버 () RADIUS 클라이언트로 배포할 때 클라이언트가 되는 Nas 클라이언트로 구성 NPS 서버와 통신할 수 구성 해야 합니다.

이 절차를 제공 해야 사용 하 여 구성 Nas, 설정에 대 한 일반적인 지침 네트워크에서 배포 하는 디바이스를 구성 하는 방법에 대 한 자세한 내용은 NAS 제품 설명서를 참조 합니다.

### <a name="to-configure-the-network-access-server"></a>네트워크 액세스 서버 구성 하려면

1. NAS에 **RADIUS 설정**선택 **RADIUS 인증** 사용자 데이터 그램 Protocol (UDP) 포트에서 **1812** 및 **RADIUS 계정을** UDP 포트에서 **1813**합니다.
2. **인증 서버** 또는 **RADIUS 서버**, IP 주소 또는 NAS의 요구 사항에 따라 정식된 도메인 이름 (FQDN) NPS 서버 사용자 지정 합니다. 
3. **비밀** 또는 **공유 암호**, 강력한 암호를 입력 합니다. NAS NPS RADIUS 클라이언트로 구성할 때 잊지 마십시오 되므로 동일한 암호를 사용 합니다.
4. 을 사용 중인 PEAP 또는 EAP 인증 방법으로 EAP 인증을 사용 하 여 NAS를 구성 합니다.
5. 무선 액세스 포인트를 구성 하는 경우 **SSID**, 네트워크 이름으로 사용 되는 영숫자는 식별자를 설정 하는 서비스 \(SSID\)를 지정 합니다. 이 이름은 무선 클라이언트 하려면 액세스 지점에서 방송 하 고 무선 정확도 \(Wi-Fi\) 핫스팟에서 사용자에 게 표시 됩니다.
6. 무선 액세스 포인트를 구성 하는 경우 **802.1 X와 WPA**를 사용 하도록 설정 **IEEE 802.1 X 인증** PEAP 암호 v2, PEAP-TLS, 또는 EAP-TLS 배포 해야 합니다.

## <a name="add-the-network-access-server-as-a-radius-client-in-nps"></a>네트워크 액세스 서버 NPS RADIUS 클라이언트로 추가

네트워크 액세스 서버 NPS RADIUS 클라이언트로 추가할이 절차를 사용 합니다. 이 절차 NPS 본체를 사용 하 여 RADIUS 클라이언트로 NAS 구성에 사용할 수 있습니다.

이 절차를 완료 하려면의 회원 있어야는 **관리자** 그룹입니다.

### <a name="to-add-a-network-access-server-as-a-radius-client-in-nps"></a>네트워크 액세스 서버 NPS RADIUS 클라이언트로 추가 하려면

1. 서버 관리자에서 NPS 서버에서 클릭 **도구**을 차례로 클릭 하 고 **네트워크 정책 서버**합니다. NPS console을 엽니다.
2. 두 번 클릭 NPS 콘솔에서 **RADIUS 클라이언트 및 서버**합니다. 마우스 오른쪽 단추로 클릭 **RADIUS 클라이언트**을 차례로 클릭 하 고 **새 RADIUS 클라이언트**합니다. 
3. **새 RADIUS 클라이언트**, 되어 있는지 확인는 **이 RADIUS 클라이언트를 사용 하도록 설정** 확인란을 선택 합니다.
4. **새 RADIUS 클라이언트**에 **이름**, NAS의 표시 이름을 입력 합니다. **(IP 또는 DNS) 주소**, NAS IP 주소 또는 정식된 FQDN (도메인 이름)을 입력 합니다. FQDN 입력 하면 클릭 **확인** 이름이 올바른지, 지도 유효한 IP 주소를 확인 하려면. 
5. **새 RADIUS 클라이언트**에 **공급 업체**, NAS 제조업체의 이름을 지정 합니다. NAS 제조업체의 이름을 모르는 경우 **RADIUS 표준**합니다.
6. **새 RADIUS 클라이언트**에 **공유 암호**에서 다음 중 하나를 수행 합니다.
    - 되도록 **수동** 선택 되어 한 다음 **공유 암호**, NAS에도 입력 강력한 암호를 입력 합니다. 공유에서 암호를 다시 입력 **공유 암호 확인**합니다.
    - 선택 **생성**을 차례로 클릭 하 고 **생성** 를 자동으로 공유 암호를 생성 합니다. NPS 서버와 통신할 수 있도록 NAS에서 생성 된 공유 구성에 대 한 암호를 저장 합니다.
7. **새 RADIUS 클라이언트**에 **추가 옵션**지원 메시지 인증 특성을 사용 하 여 NAS 선택 EAP와 PEAP 이외의 인증 방법을 사용 하는 경우, **액세스 요청 메시지 메시지 인증자 특성 있어야**합니다.
8. 클릭 **확인**합니다. 사용자 NAS RADIUS 클라이언트 NPS 서버에서 구성 된 목록에 표시 됩니다.

## <a name="configure-radius-clients-by-ip-address-range-in-windows-server-2016-datacenter"></a>Windows Server 2016 데이터 센터에 IP 주소 범위도 RADIUS 클라이언트를 구성 합니다.

Windows Server 2016 데이터 센터를 실행 하는 경우 IP 주소 범위 하 여에서 NPS RADIUS 클라이언트 구성할 수 있습니다. 각 RADIUS 클라이언트를 개별적으로 추가 하는 대신 한 번에 많은 (예: 무선 액세스 포인트) RADIUS 클라이언트 NPS 콘솔에 추가할 수 있습니다.

Windows Server 2016 표준 NPS을 실행 하는 경우 IP 주소 범위 RADIUS 클라이언트를 구성할 수 없습니다.

이 절차를 사용 하 여 동일한 IP 주소 범위의 IP 주소를 가진 구성 RADIUS 클라이언트로 그룹 네트워크 Nas 액세스 서버 ()을 추가 합니다.

모든 범위에 RADIUS 클라이언트 같은 구성 및 공유 암호 사용 해야 합니다.

이 절차를 완료 하려면의 회원 있어야는 **관리자** 그룹입니다.

### <a name="to-set-up-radius-clients-by-ip-address-range"></a>IP 주소 범위 RADIUS 클라이언트를 설정 하려면

1. 서버 관리자에서 NPS 서버에서 클릭 **도구**을 차례로 클릭 하 고 **네트워크 정책 서버**합니다. NPS console을 엽니다.
2. 두 번 클릭 NPS 콘솔에서 **RADIUS 클라이언트 및 서버**합니다. 마우스 오른쪽 단추로 클릭 **RADIUS 클라이언트**을 차례로 클릭 하 고 **새 RADIUS 클라이언트**합니다.
3. **새 RADIUS 클라이언트**에 **이름**, 컬렉션 Nas의 표시 이름을 입력 합니다.
4. **주소 \(IP or DNS\)**, RADIUS 클라이언트 클래스 없는 도메인 간 경로 \(CIDR\) 표기법을 사용 하 여 IP 주소 범위를 입력 합니다. 예를 들어, IP 주소 범위는 Nas에 대 한 10.10.0.0 면 입력 **10.10.0.0/16**합니다.
5. **새 RADIUS 클라이언트**에 **공급 업체**, NAS 제조업체의 이름을 지정 합니다. NAS 제조업체의 이름을 모르는 경우 **RADIUS 표준**합니다.
6. **새 RADIUS 클라이언트**에 **공유 암호**에서 다음 중 하나를 수행 합니다.
    - 되도록 **수동** 선택 되어 한 다음 **공유 암호**, NAS에도 입력 강력한 암호를 입력 합니다. 공유에서 암호를 다시 입력 **공유 암호 확인**합니다.
    - 선택 **생성**을 차례로 클릭 하 고 **생성** 를 자동으로 공유 암호를 생성 합니다. NPS 서버와 통신할 수 있도록 NAS에서 생성 된 공유 구성에 대 한 암호를 저장 합니다.
7. **새 RADIUS 클라이언트**에서 **추가 옵션**EAP와 PEAP 이외의 인증 방법을 사용 하는 모든 사용자 Nas 지원 메시지 인증 특성을 활용 하는 경우를 선택 하는 경우, **액세스 요청 메시지 메시지 인증자 특성 있어야**합니다.
8. 클릭 **확인**합니다. 사용자 Nas RADIUS 클라이언트 NPS 서버에서 구성 된 목록에 표시 됩니다.

자세한 내용은 참조 [RADIUS 클라이언트](nps-radius-clients.md)합니다.

NPS에 대 한 자세한 내용은 참조 [네트워크 NPS 정책 서버 ()](nps-top.md)합니다.