---
title: 인증서 NPS와 함께 사용 관리
description: 이 항목의 Windows Server 2016 네트워크 정책 서버 서버의 인증서 사용에 대 한 정보를 제공 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 204a4ef4-9d78-4a62-9940-43cc0e1c39d0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2044cf30cc90c1673e05a1948ac9196d05940d1f
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="manage-certificates-used-with-nps"></a>인증서 NPS와 함께 사용 관리

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

Extensible 인증 Protocol\ Transport Layer 보안 \(EAP\-TLS\), 보호 Extensible 인증 Protocol\ Transport Layer 보안 \(PEAP\-TLS\) PEAP\ Microsoft Challenge Handshake 인증 프로토콜 버전 2 등 가지 옵션이 인증 방법, 배포한 \ (MS\ 기능을 제공 v2\) 서버의 인증서 모든 NPS 서버에 등록 해야 합니다. 서버 인증서 수행 해야합니다.

- 에 설명 된 대로 최소 서버 인증서 요구 사항을 충족 [구성 인증서 PEAP 및 템플릿을 EAP 요구 사항](nps-manage-cert-requirements.md)

- 인증 기관에서 발급 되어야 \(CA\) 클라이언트 컴퓨터에서 신뢰할 수 있습니다. 캘리포니아를 신뢰할 수 있는 때 인증서가 신뢰할 수 있는 인증 기관을 인증서 저장소 현재 사용자 및 로컬 컴퓨터에 대 한에 합니다.

다음 지침 지원 NPS 서버의 인증서를 신뢰할 수 있는 루트 캘리포니아 Verisign와 같은 제 3 자 캐나다 되었거나 공개 키 인프라에 대 한 배포 캘리포니아 배포에서 관리 Active Directory 인증서 서비스를 사용 하 여 \(PKI\) \ (AD CS \).

## <a name="change-the-cached-tls-handle-expiry"></a>캐시 된 TLS 핸들 만료 변경

초기 인증 프로세스 EAP\ TLS, PEAP\ TLS 및 v2 PEAP\ 기능 MS\ 기능을 제공 하는 동안 NPS 서버 연결 클라이언트 TLS 연결 속성의 일부를 캐시합니다. 또한 클라이언트 NPS 서버 TLS 연결 속성의 일부를 캐시합니다.

이러한 TLS 연결 속성 각 개별 컬렉션 TLS 핸들을 라고 합니다.

클라이언트 컴퓨터 NPS 서버 수 많은 클라이언트 컴퓨터의 TLS 핸들을 캐시 하는 동안 TLS 핸들 여러 인증자에 대 한 캐시 수 있습니다.

클라이언트 및 서버에 있는 캐시 된 TLS 핸들을 보다 빠르게 수행 되기를 다시 인증 프로세스를 허용 합니다. 예를 들어, NPS 서버가 무선 컴퓨터를 다시 인증할 NPS 서버 무선 클라이언트 TLS 핸들을 확인할 수 있습니다와 빠르게 클라이언트 연결이 다시 연결 되어 있는지 확인할 수 있습니다. 전체 인증은 수행 하지 않고 NPS 서버에 연결 권한을 부여 합니다.

따라서 클라이언트 NPS 서버에 대 한 TLS 핸들을 검사 하 여, 확인 되는 다시 연결 하 고 서버 인증을 수행 하지 않아도 됩니다.

Windows 10 및 Windows Server 2016 실행 하는 컴퓨터의 기본 TLS 핸들 만료 10 시간입니다.

경우에 따라 높이기 또는 낮추기 TLS 핸들 만료 시간 수도 있습니다.

예를 들어, 관리자가 사용자의 인증서가 해지 장소와 인증서가 만료 경우에서 TLS 핸들 만료 시간을 줄일 좋습니다. 사용자가이 시나리오에서 여전히 NPS 서버 만료 되지 않은 캐시 된 TLS 핸들에 있는 경우는 네트워크에 연결할 수 있습니다. TLS 줄이기 핸들 만료 인증서 해지으로 이러한 사용자 다시 연결 하는 것을 방지 도움이 될 수 있습니다.

