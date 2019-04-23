---
title: NPS와 함께 사용되는 인증서 관리
description: 이 항목에서는 Windows Server 2016에서 네트워크 정책 서버를 사용 하 여 서버 인증서를 사용 하는 방법에 대 한 정보를 제공 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 204a4ef4-9d78-4a62-9940-43cc0e1c39d0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 73f3d6a1e9dc6ae1520b1d685b6b05b5f3aed601
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864234"
---
# <a name="manage-certificates-used-with-nps"></a>NPS와 함께 사용되는 인증서 관리

>적용 대상: Windows Server (반기 채널), Windows Server 2016

Extensible Authentication Protocol 등는 인증서 기반 인증 방법을 배포한 경우\-Transport Layer Security \(EAP\-TLS\), Protected Extensible Authentication Protocol\-Transport Layer Security \(PEAP\-TLS\), 및 PEAP\-Microsoft Challenge Handshake Authentication Protocol 버전 2 \(MS\-CHAP v2\), 모든 프로그램 NPSs에 서버 인증서를 등록 해야 합니다. 서버 인증서는 다음 작업을 수행 해야합니다.

- 에 설명 된 대로 최소 서버 인증서 요구 사항을 충족 [PEAP 및 EAP 요구 사항에 대 한 인증서 템플릿 구성](nps-manage-cert-requirements.md)

- 인증 기관에서 발급 \(CA\) 클라이언트 컴퓨터에서 신뢰할 수 있는 것입니다. 현재 사용자와 로컬 컴퓨터에 대 한 신뢰할 수 있는 루트 인증 기관 인증서 저장소에 해당 인증서가 있는 경우 CA는 신뢰할 수 있는 합니다.

신뢰할 수 있는 루트 CA가 타사 CA에서 Verisign 등 또는 공개 키 인프라에 대 한 배포는 CA가 있는 배포에 NPS 인증서를 관리에 도움이 되도록 다음 지침 \(PKI\) 활성을 사용 하 여 Directory 인증서 서비스 \(AD CS\)합니다.

## <a name="change-the-cached-tls-handle-expiry"></a>캐시 된 TLS 핸들 만료를 변경 합니다.

EAP에 대 한 초기 인증 프로세스 중\-TLS, PEAP\-TLS 및 PEAP\-MS\-CHAP v2, NPS 연결 중인 클라이언트의 TLS 연결 속성의 일부분을 캐시 합니다. 클라이언트는 또한 NPS의 TLS 연결 속성의 일부분을 캐시합니다.

이러한 TLS 연결 속성의 각 개별 컬렉션에 대 한 TLS 핸들을 라고 합니다.

클라이언트 컴퓨터 NPSs 여러 클라이언트 컴퓨터의 TLS 핸들을 캐시할 수 있지만 여러 인증자에 대 한 TLS 핸들을 캐시할 수 있습니다.

클라이언트와 서버에서 캐시 된 TLS 핸들을 더 신속 하 게 발생 하는 다시 인증 프로세스를 허용 합니다. 예를 들어, 무선 컴퓨터가는 NPS를 사용 하 여 다시 인증할 NPS 무선 클라이언트에 대 한 TLS 핸들을 검사할 수 및 클라이언트 연결이 다시 연결 되도록 빠르게 확인할 수 있습니다. NPS에는 전체 인증을 수행 하지 않고 연결 권한을 부여 합니다.

마찬가지로, 클라이언트 NPS에 대 한 TLS 핸들 검사, 확인을 다시 연결 되 고 서버 인증을 수행할 필요가 없습니다.

Windows 10 및 Windows Server 2016를 실행 하는 컴퓨터에서 기본 TLS 핸들 만료는 10 시간입니다.

일부 경우에는 TLS 핸들 만료 시간을 늘리거나는 것이 좋습니다.

예를 들어 다음 경우 관리자가 사용자의 인증서가 해지 된 인증서가 만료 되었습니다 않았고 TLS 핸들 만료 시간을 감소 하는 것이 좋습니다. 사용자가이 시나리오에서는 여전히 NPS에 캐시 된 TLS 핸들 만료 되지 않은 경우 네트워크에 연결할 수 있습니다. TLS를 줄이는 핸들 만료 방지할 수 있습니다 해지 된 인증서를 사용 하 여 사용자가 다시 연결 합니다.

