---
title: 인증서 템플릿을 PEAP 및 EAP 요구 사항에 대 한 구성
description: 이 항목에서는 네트워크 정책 서버와 Windows Server 2016에 대 한 원격 액세스 인증서 사용에 대 한 정보를 제공 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 2af0a1df-5c44-496b-ab11-5bc340dc96f0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e597a65982aeead907c9a41f17f1785a0bf81016
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="configure-certificate-templates-for-peap-and-eap-requirements"></a>인증서 템플릿을 PEAP 및 EAP 요구 사항에 대 한 구성

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

네트워크 액세스 인증 Extensible 인증 Protocol\ Transport Layer 보안 \(EAP\-TLS\), 보호 Extensible 인증 Protocol\ Transport Layer 보안 \(PEAP\-TLS\) PEAP\ Microsoft Challenge Handshake 인증 프로토콜 버전 2와에 사용 되는 모든 인증서 \ (MS\ 기능을 제공 v2\) Secure Socket Transport Layer/수준 보안 (SSL/TLS)를 사용 하는 연결에 대 한 작업 및 X.509 인증서의 요구 사항을 만족 해야 합니다. 클라이언트 및 서버 인증서 추가 요구 사항이 있습니다.

>[!IMPORTANT]
>이 항목에서는 인증서 템플릿 구성에 대해 설명 합니다. 다음 절차에 필요는 Active Directory 인증서 서비스와 직접 공개 키 인프라 \(PKI\) 배포한 \ (AD CS \).

## <a name="minimum-server-certificate-requirements"></a>최소 서버 인증서 요구 사항

PEAP\ 기능 MS\ 기능을 제공 v2, PEAP\ TLS 또는 인증 방법으로 EAP\ TLS NPS 서버 최소 서버 인증서 요구 사항을 충족 하는 서버 인증서를 사용 해야 합니다. 

클라이언트 컴퓨터를 사용 하 여 서버 인증서를 확인 하도록 구성할 수 있습니다는 **유효성 검사 서버 인증서** 옵션 클라이언트 컴퓨터에서 또는 그룹 정책에서 합니다. 

클라이언트 컴퓨터 서버 인증서 다음 요구 사항을 충족 하는 경우 서버 인증 시도를 받습니다.

- 주체 이름 값을 포함 합니다. 네트워크 NPS 정책 서버 () 빈 주제 이름이 지정 된 실행 하는 서버에 인증서를 실행 하는 경우 인증서 NPS 서버 인증을 제공 되지 않습니다. 구성 하려면 인증서 템플릿을 주체 이름을 사용:

    1. 인증서 템플릿을 엽니다.
    2. 세부 정보 창에서 마우스 오른쪽 단추로 클릭을 바꾸고 클릭 한 다음 원하는 인증서 템플릿을 **속성** 합니다.
    3. 클릭는 **주체 이름** 탭을 클릭 한 다음 **Active Directory이 정보로 작성할**합니다.
    4. **주체 이름 형식**, 값 이외의 선택 **없음**합니다.

- 컴퓨터 인증서 통과 원격 액세스 정책 또는 네트워크 정책에 지정 된 CryptoAPI에서 수행 하는 검사 중 하나를 신뢰할 수 있는 루트 인증 기관 (캐나다), 서버 연결 합니다.

- NPS 서버 또는 VPN 서버에 대 한 컴퓨터 인증서가 서버 인증 용도로 확장 확장 키 (EKU 사용)에서 구성 되어 있습니다. (서버 인증을 위한 개체 식별자 1.3.6.1.5.5.7.3.1입니다.)

- 서버 인증서가 필요한 알고리즘 값으로 구성 되어 **RSA**합니다. 필요한 암호화 설정을 구성 하려면

    1. 인증서 템플릿을 엽니다.
    2. 세부 정보 창에서 마우스 오른쪽 단추로 클릭을 바꾸고 클릭 한 다음 원하는 인증서 템플릿을 **속성**합니다.
    3. 클릭 하 고 **암호화** 탭 합니다. **알고리즘 이름**, 클릭 **RSA** 합니다. 되도록 **키 최소 크기** 로 설정 되어 **2048**합니다.

