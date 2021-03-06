---
title: NPS 서버 설치 및 구성
description: VPN 서버에서 전송 하는 연결 요청에 대 한 NPS 서버 처리는 사용자에 게 연결 권한이 있는지 확인 하 고, 사용자의 id를 확인 하 고, NPS에서 RADIUS 계정을 구성할 때 선택한 연결 요청의 측면을 기록 합니다.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.localizationpriority: medium
ms.author: v-tea
author: Teresa-MOTIV
ms.date: 08/30/2018
ms.openlocfilehash: d286f44e198aa13204b884da3fdf729f18b7553b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860456"
---
# <a name="step-4-install-and-configure-the-network-policy-server-nps"></a>4단계. NPS (네트워크 정책 서버) 설치 및 구성

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**다음:** 3 단계. Always On VPN에 대 한 원격 액세스 서버 구성](vpn-deploy-ras.md)
- [**다음:** 5 단계. DNS 및 방화벽 설정 구성](vpn-deploy-dns-firewall.md)

이 단계에서는 VPN 서버에서 전송 하는 연결 요청을 처리 하기 위해 NPS (네트워크 정책 서버)를 설치 합니다.

- 권한 부여를 수행 하 여 사용자에 게 연결할 권한이 있는지 확인 합니다.
- 인증을 수행 하 여 사용자의 id를 확인 합니다.
- NPS에서 RADIUS 계정을 구성할 때 선택한 연결 요청의 측면을 기록 하기 위해 계정을 수행 합니다.

이 섹션의 단계를 통해 다음 항목을 완료할 수 있습니다.

1. NPS 서버에 대해 계획 하 고 조직 또는 회사 네트워크에 설치 된 컴퓨터 또는 VM에서 NPS를 설치할 수 있습니다.

   >[!TIP]
   >네트워크에 하나 이상의 NPS 서버가 이미 있는 경우 NPS 서버 설치를 수행할 필요가 없습니다. 대신이 항목을 사용 하 여 기존 NPS 서버의 구성을 업데이트할 수 있습니다.

> [!NOTE]
> Windows Server Core에는 네트워크 정책 서버 서비스를 설치할 수 없습니다.

2. 조직/회사 NPS 서버에서 VPN 서버 로부터 받은 연결 요청을 처리 하는 RADIUS 서버를 수행 하도록 NPS를 구성할 수 있습니다.

## <a name="install-network-policy-server"></a>NPS(네트워크 정책 서버) 설치

이 절차에서는 Windows PowerShell 또는 서버 관리자 역할 및 기능 추가 마법사를 사용 하 여 NPS를 설치 합니다. NPS는 네트워크 정책 및 액세스 서비스 서버 역할의 역할 서비스입니다.

>[!TIP]
>기본적으로 NPS는 설치된 모든 네트워크 어댑터의 포트 1812, 1813, 1645 및 1646에서 RADIUS 트래픽을 수신 대기합니다. NPS를 설치 하 고 고급 보안이 포함 된 Windows 방화벽을 사용 하도록 설정 하면 이러한 포트에 대 한 방화벽 예외가 IPv4 및 IPv6 트래픽 모두에 대해 자동으로 생성 됩니다. 네트워크 액세스 서버가 이러한 기본값 이외의 포트를 통해 RADIUS 트래픽을 보내도록 구성 된 경우에는 NPS 설치 중에 고급 보안이 설정 된 Windows 방화벽에서 생성 된 예외를 제거 하 고에서 사용 하는 포트에 대 한 예외를 만듭니다. RADIUS 트래픽

**Windows PowerShell에 대 한 절차:**

Windows PowerShell을 사용 하 여이 절차를 수행 하려면 관리자 권한으로 Windows PowerShell을 실행 하 고 다음 cmdlet을 입력 합니다.

```powershell
Install-WindowsFeature NPAS -IncludeManagementTools
```

**서버 관리자에 대 한 절차:**

1.  서버 관리자에서 **관리**를 선택 하 고 **역할 및 기능 추가**를 선택 합니다.
        역할 및 기능 추가 마법사가 열립니다.

