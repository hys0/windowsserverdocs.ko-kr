---
title: PEAP 및 EAP 요구 사항에 대한 인증서 템플릿 구성
description: 이 항목에서는 인증서를 사용 하 여 네트워크 정책 서버와 Windows Server 2016에서 원격 액세스에 대 한 정보를 제공 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 2af0a1df-5c44-496b-ab11-5bc340dc96f0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 41f6f88705fa3d58be695fd825d960e7df21cd24
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885884"
---
# <a name="configure-certificate-templates-for-peap-and-eap-requirements"></a>PEAP 및 EAP 요구 사항에 대한 인증서 템플릿 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

Extensible Authentication Protocol을 사용 하 여 네트워크 액세스 인증에 사용 되는 모든 인증서\-Transport Layer Security \(EAP\-TLS\), Protected Extensible Authentication Protocol\- 전송 계층 보안 \(PEAP\-TLS\), 및 PEAP\-Microsoft Challenge Handshake Authentication Protocol 버전 2 \(MS\-CHAP v2\) 해야 X.509 인증서에 대 한 요구 사항을 충족 하 고 Secure Socket Layer/Transport 수준 보안 (SSL/TLS)를 사용 하는 연결에 대해 작동 합니다. 클라이언트와 서버 인증서에는 추가 요구 사항이 있습니다.

>[!IMPORTANT]
>이 항목에서는 인증서 템플릿을 구성 하기 위한 지침을 제공 합니다. 이러한 지침을 사용 하려면 필요한가 사용자 고유의 공개 키 인프라를 배포한 \(PKI\) Active Directory 인증서 서비스를 사용 하 여 \(AD CS\)합니다.

## <a name="minimum-server-certificate-requirements"></a>최소 서버 인증서 요구 사항

Peap\-MS\-CHAP v2, PEAP\-TLS 또는 EAP\-인증 방법으로 TLS를 NPS에는 최소 서버 인증서 요구 사항을 충족 하는 서버 인증서를 사용 해야 합니다. 

서버 인증서를 사용 하 여 유효성을 검사 하는 클라이언트 컴퓨터를 구성할 수 있습니다 합니다 **서버 인증서 유효성 검사** 클라이언트 컴퓨터 또는 그룹 정책 옵션입니다. 

서버 인증서는 다음 요구 사항을 충족 하는 경우 서버 인증 시도 허용 하는 클라이언트 컴퓨터:

- 값을 포함 하는 주체 이름입니다. 네트워크 정책 (NPS 서버) 빈 주체 이름을 가진 실행 중인 서버에 인증서를 발급 하는 경우 인증서에 NPS 인증에 사용할 수 없는 경우 주체 이름을 가진 인증서 템플릿을 구성:

    1. 인증서 템플릿을 엽니다.
    2. 세부 정보 창에서 변경 하 고 클릭 하려는 인증서 템플릿을 마우스 오른쪽 단추로 클릭 **속성** 합니다.
    3. 클릭 합니다 **주체 이름** 탭을 클릭 한 다음 **이 Active Directory 정보에서 구축**합니다.
    4. **주체 이름 형식**, 이외의 값을 선택 **None**합니다.

- 컴퓨터 인증서 서버 체인을 신뢰할 수 있는 루트 CA (인증 기관) 및 원격 액세스 정책 또는 네트워크 정책에 지정 된 CryptoAPI에서 수행 되는 검사가 실패 하지 않습니다.

- NPS 또는 VPN 서버의 컴퓨터 인증서는 서버 인증 용도로 확장 키 사용 현황 EKU (확장)를 사용 하 여 구성 됩니다. (서버 인증에 대 한 개체 식별자 1.3.6.1.5.5.7.3.1 됩니다.)

- 필요한 암호화 설정을 사용 하 여 서버 인증서를 구성 합니다.

    1. 인증서 템플릿을 엽니다.
    2. 세부 정보 창에서 변경 하 고 클릭 하려는 인증서 템플릿을 마우스 오른쪽 단추로 클릭 **속성**합니다.
    3. 클릭 합니다 **암호화** 탭 하 고 다음을 구성 해야 합니다.
       - **공급자 범주:** 키 저장소 공급자
       - **알고리즘 이름:** RSA
       - **공급자:** Microsoft 플랫폼 암호화 공급자
       - **최소 키 크기:** 2048
       - **해시 알고리즘:** SHA2
    4. **다음**을 클릭합니다.

