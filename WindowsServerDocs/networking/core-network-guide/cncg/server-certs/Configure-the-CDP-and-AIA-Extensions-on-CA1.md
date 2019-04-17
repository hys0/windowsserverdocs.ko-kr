---
title: CA1에 CDP 및 확장 프로그램 AIA 구성
description: 이 항목은 802.1 X 유선 및 무선 배포에 대 한 배포 서버 인증서 가이드
manager: brianlic
ms.topic: article
ms.assetid: f77a3989-9f92-41ef-92a8-031651dd73a8
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 80f6d68816a58b2ac30010e0917ce0f816a30234
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="configure-the-cdp-and-aia-extensions-on-ca1"></a>CA1에 CDP 및 확장 프로그램 AIA 구성

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 절차 CA1에는 인증서 목록 CRL (해지) 지점 CDP (배포) 및 정보 AIA 기관 액세스 () 설정을 구성할 수 사용할 수 있습니다.  
  
이 절차를 수행 하려면 관리자 도메인의 회원 이어야 합니다.  
  
#### <a name="to-configure-the-cdp-and-aia-extensions-on-ca1"></a>확장 CDP 및 AIA CA1에서 구성 하려면  
  
1.  서버 관리자 클릭 **도구** 차례로 클릭 하 고 **인증 기관**합니다.  
  
2.  인증 기관 콘솔 트리에서 마우스 오른쪽 단추로 클릭 **corp-CA1-캐나다**을 차례로 클릭 하 고 **속성**합니다.  
  
    > [!NOTE]  
    > CA1 컴퓨터 이름을 하지 않은 경우 여기서에서 다른은 도메인 이름 기관 이름은 다양 합니다. 캘리포니아 이름은 형식에서 *도메인*-*CAComputerName*-캐나다 합니다.  
  
3.  클릭는 **확장** 탭 되도록 **확장을 선택** 로 설정 되어 **CRL 지점 CDP (배포)**의 사용자 (CRL), 다음을 수행 합니다.  
  
    1.  항목 선택 `file:\/\/\\\\<ServerDNSName>\/CertEnroll\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`을 차례로 클릭 하 고 **제거**합니다. **제거 확인**, 클릭 **예**합니다.  
  
    2.  항목 선택 `http:\/\/<ServerDNSName>\/CertEnroll\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`을 차례로 클릭 하 고 **제거**합니다. **제거 확인**, 클릭 **예**합니다.  
  
    3.  경로으로 시작 되는 항목 선택 `ldap:\/\/CN\=<CATruncatedName><CRLNameSuffix>,CN\=<ServerShortName>`을 차례로 클릭 하 고 **제거**합니다. **제거 확인**, 클릭 **예**합니다.  
  
4.  **사용자는 인증서 CRL (해지 목록)을 얻을 수 있는 위치를 지정**, 클릭 **추가**합니다. **위치 추가** 대화 상자를 엽니다.  
  
5.  **위치 추가**에 **위치**, 입력 `http:\/\/pki.corp.contoso.com\/pki\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`을 차례로 클릭 하 고 **확인**합니다. 캘리포니아 속성 대화 상자 돌아갑니다.  
  
6.  에 **확장** 탭에서 다음 확인란을 선택 합니다.  
  
    -   **Crl에 포함 됩니다. 클라이언트를 사용 하 여이 델타 CRL 위치 찾기**  
  
    -   **CDP 확장 발급 된 인증서의에 포함**  
  
7.  **사용자는 인증서 CRL (해지 목록)을 얻을 수 있는 위치를 지정**, 클릭 **추가**합니다. **위치 추가** 대화 상자를 엽니다.  
  
8.  **위치 추가**에 **위치**, 입력 `file:\/\/\\\\pki.corp.contoso.com\/pki\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`을 차례로 클릭 하 고 **확인**합니다. 캘리포니아 속성 대화 상자 돌아갑니다.  
  
9. 에 **확장** 탭에서 다음 확인란을 선택 합니다.  
  
    -   **Crl이이 위치에 게시**  
  
    -   **델타 Crl이이 위치에 게시**  
  
10. 변경 **확장을 선택** 에 **기관 액세스 AIA (정보)**의 **사용자는 인증서 CRL (해지 목록)을 얻을 수 있는 위치를 지정**에서 다음을 수행 합니다.  
  
    1.  경로으로 시작 되는 항목 선택 `ldap:\/\/CN\=<CATruncatedName>,CN\=AIA,CN\=Public Key Services`을 차례로 클릭 하 고 **제거**합니다. **제거 확인**, 클릭 **예**합니다.  
  
    2.  항목 선택 `http:\/\/<ServerDNSName>\/CertEnroll\/<ServerDNSName>\_<CaName><CertificateName>.crt`을 차례로 클릭 하 고 **제거**합니다. **제거 확인**, 클릭 **예**합니다.  
  
    3.  항목 선택 `file:\/\/\\\\<ServerDNSName>\/CertEnroll\/<ServerDNSName>\_<CaName><CertificateName>.crt`을 차례로 클릭 하 고 **제거**합니다. **제거 확인**, 클릭 **예**합니다.  
  
11. **사용자는 인증서 CRL (해지 목록)을 얻을 수 있는 위치를 지정**, 클릭 **추가**합니다. **위치 추가** 대화 상자를 엽니다.  
  
12. **위치 추가**에 **위치**, 입력 `http:\/\/pki.corp.contoso.com\/pki\/<ServerDNSName>\_<CaName><CertificateName>.crt`을 차례로 클릭 하 고 **확인**합니다. 캘리포니아 속성 대화 상자 돌아갑니다.  
  
13. 에 **확장** 탭을 선택 하 고 **발급 된 인증서 AIA에 포함**합니다.  
  
14. **위치 추가**에 **위치**, 입력 `file:\/\/\\\\pki.corp.contoso.com\/pki\/<ServerDNSName>\_<CaName><CertificateName>.crt`을 차례로 클릭 하 고 **확인**합니다. 캘리포니아 속성 대화 상자 돌아갑니다.  
  
    > [!IMPORTANT]  
    > 되도록 **AIA 확장 발급 된 인증서의에 포함** 선택 하지 않으면 합니다.  
  
15. 를 Active Directory 인증서 서비스를 다시 시작 하 라는 메시지가 나타나면 클릭 **아니요**합니다. 나중에 서비스를 다시 시작 됩니다.  
  