>[!NOTE]
>이 시나리오에 가장 적합 한 솔루션 인지 Active Directory에서 사용자 계정을 사용 하지 않으려면 네트워크 정책에서 네트워크를 연결할 수 있는 권한이 부여 되는 Active Directory 그룹에서 사용자 계정을 제거 하려면. 모든 도메인 컨트롤러에 이러한 변경 내용 전파도 지연 될 수 있습니다, 있지만 복제 지연으로 인 한 합니다. 

## <a name="configure-the-tls-handle-expiry-time-on-client-computers"></a>클라이언트 컴퓨터에서 TLS 핸들 만료 시간을 구성 합니다.

클라이언트 컴퓨터는 NPS의 TLS 핸들을 캐시 하는 크기를 변경 하려면이 절차를 사용할 수 있습니다. NPS를 성공적으로 인증 한 후 클라이언트 컴퓨터는 TLS 핸들로 NPS의 TLS 연결 속성을 캐시 합니다. TLS 핸들 10 시간의 기본 기간이 \(36,000,000 밀리초\)합니다. 증가 하 하거나 다음 절차를 사용 하 여 TLS 핸들 만료 시간을 줄일 수 있습니다.

멤버 자격이 **관리자**, 또는 이와 동등한 최소한이이 절차를 완료 합니다.

>[!IMPORTANT]
>이 절차는 클라이언트 컴퓨터에 없는 NPS에서 수행 되어야 합니다.

### <a name="to-configure-the-tls-handle-expiry-time-on-client-computers"></a>TLS를 구성 하려면 클라이언트 컴퓨터에서 만료 시간을 처리

1. NPS를에서 레지스트리 편집기를 엽니다.

2. 레지스트리 키를 찾습니다 **HKEY\_로컬\_MACHINE\System\CurrentControlSet\Control\SecurityProviders\SCHANNEL**

3. 에 **편집** 메뉴에서 클릭 **새로 만들기**를 클릭 하 고 **키**합니다.

4. 형식 **ClientCacheTime**, 한 다음 ENTER를 누릅니다.

5. 마우스 오른쪽 단추로 클릭 **ClientCacheTime**, 클릭 **새로 만들기**를 클릭 하 고 **(32 비트) Dword**합니다.

6. 클라이언트 컴퓨터는 NPS를 통해 첫 번째 성공한 인증 시도 후에 NPS의 TLS 핸들을 캐시 하려는 시간 (밀리초)의 시간을 입력 합니다.

## <a name="configure-the-tls-handle-expiry-time-on-npss"></a>NPSs에서 TLS 핸들 만료 시간을 구성 합니다.

NPSs 클라이언트 컴퓨터의 TLS 핸들을 캐시 하는 크기를 변경 하려면이 절차를 따르십시오. 액세스 클라이언트를 성공적으로 인증 한 후 NPSs TLS 핸들로 클라이언트 컴퓨터의 TLS 연결 속성을 캐시 합니다. TLS 핸들 10 시간의 기본 기간이 \(36,000,000 밀리초\)합니다. 증가 하 하거나 다음 절차를 사용 하 여 TLS 핸들 만료 시간을 줄일 수 있습니다.

멤버 자격이 **관리자**, 또는 이와 동등한 최소한이이 절차를 완료 합니다.

>[!IMPORTANT]
>이 절차는 클라이언트 컴퓨터에 없는 NPS에서 수행 되어야 합니다.

### <a name="to-configure-the-tls-handle-expiry-time-on-npss"></a>구성 TLS NPSs의 만료 시간이 처리

1. NPS를에서 레지스트리 편집기를 엽니다.

2. 레지스트리 키를 찾습니다 **HKEY\_로컬\_MACHINE\System\CurrentControlSet\Control\SecurityProviders\SCHANNEL**

3. 에 **편집** 메뉴에서 클릭 **새로 만들기**를 클릭 하 고 **키**합니다.

4. 형식 **ServerCacheTime**, 한 다음 ENTER를 누릅니다.

5. 마우스 오른쪽 단추로 클릭 **ServerCacheTime**, 클릭 **새로 만들기**를 클릭 하 고 **(32 비트) Dword**합니다.

6. 밀리초 NPSs 클라이언트에서 첫 번째 성공한 인증 시도 후 클라이언트 컴퓨터의 TLS 핸들을 캐시 하려는 시간에를 입력 합니다.