2.  시작 하기 전에에서 **다음**을 선택 합니다.

    >[!NOTE] 
    >이전에 역할 및 기능 추가 마법사가 실행 될 때 **이 페이지를 기본적으로 건너뜀** 을 선택한 경우에는 역할 및 기능 추가 마법사의 **시작 하기 전** 페이지가 표시 되지 않습니다.

3.  설치 유형 선택에서 **역할 기반 또는 기능 기반 설치** 가 선택 되어 있는지 확인 하 고 **다음**을 선택 합니다.

4.  대상 서버 선택에서 **서버 풀에서 서버 선택** 이 선택 되어 있는지 확인 합니다.

5.  서버 풀에서 로컬 컴퓨터가 선택 되어 있는지 확인 하 고 **다음**을 선택 합니다.

6.  서버 역할 선택의 **역할**에서 **네트워크 정책 및 액세스 서비스**를 선택 합니다. 네트워크 정책 및 액세스 서비스에 필요한 기능을 추가 해야 하는지 여부를 묻는 대화 상자가 열립니다.

7.  **기능 추가**를 선택 하 고 **다음** 을 선택 합니다.

8.  기능 선택에서 **다음**을 선택 하 고 네트워크 정책 및 액세스 서비스에서 제공 된 정보를 검토 한 후 **다음**을 선택 합니다.

9.  역할 서비스 선택에서 **네트워크 정책 서버**를 선택 합니다.

10. 네트워크 정책 서버에 필요한 기능에 대해 **기능 추가**를 선택 하 고 **다음**을 선택 합니다.

11. 설치 선택 확인에서 **필요한 경우 자동으로 대상 서버 다시 시작**을 선택 합니다.

12. **예** 를 선택 하 여 선택한를 확인 한 후 **설치**를 선택 합니다.
    
    설치 진행률 페이지에는 설치 과정 중에 상태가 표시 됩니다. 프로세스가 완료 되 면 " *computername*에서 설치가 완료 되었습니다." 라는 메시지가 표시 됩니다. 여기서 *Computername* 은 네트워크 정책 서버를 설치한 컴퓨터의 이름입니다.

13. **닫기**를 선택합니다.

## <a name="configure-nps"></a>NPS 구성

NPS를 설치한 후 VPN 서버에서 받는 연결 요청에 대 한 모든 인증, 권한 부여 및 계정 의무를 처리 하도록 NPS를 구성 합니다.

### <a name="register-the-nps-server-in-active-directory"></a>Active Directory에 NPS 서버 등록

이 절차에서는 연결 요청을 처리 하는 동안 사용자 계정 정보에 액세스할 수 있는 권한이 있도록 Active Directory에 서버를 등록 합니다.

**여기서**

1.  서버 관리자에서 **도구**를 선택 하 고 **네트워크 정책 서버**를 선택 합니다. NPS 콘솔이 열립니다.

2.  NPS 콘솔에서 **nps (로컬)** 를 마우스 오른쪽 단추로 클릭 한 다음 **Active Directory에 서버 등록**을 선택 합니다.
   
     네트워크 정책 서버 대화 상자가 열립니다.

3.  네트워크 정책 서버 대화 상자에서 **확인** 을 두 번 선택 합니다.

NPS를 등록 하는 다른 방법은 [ACTIVE DIRECTORY 도메인 Nps 서버 등록](../../../../../networking/technologies/nps/nps-manage-register.md)을 참조 하세요.

### <a name="configure-network-policy-server-accounting"></a>네트워크 정책 서버 계정 구성

이 절차에서는 다음 로깅 유형 중 하나를 사용 하 여 네트워크 정책 서버 계정을 구성 합니다.

- **이벤트 로깅**. 주로 연결 시도를 감사 하 고 문제를 해결 하는 데 사용 됩니다. Nps 콘솔에서 nps 서버 속성을 가져와 NPS 이벤트 로깅을 구성할 수 있습니다.

- **사용자 인증 및 계정 요청을 로컬 파일에 기록**합니다. 주로 연결 분석과 청구 목적으로 사용 됩니다. 공격 후 악의적인 사용자의 활동을 추적 하는 방법을 제공 하기 때문에 보안 조사 도구로도 사용 됩니다. 계정 구성 마법사를 사용 하 여 로컬 파일 로깅을 구성할 수 있습니다.