- 주체 대체 이름 (SubjectAltName) 확장을 사용 하는 경우 DNS 서버 이름을 포함 해야 합니다. 인증서 템플릿을 등록 서버 시스템 DNS (도메인 이름) 이름으로 구성 방법: 

    1. 인증서 템플릿을 엽니다.
    2. 세부 정보 창에서 마우스 오른쪽 단추로 클릭을 바꾸고 클릭 한 다음 원하는 인증서 템플릿을 **속성** 합니다.
    3. 클릭는 **주체 이름** 탭을 클릭 한 다음 **Active Directory이 정보로 작성할**합니다.
    4. **대체 주체 이름에이 정보가 포함**선택 **DNS 이름**합니다.

EAP-TLS 및 PEAP을 사용 하는 경우 NPS 서버 컴퓨터 인증서 저장소 구성원과에서 설치 된 모든 인증서 목록이 표시 다음과 같습니다.

- 인증서가 서버 인증 목적이 EKU 확장에 포함 되지 않은 표시 되지 않습니다.

- 주체 이름을 포함 되어 있지 않은 인증서 표시 되지 않습니다.

- 레지스트리 기반 스마트 카드 로그온 인증서 표시 되지 않습니다.

자세한 내용은 참조 [802.1 X 유선 및 무선 배포에 대 한 서버 인증서 배포](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments)합니다.

## <a name="minimum-client-certificate-requirements"></a>최소 클라이언트 인증서 요구 사항

EAP-TLS 또는 PEAP-TLS 서버 클라이언트 인증 시도 인증서 다음 요구 사항을 충족 하는 경우를 허용 합니다.

- 클라이언트 인증서 엔터프라이즈 캘리포니아에서 발급 한 또는 Active Directory Domain Services에서 사용자 또는 컴퓨터 계정에 매핑됩니다 \ (AD DS \).

- 신뢰할 수 있는 루트 캐나다 클라이언트 체인에서 사용자 또는 컴퓨터 인증서 EKU 확장에서 클라이언트 인증 목적을 포함 \ (클라이언트 인증 개체 식별자가 1.3.6.1.5.5.7.3.2\), 검사 CryptoAPI 하 여 수행 하 고 원격 액세스 정책 또는 네트워크 정책에 지정 된 지도 NPS 네트워크 정책에 지정 된 인증서 개체 식별자 검사에 실패 합니다.

- 802.1 X 클라이언트 스마트 카드 로그온 있는 레지스트리를 기반으로 하는 인증서 나 암호로 보호 된 인증서를 사용 하지 않습니다.

- 인증서에 제목을 대체 이름 \(SubjectAltName\) 확장 사용자 인증서에 대 한 사용자 포함 \(UPN\) 이름을 지정 합니다. 구성 하려면 UPN 인증서 템플릿에서:

    1. 인증서 템플릿을 엽니다.
    2. 세부 정보 창에서 마우스 오른쪽 단추로 클릭을 바꾸고 클릭 한 다음 원하는 인증서 템플릿을 **속성**합니다.
    3. 클릭는 **주체 이름** 탭을 클릭 한 다음 **Active Directory이 정보로 작성할**합니다.
    4. **대체 주체 이름에이 정보가 포함**선택 **사용자 계정 \(UPN\) 이름을**합니다.

- 컴퓨터 인증서 인증서의 제목 대체 이름 \(SubjectAltName\) 확장 정식된 도메인 있어야 \(FQDN\) 라고도 하는 클라이언트의 이름을 *DNS 이름*합니다. 이 이름을 인증서 템플릿을 구성 하려면:

    1. 인증서 템플릿을 엽니다.
    2. 세부 정보 창에서 마우스 오른쪽 단추로 클릭을 바꾸고 클릭 한 다음 원하는 인증서 템플릿을 **속성**합니다.
    3. 클릭는 **주체 이름** 탭을 클릭 한 다음 **Active Directory이 정보로 작성할**합니다.
    4. **대체 주체 이름에이 정보가 포함**선택 **DNS 이름**합니다.

PEAP\ TLS와 EAP\ TLS 클라이언트 인증서 스냅인 구성원과 설치 된 모든 인증서 목록을 표시 합니다.

- 무선 클라이언트 레지스트리를 기반으로 표시 되지 않는 인증서 스마트 카드 로그온 합니다. 

- 무선 클라이언트 및 VPN 클라이언트 암호로 보호 된 인증서를 표시 하지 않습니다. 

- 인증서에 EKU 확장 클라이언트 인증 목적을 포함 되지 않은 표시 되지 않습니다.


NPS에 대 한 자세한 내용은 참조 [네트워크 NPS 정책 서버 ()](nps-top.md)합니다.