- 주체 대체 이름 (SubjectAltName) 확장을 사용 하는 경우 서버의 DNS 이름을 포함 해야 합니다. 등록 서버의 도메인 이름 시스템 (DNS) 이름으로 인증서 템플릿을 구성: 

    1. 인증서 템플릿을 엽니다.
    2. 세부 정보 창에서 변경 하 고 클릭 하려는 인증서 템플릿을 마우스 오른쪽 단추로 클릭 **속성** 합니다.
    3. 클릭 합니다 **주체 이름** 탭을 클릭 한 다음 **이 Active Directory 정보에서 구축**합니다.
    4. **대체 주체 이름에이 정보 포함**를 선택 **DNS 이름**합니다.

PEAP 및 EAP TLS를 사용 하는 경우 NPSs 컴퓨터 인증서 저장소는 다음과 같은 예외를 사용 하 여 설치 된 모든 인증서의 목록을 표시:

- 서버 인증 용도로 EKU 확장에 포함 되지 않은 인증서 표시 되지 않습니다.

- 인증서 주체 이름을 포함 하지 않는 표시 되지 않습니다.

- 레지스트리 기반 및 스마트 카드 로그온 인증서 표시 되지 않습니다.

자세한 내용은 [802.1 X 유선 및 무선 배포에 대 한 서버 인증서 배포](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments)합니다.

## <a name="minimum-client-certificate-requirements"></a>최소 클라이언트 인증서 요구 사항

EAP-TLS, PEAP TLS를 사용 하 여 서버 인증서는 다음 요구 사항을 충족 하는 경우 클라이언트 인증 시도 허용 합니다.

- 클라이언트 인증서는 엔터프라이즈 CA에서 발급 한 또는 Active Directory Domain Services에서 사용자 또는 컴퓨터 계정에 매핑된 \(AD DS\)합니다.

- 신뢰할 수 있는 루트 CA에 클라이언트 연결에서 사용자 또는 컴퓨터 인증서 EKU 확장에 대 한 클라이언트 인증 용도의 \(클라이언트 인증에 대 한 개체 식별자는 1.3.6.1.5.5.7.3.2\), 모두 실패 합니다 CryptoAPI에 의해 수행 되는 및 원격 액세스 정책 또는 네트워크 정책 및 NPS 네트워크 정책을에 지정 된 인증서 개체 식별자 확인에 지정 된 확인 합니다.

- 802.1x 클라이언트 암호로 보호 된 인증서 나 스마트 카드 로그온 된 레지스트리 기반 인증서를 사용 하지 않습니다.

- 사용자 인증서의 주체 대체 이름 \(SubjectAltName\) 인증서에 대 한 확장 포함 사용자 계정 이름 \(UPN\)합니다. UPN을 인증서 템플릿에서 구성:

    1. 인증서 템플릿을 엽니다.
    2. 세부 정보 창에서 변경 하 고 클릭 하려는 인증서 템플릿을 마우스 오른쪽 단추로 클릭 **속성**합니다.
    3. 클릭 합니다 **주체 이름** 탭을 클릭 한 다음 **이 Active Directory 정보에서 구축**합니다.
    4. **대체 주체 이름에이 정보 포함**를 선택 **사용자 계정 이름 \(UPN\)** 합니다.

- 컴퓨터 인증서의 경우 주체 대체 이름 \(SubjectAltName\) 인증서에 확장 정규화 된 도메인 이름이 들어 있어야 \(FQDN\) 합니다 라고도하는클라이언트의 *DNS 이름*합니다. 이 이름을 인증서 템플릿에서 구성:

    1. 인증서 템플릿을 엽니다.
    2. 세부 정보 창에서 변경 하 고 클릭 하려는 인증서 템플릿을 마우스 오른쪽 단추로 클릭 **속성**합니다.
    3. 클릭 합니다 **주체 이름** 탭을 클릭 한 다음 **이 Active Directory 정보에서 구축**합니다.
    4. **대체 주체 이름에이 정보 포함**를 선택 **DNS 이름**합니다.

Peap\-TLS 및 EAP\-TLS 클라이언트는 인증서 스냅인 다음 예외를 사용 하 여의 설치 된 모든 인증서 목록의 표시 합니다.

- 무선 클라이언트에 레지스트리를 기반으로 표시 되지 않습니다 및 스마트 카드 로그온 인증서입니다. 

- 무선 클라이언트와 VPN 클라이언트는 암호로 보호 된 인증서를 표시 하지 않습니다. 

- 클라이언트 인증 용도의 EKU 확장에 포함 되지 않은 인증서 표시 되지 않습니다.


NPS에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 (NPS 서버)](nps-top.md)합니다.