## <a name="obtain-the-sha-1-hash-of-a-trusted-root-ca-certificate"></a>신뢰할 수 있는 루트 CA 인증서의 sha-1 해시를 가져오려면

이 절차를 로컬 컴퓨터에 설치 되어 있는 인증서 로부터 Secure Hash Algorithm (sha-1)을 신뢰할 수 있는 루트 인증 기관 (CA)의 해시를 가져올 수 있습니다. 일부 경우에는 인증서의 sha-1 해시를 사용 하 여 인증서를 지정 하는 데 필요한 그룹 정책에 배포할 때와 같이 합니다.

그룹 정책을 사용 하는 경우에 클라이언트 EAP 또는 PEAP를 사용 하 여 상호 인증 프로세스 중 NPS 인증 하기 위해 사용 해야 하는 하나 이상의 신뢰할 수 있는 루트 CA 인증서를 지정할 수 있습니다. 서버 인증서의 유효성을 검사 하려면 클라이언트를 사용 해야 하는 신뢰할 수 있는 루트 CA 인증서를 지정 하려면 인증서의 sha-1 해시를 입력할 수 있습니다.

이 절차에는 인증서 Microsoft Management Console (MMC) 스냅인을 사용 하 여 sha-1 신뢰할 수 있는 루트 CA 인증서의 해시를 가져오는 방법을 보여 줍니다. 

이 절차를 완료 하려면의 구성원 이어야 하는 **사용자** 로컬 컴퓨터의 그룹입니다.

### <a name="to-obtain-the-sha-1-hash-of-a-trusted-root-ca-certificate"></a>SHA-1(secure 신뢰할 수 있는 루트 CA 인증서의 해시를 가져오려면

1. 실행 대화 상자 또는 Windows PowerShell에서 입력 **mmc**, 한 다음 ENTER를 누릅니다. Microsoft Management Console \(MMC\) 열립니다. Mmc에서 클릭 **파일**, 클릭 **추가/제거 Snap\in**합니다. **추가 / 제거 스냅인** 대화 상자가 열립니다.

2. **추가 / 제거 스냅인**의 **사용 가능한 스냅인**를 두 번 클릭 **인증서**합니다. 인증서 스냅인에서 마법사가 열립니다. 클릭 **컴퓨터 계정**를 클릭 하 고 **다음**합니다.

3. **컴퓨터 선택**, 했는지 **로컬 컴퓨터 (이 콘솔이 실행 되는 컴퓨터)** 은 선택한 상태에서 **마침**, 클릭 하 고 **확인**.

4. 왼쪽된 창에서 두 번 클릭 **인증서 (로컬 컴퓨터)** 를 차례로 두 번 클릭 합니다 **신뢰할 수 있는 루트 인증 기관** 폴더입니다.

5. 합니다 **인증서** 폴더의 하위 폴더입니다 합니다 **신뢰할 수 있는 루트 인증 기관** 폴더입니다. 클릭 합니다 **인증서** 폴더입니다.

6. 세부 정보 창에서 신뢰할 수 있는 루트 CA에 대 한 인증서를 찾습니다. 인증서를 두 번 클릭 합니다. 합니다 **인증서** 대화 상자가 열립니다.

7. 에 **인증서** 대화 상자에서 클릭 합니다 **세부 정보** 탭 합니다.

8. 필드 목록에서 선택한 **지문을**합니다.

9. 인증서의 sha-1 해시는 16 진수 문자열은 아래쪽 창에 표시 됩니다. Sha-1 해시를 선택 하 고 복사 명령에 대 한 Windows 바로 가기 키를 누릅니다 \(CTRL\+C\) 해시를 Windows 클립보드에 복사 합니다.

10. Sha-1 해시를 붙여 넣습니다, 커서를 올바르게 찾습니다 및 붙여넣기 명령에 대 한 Windows 바로 가기 키를 누릅니다. 하려는 위치를 엽니다 \(CTRL\+V\)합니다. 

인증서 및 NPS에 대 한 자세한 내용은 참조 하세요. [PEAP 및 EAP 요구 사항에 대 한 인증서 템플릿 구성](nps-manage-cert-requirements.md)합니다.

NPS에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 (NPS 서버)](nps-top.md)합니다.