>[!NOTE]
>이 경우에 가장 좋은 방법은 Active directory, 사용자 계정을 사용 하지 않도록 설정 하거나 네트워크 정책에서 네트워크에 연결할 수 있는 권한이 부여 된 Active Directory 그룹에서 사용자 계정을 제거 하려면입니다. 그러나 모든 도메인 컨트롤러에 이러한 변경의 전파도 지연 될 수 있습니다, 복제 지연 때문입니다. 

## <a name="configure-the-tls-handle-expiry-time-on-client-computers"></a>클라이언트 컴퓨터에서 TLS 핸들 만료 시간이 구성

클라이언트 컴퓨터 NPS 서버 TLS 핸들을 캐시 하는 크기를 변경 하려면이 절차를 사용할 수 있습니다. 성공적으로 인증 NPS 서버, 한 후 클라이언트 컴퓨터 TLS 핸들 TLS 연결 속성 NPS 서버를 캐시 합니다. TLS 핸들에 10 시간 \(36,000,000 milliseconds\)의 기본 기간이합니다. 높이기 또는 다음 절차를 사용 하 여 TLS 핸들 만료 시간을 줄일 수 있습니다.

회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.

>[!IMPORTANT]
>클라이언트 컴퓨터 NPS 서버의이 절차를 수행 해야 합니다.

### <a name="to-configure-the-tls-handle-expiry-time-on-client-computers"></a>TLS 처리 클라이언트 컴퓨터에 만료 시간 구성 하려면

1. NPS 서버에서 레지스트리 편집기 열기

2. 레지스트리 키를 찾습니다 **HKEY\_LOCAL\_MACHINE\System\CurrentControlSet\Control\SecurityProviders\SCHANNEL**

3. 에 **편집** 메뉴를 클릭 **새로**을 차례로 클릭 하 고 **키**합니다.

4. 입력 **ClientCacheTime**, ENTER 키를 누릅니다.

5. 마우스 오른쪽 단추로 클릭 **ClientCacheTime**, 클릭 **새로**을 차례로 클릭 하 고 **DWORD (32 비트) 값**합니다.

6. 클라이언트 컴퓨터 NPS 서버 시도할 첫 번째 성공적으로 인증 후 NPS 서버 TLS 핸들을 캐시 하 않도록 밀리초에서 시간을 입력 합니다.

## <a name="configure-the-tls-handle-expiry-time-on-nps-servers"></a>NPS 서버의 TLS 핸들 만료 시간이 구성

이 절차를 사용 하 여 NPS 서버 클라이언트 컴퓨터의 TLS 핸들을 캐시 하는 시간을 변경할 수 있습니다. 액세스 클라이언트를 성공적으로 인증 후 NPS 서버 TLS 핸들 클라이언트 컴퓨터의 TLS 연결 속성을 캐시 합니다. TLS 핸들에 10 시간 \(36,000,000 milliseconds\)의 기본 기간이합니다. 높이기 또는 다음 절차를 사용 하 여 TLS 핸들 만료 시간을 줄일 수 있습니다.

회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.

>[!IMPORTANT]
>클라이언트 컴퓨터 NPS 서버의이 절차를 수행 해야 합니다.

### <a name="to-configure-the-tls-handle-expiry-time-on-nps-servers"></a>TLS 처리 NPS 서버에 만료 시간 구성 하려면

1. NPS 서버에서 레지스트리 편집기 열기

2. 레지스트리 키를 찾습니다 **HKEY\_LOCAL\_MACHINE\System\CurrentControlSet\Control\SecurityProviders\SCHANNEL**

3. 에 **편집** 메뉴를 클릭 **새로**을 차례로 클릭 하 고 **키**합니다.

4. 입력 **ServerCacheTime**, ENTER 키를 누릅니다.

5. 마우스 오른쪽 단추로 클릭 **ServerCacheTime**, 클릭 **새로**을 차례로 클릭 하 고 **DWORD (32 비트) 값**합니다.

6. 시간, NPS 서버 첫 번째 성공적으로 인증을 시도 클라이언트가 후 클라이언트 컴퓨터의 TLS 핸들 캐시를 원하는 시간 (밀리초)에 입력 합니다.

