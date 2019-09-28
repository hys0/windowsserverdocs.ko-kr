---
title: NPS와 함께 사용되는 인증서 관리
description: 이 항목에서는 Windows Server 2016의 네트워크 정책 서버에서 서버 인증서를 사용 하는 방법에 대 한 정보를 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 204a4ef4-9d78-4a62-9940-43cc0e1c39d0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b83f68b52a9cceef779e5204e295bbc9e45e7a14
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71396200"
---
# <a name="manage-certificates-used-with-nps"></a>NPS와 함께 사용되는 인증서 관리

>적용 대상: Windows Server(반기 채널), Windows Server 2016

인증서 기반 인증 방법을 배포 하는 경우 (예: 확장할 수 있는 인증 프로토콜 @ no__t-0Transport Layer Security \(EAP @ no__t-2TLS @ no__t-3, Protected Extensible Authentication Protocol @ no__t-4Transport Layer Security @no__ t-5PEAP @ no__t-6TLS @ no__t-7 및 PEAP @ no__t-8Microsoft 챌린지 핸드셰이크 인증 프로토콜 버전 2 \(MS @ no__t-10CHAP v2 @ no__t-11, 모든 NPSs에 서버 인증서를 등록 해야 합니다. 서버 인증서는 다음을 수행 해야 합니다.

- [PEAP 및 EAP 요구 사항에 대 한 인증서 템플릿 구성](nps-manage-cert-requirements.md) 에 설명 된 최소 서버 인증서 요구 사항을 충족 합니다.

- 클라이언트 컴퓨터에서 신뢰 하는 \(CA @ no__t-1 인증 기관에서 발급 합니다. 현재 사용자 및 로컬 컴퓨터에 대 한 신뢰할 수 있는 루트 인증 기관 인증서 저장소에 해당 인증서가 있으면 CA를 신뢰할 수 있습니다.

다음 지침에 따라 신뢰할 수 있는 루트 CA가 타사 CA (예: Verisign) 인 배포에서 NPS 인증서를 관리할 수 있으며,를 사용 하 여 \(PKI @ no__t-1을 사용 하 여 공개 키 인프라에 대해 배포한 CA를 관리할 수 있습니다 Active Directory 인증서 서비스 \(AD CS @ no__t-3.

## <a name="change-the-cached-tls-handle-expiry"></a>캐시 된 TLS 핸들 만료 변경

EAP @ no__t-0TLS, PEAP @ no__t-1TLS 및 PEAP @ no__t-2MS @ no__t-3CHAP v 2에 대 한 초기 인증 프로세스 중에 NPS는 연결 하는 클라이언트의 TLS 연결 속성의 일부를 캐시 합니다. 또한 클라이언트는 NPS의 TLS 연결 속성 일부를 캐시 합니다.

이러한 TLS 연결 속성의 각 개별 컬렉션을 TLS 핸들 이라고 합니다.

클라이언트 컴퓨터는 여러 인증자에 대 한 TLS 핸들을 캐시할 수 있지만 NPSs는 많은 클라이언트 컴퓨터의 TLS 핸들을 캐시할 수 있습니다.

클라이언트 및 서버에서 캐시 된 TLS 핸들을 사용 하면 재인증 프로세스가 보다 신속 하 게 발생 합니다. 예를 들어, 무선 컴퓨터가 NPS로 reauthenticates 때 NPS는 무선 클라이언트에 대 한 TLS 핸들을 검사 하 고 클라이언트 연결이 다시 연결 인지 여부를 신속 하 게 확인할 수 있습니다. NPS는 전체 인증을 수행 하지 않고 연결에 권한을 부여 합니다.

마찬가지로, 클라이언트는 NPS에 대 한 TLS 핸들을 검사 하 고, 다시 연결 하는 것을 확인 하며, 서버 인증을 수행할 필요가 없습니다.

Windows 10 및 Windows Server 2016를 실행 하는 컴퓨터에서 기본 TLS 핸들 만료 시간은 10 시간입니다.

경우에 따라 TLS 핸들 만료 시간을 늘리거나 줄일 수 있습니다.

예를 들어 관리자가 사용자 인증서를 해지 하 고 인증서가 만료 된 경우에 TLS 핸들 만료 시간을 줄일 수 있습니다. 이 시나리오에서는 NPS에 만료 되지 않은 캐시 된 TLS 핸들이 있는 경우에도 사용자가 네트워크에 연결할 수 있습니다. TLS 핸들 만료를 줄이면 해지 된 인증서를 가진 사용자가 다시 연결 되지 않도록 방지 하는 데 도움이 될 수 있습니다.

>[!NOTE]
>이 시나리오의 가장 좋은 해결 방법은 Active Directory에서 사용자 계정을 사용 하지 않도록 설정 하거나 네트워크 정책에서 네트워크에 연결할 수 있는 권한이 부여 된 Active Directory 그룹에서 사용자 계정을 제거 하는 것입니다. 그러나 복제 대기 시간으로 인해 모든 도메인 컨트롤러에 대 한 이러한 변경 내용의 전파가 지연 될 수도 있습니다. 

## <a name="configure-the-tls-handle-expiry-time-on-client-computers"></a>클라이언트 컴퓨터에서 TLS 핸들 만료 시간 구성

이 절차를 사용 하 여 클라이언트 컴퓨터가 NPS의 TLS 핸들을 캐시 하는 시간을 변경할 수 있습니다. NPS를 성공적으로 인증 한 후 클라이언트 컴퓨터는 NPS의 TLS 연결 속성을 TLS 핸들로 캐시 합니다. TLS 핸들의 기본 기간은 10 시간 \(36000000 밀리초 @ no__t-1입니다. 다음 절차를 사용 하 여 TLS 핸들 만료 시간을 늘리거나 줄일 수 있습니다.

멤버 자격이 **관리자**, 또는 이와 동등한 최소한이이 절차를 완료 합니다.

>[!IMPORTANT]
>이 절차는 클라이언트 컴퓨터가 아닌 NPS에서 수행 해야 합니다.

### <a name="to-configure-the-tls-handle-expiry-time-on-client-computers"></a>클라이언트 컴퓨터에서 TLS 핸들 만료 시간을 구성 하려면

1. NPS에서 레지스트리 편집기를 엽니다.

2. **HKEY @ no__t-1LOCAL @ no__t-2MACHINE\System\CurrentControlSet\Control\SecurityProviders\SCHANNEL** 레지스트리 키로 이동 합니다.

3. **편집** 메뉴에서 **새로 만들기**를 클릭 한 다음 **키**를 클릭 합니다.

4. **Clientcachetime**을 입력 한 다음 enter 키를 누릅니다.

5. **Clientcachetime**을 마우스 오른쪽 단추로 클릭 하 고 **새로 만들기**를 클릭 한 다음 **DWORD (32 비트) 값**을 클릭 합니다.

6. 클라이언트 컴퓨터에서 nps의 인증 시도가 처음 성공한 후 NPS의 TLS 핸들을 캐시 하도록 할 시간 (밀리초)을 입력 합니다.

## <a name="configure-the-tls-handle-expiry-time-on-npss"></a>NPSs에서 TLS 핸들 만료 시간 구성

NPSs가 클라이언트 컴퓨터의 TLS 핸들을 캐시 하는 시간을 변경 하려면 다음 절차를 따르십시오. Access 클라이언트를 성공적으로 인증 한 후 NPSs는 클라이언트 컴퓨터의 TLS 연결 속성을 TLS 핸들로 캐시 합니다. TLS 핸들의 기본 기간은 10 시간 \(36000000 밀리초 @ no__t-1입니다. 다음 절차를 사용 하 여 TLS 핸들 만료 시간을 늘리거나 줄일 수 있습니다.

멤버 자격이 **관리자**, 또는 이와 동등한 최소한이이 절차를 완료 합니다.

>[!IMPORTANT]
>이 절차는 클라이언트 컴퓨터가 아닌 NPS에서 수행 해야 합니다.

### <a name="to-configure-the-tls-handle-expiry-time-on-npss"></a>NPSs에서 TLS 핸들 만료 시간을 구성 하려면

1. NPS에서 레지스트리 편집기를 엽니다.

2. **HKEY @ no__t-1LOCAL @ no__t-2MACHINE\System\CurrentControlSet\Control\SecurityProviders\SCHANNEL** 레지스트리 키로 이동 합니다.

3. **편집** 메뉴에서 **새로 만들기**를 클릭 한 다음 **키**를 클릭 합니다.

4. **Servercachetime**을 입력 한 다음 enter 키를 누릅니다.

5. **Servercachetime**을 마우스 오른쪽 단추로 클릭 하 고 **새로 만들기**를 클릭 한 다음 **DWORD (32 비트) 값**을 클릭 합니다.

6. 클라이언트의 첫 번째 인증 시도가 성공한 후에 NPSs가 클라이언트 컴퓨터의 TLS 핸들을 캐시 하는 데 걸린 시간 (밀리초)을 입력 합니다.

## <a name="obtain-the-sha-1-hash-of-a-trusted-root-ca-certificate"></a>신뢰할 수 있는 루트 CA 인증서의 SHA-1 해시 가져오기

이 절차를 사용 하 여 로컬 컴퓨터에 설치 된 인증서에서 신뢰할 수 있는 루트 CA (인증 기관)의 SHA-1 (Secure Hash Algorithm) 해시를 가져올 수 있습니다. 그룹 정책를 배포 하는 경우와 같이 인증서의 SHA-1 해시를 사용 하 여 인증서를 지정 해야 하는 경우도 있습니다.

그룹 정책를 사용 하는 경우 EAP 또는 PEAP를 사용 하 여 상호 인증 과정에서 NPS를 인증 하기 위해 클라이언트가 사용 해야 하는 신뢰할 수 있는 루트 CA 인증서를 하나 이상 지정할 수 있습니다. 클라이언트에서 서버 인증서의 유효성을 검사 하는 데 사용 해야 하는 신뢰할 수 있는 루트 CA 인증서를 지정 하기 위해 인증서의 SHA-1 해시를 입력할 수 있습니다.

이 절차에서는 인증서 MMC (Microsoft Management Console) 스냅인을 사용 하 여 신뢰할 수 있는 루트 CA 인증서의 SHA-1 해시를 가져오는 방법을 보여 줍니다. 

이 절차를 완료 하려면 로컬 컴퓨터에서 **사용자** 그룹의 구성원 이어야 합니다.

### <a name="to-obtain-the-sha-1-hash-of-a-trusted-root-ca-certificate"></a>신뢰할 수 있는 루트 CA 인증서의 SHA-1 해시를 가져오려면

1. 실행 대화 상자 또는 Windows PowerShell에서 **mmc**를 입력 한 다음 enter 키를 누릅니다. Microsoft Management Console \(MMC @ no__t-1이 열립니다. MMC에서 **파일**을 클릭 한 다음 **Snap\in 추가/제거**를 클릭 합니다. **추가 / 제거 스냅인** 대화 상자가 열립니다.

2. **스냅인 추가/제거**의 **사용 가능한 스냅인**에서 **인증서**를 두 번 클릭 합니다. 인증서 스냅인 마법사가 열립니다. **컴퓨터 계정**을 클릭 한 후 **다음**을 클릭 합니다.

3. **컴퓨터 선택**에서 **로컬 컴퓨터 (이 콘솔이 실행 되 고 있는 컴퓨터)** 가 선택 되어 있는지 확인 하 고 **마침**을 클릭 한 다음 **확인**을 클릭 합니다.

4. 왼쪽 창에서 **인증서 (로컬 컴퓨터)** 를 두 번 클릭 한 다음 **신뢰할 수 있는 루트 인증 기관** 폴더를 두 번 클릭 합니다.

5. **Certificate** 폴더는 **신뢰할 수 있는 루트 인증 기관** 폴더의 하위 폴더입니다. **인증서** 폴더를 클릭 합니다.

6. 세부 정보 창에서 신뢰할 수 있는 루트 CA에 대 한 인증서를 찾습니다. 인증서를 두 번 클릭 합니다. **인증서** 대화 상자가 열립니다.

7. **인증서** 대화 상자에서 **세부 정보** 탭을 클릭 합니다.

8. 필드 목록에서를 스크롤하여 **지문**을 선택 합니다.

9. 아래쪽 창에서 인증서의 SHA-1 해시가 표시 되는 16 진수 문자열을 표시 합니다. SHA-1 해시를 선택 하 고 복사 명령에 대 한 Windows 바로 가기 키 \(CTRL @ no__t-1C @ no__t-2를 눌러 해시를 Windows 클립보드에 복사 합니다.

10. SHA-1 해시를 붙여 넣을 위치를 열고, 커서를 올바르게 찾은 다음, 붙여넣기 명령에 대 한 Windows 바로 가기 키 \(CTRL @ no__t-1V no__t-2를 누릅니다. 

인증서 및 NPS에 대 한 자세한 내용은 [PEAP 및 EAP 요구 사항에 대 한 인증서 템플릿 구성](nps-manage-cert-requirements.md)을 참조 하세요.

NPS에 대 한 자세한 내용은 [nps (네트워크 정책 서버)](nps-top.md)를 참조 하세요.
