---
title: RADIUS 클라이언트 구성
description: 이 항목에서는 Windows Server 2016에서 네트워크 정책 서버에 대 한 RADIUS 클라이언트를 구성 하는 방법에 대해 설명 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: cde37849-ce79-4c26-aa14-cd0ef31cae18
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6870029e02ae91b1ef5bf4d4302ac2bed2e27d84
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405294"
---
# <a name="configure-radius-clients"></a>RADIUS 클라이언트 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 NPS에서 네트워크 액세스 서버를 RADIUS 클라이언트로 구성할 수 있습니다.

네트워크에\) 새 네트워크 액세스 서버 \(VPN 서버, 무선 액세스 지점, 인증 스위치 또는 전화 접속 서버를 추가 하는 경우 NPS에서 서버를 RADIUS 클라이언트로 추가한 다음 NPS와 통신 하도록 RADIUS 클라이언트를 구성 해야 합니다.

>[!IMPORTANT]
>클라이언트 컴퓨터 및 장치 (예: 랩톱 컴퓨터, 태블릿, 휴대폰 및 클라이언트 운영 체제를 실행 하는 다른 컴퓨터)는 RADIUS 클라이언트가 아닙니다. RADIUS 클라이언트는 radius 프로토콜을 사용 하 여 NPS\) 서버 \(네트워크 정책 서버와 같은 RADIUS 서버와 통신 하기 때문에 무선 액세스 지점과 802.1 X 가능 스위치, VPN (가상 사설망) 서버 및 전화 접속 서버와 같은 네트워크 액세스 서버입니다.

Nps가 NPS 프록시에 구성 된 원격 RADIUS 서버 그룹의 구성원 인 경우에도이 단계가 필요 합니다. 이 경우 NPS 프록시에서이 작업의 단계를 수행 하는 것 외에도 다음 작업을 수행 해야 합니다.

- NPS 프록시에서 NPS를 포함 하는 원격 RADIUS 서버 그룹을 구성 합니다.
- 원격 NPS에서 RADIUS 클라이언트로 NPS 프록시를 구성 합니다.

이 항목의 절차를 수행 하려면 네트워크에 물리적으로 설치 된 하나 이상의 네트워크 액세스 서버 \(VPN 서버, 무선 액세스 지점, 인증 스위치 또는 전화 접속 서버\) 또는 NPS 프록시를 사용 해야 합니다.

## <a name="configure-the-network-access-server"></a>네트워크 액세스 서버 구성

NPS에서 사용할 네트워크 액세스 서버를 구성 하려면 다음 절차를 따르십시오. RADIUS 클라이언트로 Nas (네트워크 액세스 서버)를 배포 하는 경우 Nas가 클라이언트로 구성 된 NPSs와 통신 하도록 클라이언트를 구성 해야 합니다.

이 절차에서는 Nas를 구성 하는 데 사용 해야 하는 설정에 대 한 일반적인 지침을 제공 합니다. 네트워크에 배포 하는 장치를 구성 하는 방법에 대 한 구체적인 지침은 NAS 제품 설명서를 참조 하십시오.

### <a name="to-configure-the-network-access-server"></a>네트워크 액세스 서버를 구성 하려면

1. NAS의 **radius 설정**에서 Udp (사용자 데이터 그램 프로토콜) 포트 **1812** 에 대 한 **radius 인증** 및 udp 포트 **1813**의 **radius 계정** 을 선택 합니다.
2. **인증 서버** 또는 **RADIUS 서버**에서 NAS 요구 사항에 따라 IP 주소 또는 FQDN (정규화 된 도메인 이름)을 기준으로 NPS를 지정 합니다. 
3. **비밀** 또는 **공유 암호**에 강력한 암호를 입력 합니다. NPS를 NPS에서 RADIUS 클라이언트로 구성 하는 경우 동일한 암호를 사용 하므로 암호를 잊지 마십시오.
4. PEAP 또는 EAP를 인증 방법으로 사용 하는 경우 EAP 인증을 사용 하도록 NAS를 구성 합니다.
5. 무선 액세스 지점을 구성 하는 경우 **ssid**에서 네트워크 이름으로 사용 되는 영숫자 문자열인 ssid\)\(서비스 집합 식별자를 지정 합니다. 이 이름은 무선 클라이언트에 대 한 액세스 지점에 의해 브로드캐스트 되며, 무선 충실도 \(Wi-fi\) 핫스팟에 사용자에 게 표시 됩니다.
6. 무선 액세스 지점을 구성 하는 경우 **802.1 x 및 WPA**에서 PEAP-CHAP V2, PEAP-TLS 또는 eap-tls를 배포 하려는 경우 **IEEE 802.1 x 인증** 을 사용 하도록 설정 합니다.

## <a name="add-the-network-access-server-as-a-radius-client-in-nps"></a>NPS에서 RADIUS 클라이언트로 네트워크 액세스 서버 추가

NPS에서 RADIUS 클라이언트로 네트워크 액세스 서버를 추가 하려면 다음 절차를 따르십시오. 이 절차에 따라 NPS 콘솔을 사용 하 여 NAS를 RADIUS 클라이언트로 구성할 수 있습니다.

이 절차를 완료 하려면의 구성원 이어야는 **관리자** 그룹입니다.

### <a name="to-add-a-network-access-server-as-a-radius-client-in-nps"></a>NPS에서 RADIUS 클라이언트로 네트워크 액세스 서버를 추가 하려면

1. NPS의 서버 관리자에서 **도구**를 클릭 한 다음 **네트워크 정책 서버**를 클릭 합니다. NPS 콘솔이 열립니다.
2. NPS 콘솔에서 **RADIUS 클라이언트 및 서버**를 두 번 클릭 합니다. **Radius 클라이언트**를 마우스 오른쪽 단추로 클릭 한 다음 **새 radius 클라이언트**를 클릭 합니다. 
3. **새 RADIUS 클라이언트**, 있는지는 **이 RADIUS 클라이언트를 사용 하도록 설정** 확인란을 선택 합니다.
4. **새 RADIUS 클라이언트**의 **이름**에 NAS에 대 한 표시 이름을 입력 합니다. **주소 (ip 또는 DNS)** 에 NAS IP 주소 또는 FQDN (정규화 된 도메인 이름)을 입력 합니다. FQDN을 입력 하는 경우 이름이 올바르고 올바른 IP 주소에 매핑되는지 확인 하려면 **확인** 을 클릭 합니다. 
5. **새 RADIUS 클라이언트**의 **공급 업체**에서 NAS 제조업체 이름을 지정 합니다. NAS 제조업체의 이름을 정확히 알지 못하는 경우 선택 **RADIUS 표준**합니다.
6. **새 RADIUS 클라이언트**의 **공유 암호**에서 다음 중 하나를 수행 합니다.
    - **수동** 이 선택 되어 있는지 확인 한 다음 **공유 암호**에서 NAS에도 입력 된 강력한 암호를 입력 합니다. 공유 암호를 다시 입력 **공유 암호 확인**합니다.
    - **생성**을 선택 하 고 **생성** 을 클릭 하 여 공유 암호를 자동으로 생성 합니다. NPS와 통신할 수 있도록 NAS에 구성 하기 위해 생성 된 공유 암호를 저장 합니다.
7. **새 RADIUS 클라이언트**의 **추가 옵션**에서 EAP 및 PEAP 이외의 다른 인증 방법을 사용 하는 경우 NAS에서 메시지 인증자 특성 사용을 지 원하는 경우 **액세스 요청 메시지에 메시지 인증자 특성이 포함 되어야 합니다**.를 선택 합니다.
8. **확인**을 클릭합니다. NAS가 NPS에 구성 된 RADIUS 클라이언트 목록에 표시 됩니다.

## <a name="configure-radius-clients-by-ip-address-range-in-windows-server-2016-datacenter"></a>Windows Server 2016 데이터 센터의 IP 주소 범위를 기준으로 RADIUS 클라이언트 구성

Windows Server 2016 Datacenter를 실행 하는 경우 IP 주소 범위를 통해 NPS에서 RADIUS 클라이언트를 구성할 수 있습니다. 이렇게 하면 각 RADIUS 클라이언트를 개별적으로 추가 하는 대신 한 번에 많은 수의 RADIUS 클라이언트 (예: 무선 액세스 지점)를 NPS 콘솔에 추가할 수 있습니다.

Windows Server 2016 Standard에서 NPS를 실행 하는 경우 IP 주소 범위를 기준으로 RADIUS 클라이언트를 구성할 수 없습니다.

이 절차를 사용 하 여 Nas (네트워크 액세스 서버) 그룹을 동일한 IP 주소 범위의 IP 주소로 모두 구성 된 RADIUS 클라이언트로 추가 합니다.

범위의 모든 RADIUS 클라이언트는 동일한 구성 및 공유 암호를 사용 해야 합니다.

이 절차를 완료 하려면의 구성원 이어야는 **관리자** 그룹입니다.

### <a name="to-set-up-radius-clients-by-ip-address-range"></a>IP 주소 범위를 기준으로 RADIUS 클라이언트를 설정 하려면

1. NPS의 서버 관리자에서 **도구**를 클릭 한 다음 **네트워크 정책 서버**를 클릭 합니다. NPS 콘솔이 열립니다.
2. NPS 콘솔에서 **RADIUS 클라이언트 및 서버**를 두 번 클릭 합니다. **Radius 클라이언트**를 마우스 오른쪽 단추로 클릭 한 다음 **새 radius 클라이언트**를 클릭 합니다.
3. **새 RADIUS 클라이언트**의 **이름**에 nas의 컬렉션에 대 한 표시 이름을 입력 합니다.
4. **주소 \(ip 또는 DNS\)** 에서 클래스 없는 도메인 간 라우팅 \(CIDR\) 표기법을 사용 하 여 RADIUS 클라이언트의 IP 주소 범위를 입력 합니다. 예를 들어 Nas에 대 한 IP 주소 범위가 10.10.0.0 인 경우 **10.10.0.0/16**을 입력 합니다.
5. **새 RADIUS 클라이언트**의 **공급 업체**에서 NAS 제조업체 이름을 지정 합니다. NAS 제조업체의 이름을 정확히 알지 못하는 경우 선택 **RADIUS 표준**합니다.
6. **새 RADIUS 클라이언트**의 **공유 암호**에서 다음 중 하나를 수행 합니다.
    - **수동** 이 선택 되어 있는지 확인 한 다음 **공유 암호**에서 NAS에도 입력 된 강력한 암호를 입력 합니다. 공유 암호를 다시 입력 **공유 암호 확인**합니다.
    - **생성**을 선택 하 고 **생성** 을 클릭 하 여 공유 암호를 자동으로 생성 합니다. NPS와 통신할 수 있도록 NAS에 구성 하기 위해 생성 된 공유 암호를 저장 합니다.
7. **새 RADIUS 클라이언트**의 **추가 옵션**에서 EAP 및 PEAP 이외의 다른 인증 방법을 사용 하 고 모든 nas에서 메시지 인증자 특성 사용을 지 원하는 경우 **액세스 요청 메시지에 메시지 인증자 특성이 포함 되어야 합니다**.를 선택 합니다.
8. **확인**을 클릭합니다. Nas NPS에 구성 된 RADIUS 클라이언트 목록에 표시 됩니다.

자세한 내용은 [RADIUS 클라이언트](nps-radius-clients.md)를 참조 하세요.

NPS에 대 한 자세한 내용은 [nps (네트워크 정책 서버)](nps-top.md)를 참조 하세요.