- **MICROSOFT SQL SERVER XML 규격 데이터베이스에 사용자 인증 및 계정 요청을 기록**합니다. NPS를 실행 하는 여러 서버에서 하나의 데이터 원본을 갖도록 허용 하는 데 사용 됩니다. 에서는 관계형 데이터베이스를 사용 하는 경우의 이점도 제공 합니다. 계정 구성 마법사를 사용 하 여 SQL Server 로깅을 구성할 수 있습니다.

네트워크 정책 서버 계정을 구성 하려면 [네트워크 정책 서버 계정 구성](../../../../../networking/technologies/nps/nps-accounting-configure.md)을 참조 하세요.

### <a name="add-the-vpn-server-as-a-radius-client"></a>VPN 서버를 RADIUS 클라이언트로 추가

[ALWAYS ON vpn에 대 한 원격 액세스 서버 구성](vpn-deploy-ras.md) 섹션에서 vpn 서버를 설치 하 고 구성 했습니다. VPN 서버를 구성 하는 동안 VPN 서버에 RADIUS 공유 암호를 추가 했습니다.

이 절차에서는 동일한 공유 암호 텍스트 문자열을 사용 하 여 NPS에서 VPN 서버를 RADIUS 클라이언트로 구성 합니다. VPN 서버에서 사용한 것과 같은 텍스트 문자열을 사용 하거나 NPS 서버와 VPN 서버 간의 통신에 실패 합니다.

>[!IMPORTANT] 
>네트워크에 새 네트워크 액세스 서버 (VPN 서버, 무선 액세스 지점, 인증 스위치 또는 전화 접속 서버)를 추가할 때 NPS가 인식 하 고 네트워크 액세스 서버와 통신할 수 있도록 NPS에서 서버를 RADIUS 클라이언트로 추가 해야 합니다.

**여기서**

1. Nps 서버의 NPS 콘솔에서 **RADIUS 클라이언트 및 서버**를 두 번 클릭 합니다.

2. **RADIUS 클라이언트** 를 마우스 오른쪽 단추로 클릭 하 고 **새로 만들기**를 선택 합니다. 새 RADIUS 클라이언트 대화 상자가 열립니다.

3. **이 RADIUS 클라이언트 사용** 확인란이 선택 되어 있는지 확인 합니다.

4. **이름**에 VPN 서버에 대 한 표시 이름을 입력 합니다.

5. **주소 (ip 또는 DNS)** 에 NAS IP 주소 또는 FQDN을 입력 합니다.
     
     FQDN을 입력 하는 경우 **확인** 을 선택 하 여 이름이 올바른지와 유효한 IP 주소에 매핑되는지 확인 합니다.

6. **공유 암호**에서 다음을 수행 합니다.

    1. **수동** 이 선택 되어 있는지 확인 합니다.

    2. VPN 서버에 입력 한 강력한 텍스트 문자열을 입력 합니다.

    3. 공유 암호 확인에서 공유 암호를 다시 입력 합니다.

7. **확인**을 선택합니다. VPN 서버가 NPS 서버에 구성 된 RADIUS 클라이언트 목록에 표시 됩니다.

## <a name="configure-nps-as-a-radius-for-vpn-connections"></a>VPN 연결을 위한 RADIUS로 NPS 구성

이 절차에서는 조직 네트워크에서 RADIUS 서버로 NPS를 구성 합니다. NPS에서는 특정 그룹의 사용자만 VPN 서버를 통해 조직/회사 네트워크에 액세스할 수 있도록 허용 하는 정책을 정의 하 고, PEAP 인증 요청에 유효한 사용자 인증서를 사용 하는 경우에만 정책을 정의 해야 합니다.

**여기서**

1. NPS 콘솔의 표준 구성에서 **전화 접속 또는 VPN 연결을 위한 RADIUS 서버** 가 선택 되어 있는지 확인 합니다.