## <a name="obtain-the-sha-1-hash-of-a-trusted-root-ca-certificate"></a>신뢰할 수 있는 루트 인증서를 콘텐츠의 해시의 SHA-1 받기

이 절차를 사용 하 여 Secure Hash Algorithm sha-1 () 콘텐츠의 해시 신뢰할 수 있는 루트 인증 기관 (캐나다), 로컬 컴퓨터에 설치 되어 있는 인증서를 얻을 수 있습니다. 어떤 경우에는 인증서 SHA-1 해시 인증서를 사용 하 여 지정 하는 데 필요한 그룹 정책, 배포할 때와 같은 합니다.

그룹 정책을 사용 하 고 EAP 또는 PEAP 상호 인증 과정 NPS 서버 인증을 위해 클라이언트를 사용 해야 하는 하나 이상의 신뢰할 수 있는 루트 캘리포니아 인증서 지정할 수 있습니다. 서버 인증서를 확인 하는 클라이언트를 사용 해야 하는 신뢰할 수 있는 루트 캘리포니아 인증서를 지정 하려면 인증서의 SHA-1 해시를 입력할 수 있습니다.

이 절차를 신뢰할 수 있는 루트 인증서를의 SHA-1 해시 인증서 Microsoft Management Console (MMC) 스냅인를 사용 하 여 가져오는 방법을 보여 줍니다. 

이 절차를 완료 하려면의 회원 있어야는 **사용자** 로컬 컴퓨터에서 합니다.

### <a name="to-obtain-the-sha-1-hash-of-a-trusted-root-ca-certificate"></a>SHA-1 해시 신뢰할 수 있는 캘리포니아 루트 인증서를 얻는

1. Windows PowerShell 또는 실행 대화 상자를에 입력 **mmc**, ENTER 키를 누릅니다. Microsoft Management Console \(MMC\) 열립니다. MMC 클릭 **파일**, 클릭 한 다음 **추가/제거 Snap\in**합니다. **추가 또는 제거 스냅인** 대화 상자를 엽니다.

2. **추가 또는 제거 스냅인**에서 **사용 가능한 스냅인**, 두 번 클릭 **인증서**합니다. 마법사 스냅인 인증서가 열립니다. 클릭 **컴퓨터 계정**을 차례로 클릭 하 고 **다음**합니다.

3. **컴퓨터 선택**, 되도록 **로컬 컴퓨터 (이 본체에서 실행 중인 컴퓨터)** 는 선택한 클릭 **완료**, 클릭 한 다음 **확인**합니다.

4. 왼쪽된 창에서 두 번 클릭 **(로컬 컴퓨터) 인증서**, 다음 두 번 클릭 하 고 있는 **신뢰할 수 있는 인증 기관** 폴더 합니다.

5. **인증서** 폴더의 하위 폴더는는 **신뢰할 수 있는 인증 기관** 폴더 합니다. 클릭 하 고 **인증서** 폴더 합니다.

6. 세부 정보 창에서 신뢰할 수 있는 사용자 루트 캘리포니아 인증서를 찾습니다. 인증서를 두 번 클릭 합니다. **인증서** 대화 상자를 엽니다.

7. 에 **인증서** 대화 상자를 클릭 하는 **세부 정보** 탭 합니다.

8. 으로 스크롤하여 필드 목록에서 선택한 **지문**합니다.

9. 인증서의 SHA-1 해시 16 진 문자열 아래쪽 창에 표시 됩니다. 선택은 SHA-1 해시 누르고 Windows 바로 가기 키 복사본 해시 Windows 클립보드에 복사 하려면 \(CTRL\+C\) 명령을 실행 됩니다.

10. 위치를 열고 \(CTRL\+V\) 명령를 붙여 SHA-1 해시, 올바르게 커서를 찾아 붙여넣기에 대 한 Windows 바로 가기 키를 누릅니다. 

인증서 NPS에 대 한 자세한 내용은 참조 [PEAP 및 EAP 요구 사항에 대 한 구성 인증서 템플릿](nps-manage-cert-requirements.md)합니다.

NPS에 대 한 자세한 내용은 참조 [네트워크 NPS 정책 서버 ()](nps-top.md)합니다.