2. **VPN 또는 전화 접속 구성**을 선택 합니다.
        
    VPN 구성 또는 전화 접속 마법사가 열립니다.

3. **VPN (가상 사설망) 연결**을 선택 하 고 **다음**을 선택 합니다.

4. 전화 접속 또는 VPN 서버 지정의 RADIUS 클라이언트에서 이전 단계에서 추가한 VPN 서버의 이름을 선택 합니다. 예를 들어 VPN 서버 NetBIOS 이름이 RAS1 인 경우 **RAS1**를 선택 합니다.

5. **다음**을 선택합니다.

6. 인증 방법 구성에서 다음 단계를 완료 합니다.

    1. **Microsoft Encrypted Authentication version 2 (MS-CHAPv2)** 확인란의 선택을 취소 합니다.

    2. 확장할 수 있는 **인증 프로토콜** 확인란을 선택 하 여 선택 합니다.

    3. 형식 (액세스 및 네트워크 구성 방법에 따라)에서 **Microsoft: PROTECTED EAP (PEAP)** 를 선택 하 고 **구성**을 선택 합니다.
      
        보호 된 EAP 속성 편집 대화 상자가 열립니다.

    4. 보안 된 암호 (EAP-MSCHAP v2) EAP 유형을 제거 하려면 **제거** 를 선택 합니다.

    5. **추가**를 선택합니다. EAP 추가 대화 상자가 열립니다.

    6. **스마트 카드 또는 기타 인증서**를 선택 하 고 **확인**을 선택 합니다.

    7. **확인** 을 선택 하 여 보호 된 EAP 속성 편집을 닫습니다.

7. **다음**을 선택합니다.

8. 사용자 그룹 지정에서 다음 단계를 완료 합니다.

    1. **추가**를 선택합니다. 사용자, 컴퓨터, 서비스 계정 또는 그룹 선택 대화 상자가 열립니다.

    2. **VPN 사용자**를 입력 하 고 **확인**을 선택 합니다.

    3. **다음**을 선택합니다.

9. IP 필터 지정에서 **다음**을 선택 합니다.

10. 암호화 설정 지정에서 **다음**을 선택 합니다. 변경 하지 마십시오.

    이러한 설정은이 시나리오에서 지원 하지 않는 Microsoft MPPE (지점 간 암호화) 연결에만 적용 됩니다.

11. 영역 이름 지정에서 **다음**을 선택 합니다.

12. **마침** 을 선택 하 여 마법사를 닫습니다.

## <a name="autoenroll-the-nps-server-certificate"></a>NPS 서버 인증서 자동 등록

이 절차에서는 로컬 NPS 서버에서 그룹 정책를 수동으로 새로 고칩니다. 그룹 정책 새로 고치면 인증서 자동 등록이 구성 되어 제대로 작동 하는 경우 로컬 컴퓨터는 CA (인증 기관)에 의해 인증서를 자동으로 등록 합니다.

>[!NOTE]  
>그룹 정책 도메인 구성원 컴퓨터를 다시 시작 하거나 사용자가 도메인 구성원 컴퓨터에 로그온 할 때 자동으로 새로 고쳐집니다. 또한 그룹 정책 정기적으로 새로 고쳐집니다. 기본적으로이 정기적인 새로 고침은 최대 30 분의 임의 오프셋으로 90 분 마다 발생 합니다.

멤버 자격이 **관리자**, 또는 이와 동등한 최소한이이 절차를 완료 합니다.

**여기서**

1. NPS에서 Windows PowerShell을 엽니다.

2. Windows PowerShell 프롬프트에서 입력 **gpupdate**, 한 다음 ENTER를 누릅니다.

## <a name="next-steps"></a>다음 단계

[5 단계. Always On VPN에 대 한 DNS 및 방화벽 설정 구성](vpn-deploy-dns-firewall.md):이 단계에서는 Windows PowerShell 또는 서버 관리자 역할 및 기능 추가 마법사를 사용 하 여 NPS (네트워크 정책 서버)를 설치 합니다. 또한 VPN 서버에서 받는 연결 요청에 대 한 모든 인증, 권한 부여 및 계정 의무를 처리 하도록 NPS를 구성 합니다.