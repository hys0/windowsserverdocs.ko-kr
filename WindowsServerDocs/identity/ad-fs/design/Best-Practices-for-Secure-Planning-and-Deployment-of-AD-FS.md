---
ms.assetid: 963a3d37-d5f1-4153-b8d5-2537038863cb
title: "보안 및 배포 Adfs의에 대 한 유용한"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ed8c36d4bec455879ffd00ad40b72fd5e90484ab
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="best-practices-for-secure-planning-and-deployment-of-ad-fs"></a>보안 및 배포 Adfs의에 대 한 유용한

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목을 계획 하 고 보안 Active Directory Federation Services (ADFS) 배포 디자인할 때 평가 하는 데 도움이 모범 사례 정보를 제공 합니다. 이 항목을 검토 하 고 평가 전체적인 보안 Adfs의 사용에 영향을 주는 고려 시작 지점. 이 항목의 정보는 칭찬 기존 보안 계획 및 기타 디자인 모범 사례 확장을 위한 것입니다.  
  
## <a name="core-security-best-practices-for-ad-fs"></a>핵심 보안에 대 한 유용한 ADFS  
다음의 핵심 모범 사례 개선 하거나 디자인 또는 배포 보안 확장 하려는 모든 ADFS 설치 일반적인는 다음과 같습니다.  
  
-   **보안 구성 마법사를 사용 하 여 광고 FS 관련 보안에 대 한 유용한 정보 federation 서버와 federation 서버 프록시 컴퓨터에 적용할**  
  
    구성 SCW 보안 마법사 () Windows Server 2008, Windows Server 2008 R2 및 Windows Server 2012 컴퓨터에 사전 설치 된 제공 되는 도구입니다. 도움이 되는 유용한 하든지 서버 역할을 설치 하는 경우에 따라, 서버에 대 한 보안 적용 사용할 수 있습니다.  
  
    ADFS 설치할 경우 설치 프로그램이 만들어 역할 특정 ADFS 하는 서버 역할 (federation 서버 또는 federation 서버 프록시) 설치 중에 선택 하 게 적용 되는 보안 정책을 만드는 데 SCW로 사용할 수 있는 확장 파일  
  
    설치 된 각 역할 확장 파일 유형을 역할 및 각 컴퓨터 구성 된 하위 나타냅니다. 다음과 같은 역할 확장 파일 C:WindowsADFSScw 디렉터리에 설치 됩니다.  
  
    -   Farm.xml  
  
    -   SQLFarm.xml  
  
    -   StandAlone.xml  
  
    -   Proxy.xml (이 파일은 컴퓨터 federation 서버 프록시 역할으로 구성 된 경우에 제공 됩니다.)  
  
    SCW의 ADFS 역할 확장을 적용 하려면 순서 대로 다음 단계를 완료 합니다.  
  
    1.  ADFS 설치 하 고 해당 컴퓨터에 대 한 적절 한 서버 역할을 선택 합니다. 자세한 내용은 참조 [Federation 서비스 프록시 역할 서비스 설치](../../ad-fs/deployment/Install-the-Federation-Service-Proxy-Role-Service.md) AD FS 배포 가이드에 있습니다.  
  
    2.  Scwcmd 명령줄 도구를 사용 하 여 적절 한 역할 확장 파일을 등록 합니다. 이 도구를 사용 하 여 역할 컴퓨터 구성에 대 한 자세한 내용은 다음 표를 참조 하세요.  
  
    3.  명령 완료 된 것은 WindowssecurityMsscwLogs 디렉터리에 있는 SCWRegister_log.xml 파일을 검사 하 여 확인 합니다.  
  
    각 federation 서버 또는 광고 FS 기반 SCW 보안 정책이 적용 하려면 federation 서버 프록시 컴퓨터에서 모든이 단계를 수행 해야 합니다.  
  
    다음 표에서 ADFS 설치 된 컴퓨터에서 선택한 역할 ADFS 서버에 따라 적절 한 SCW 역할 확장 등록 하는 방법을 설명 합니다.  
  
    |광고 FS 서버 역할|ADFS 구성 데이터베이스 사용|명령 프롬프트에서 다음 명령을 입력 합니다.|  
    |---------------------|-------------------------------------|---------------------------------------------------|  
    |독립 실행형 federation 서버|Windows 내부 데이터베이스|`scwcmd register /kbname:ADFS2Standalone /kbfile:"WindowsADFSscwStandAlone.xml"`|  
    |Federation 팜 가입 서버|Windows 내부 데이터베이스|`scwcmd register /kbname:ADFS2Standalone /kbfile:"WindowsADFSscwFarm.xml"`|  
    |Federation 팜 가입 서버|SQL Server|`scwcmd register /kbname:ADFS2Standalone /kbfile:"WindowsADFSscwSQLFarm.xml"`|  
    |Federation 서버 프록시|해당 없음|`scwcmd register /kbname:ADFS2Standalone /kbfile:"WindowsADFSscwProxy.xml"`|  
  
    ADFS 함께 사용할 수 있는 데이터베이스에 대 한 자세한 내용은 참조 [AD FS 구성 데이터베이스의 The 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)합니다.  
  
-   **경우에는 보안 매우 중요 한 관심사 예를 들어, 단말기를 사용할 때 토큰 재생 검색을 사용 합니다.**  
    토큰 재생 검색 토큰 연합 서비스에는 요청을 재생할 하려고 감지 되 고 요청 삭제 되는 Adfs의 기능입니다. 토큰 재생 검색 기본적으로 활성화 됩니다. 동일한 토큰 두 번 이상 사용 하지 않도록 함으로써 WS Federation 수동 프로필 및 보안 설정 Markup 언어 (SAML) WebSSO 프로필에 대해 작동 합니다.  
  
    Federation 서비스를 시작 하는 실현 토큰 요청의 캐시 빌드 하기 시작 합니다. 시간이 지남에 따라 이후 토큰 요청 캐시를에 추가 되 Federation 서비스에 대 한 여러 번 토큰 요청을 재생 하려고를 감지 하는 기능 증가 합니다. 토큰 재생 검색을 사용 하지 않도록 설정 하 고 나중에 다시 사용 하도록 선택 하면 Federation 서비스 사용 된 이전에 재생 캐시 수 있는 시간이 충분 내용을 다시 시작할 때까지 된 시간 동안 토큰 허용 여전히 됩니다 기억 합니다. 자세한 내용은 참조 [AD FS 구성 데이터베이스의 The 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)합니다.  
  
-   **지원 SAML 아티팩트 해상도 사용 하는 경우에 특히 토큰 암호화를 사용 합니다.**  
  
    보안 및 ADFS 배포에 대해 시도할 수 있는 잠재적 남자 중간 (MITM) 공격 으로부터 보호를 강화 하기 위해 토큰 암호화는 것이 좋습니다. 사용 암호화를 사용 하 여 될 수 있습니다 영향을에 전체 하지만 일반적으로 것은 일반적으로 발견 되지 있고 많은 배포에서 보안을 강화에 대 한 혜택 초과 서버 성능이 비용이 합니다.  
  
    첫 번째 세트 토큰 암호화를 사용 하려면 신뢰 파티 신뢰 프로그램에 대 한 암호화 인증서를 추가 합니다. 신뢰를 파티에 의존 만들 때 중 하나는 한 암호화 인증서를 구성할 수 이상 합니다. 을 추가 하려면 한 암호화 인증서 나중에 기존 신뢰 파티 신뢰 하는 인증서 사용에 대 한에 설정할 수 있습니다의 **암호화** ADFS 스냅인 사용 하는 동안 신뢰 속성에서 탭 합니다. ADFS cmdlet 사용 하는 기존 보안에 대 한 인증서를 지정 하려면 EncryptionCertificate 매개 중 하나를 사용 하 여는 **설정 ClaimsProviderTrust** 또는 **설정 RelyingPartyTrust** cmdlet 합니다. 토큰 암호를 해독 때 사용 하 여 Federation 서비스에 대 한 인증서를 설정 하려면는 **설정 ADFSCertificate** cmdlet 지정 하 고 "`Token-Encryption`"에 대 한는 *CertificateType* 매개 합니다. 설정 및 특정 당사자에 대 한 암호화 해제 신뢰를 사용 하 여 편집할 수는 *EncryptClaims* 매개는 **설정 RelyingPartyTrust** cmdlet 합니다.  
  
-   **추가 보호 인증에 대 한 이용**  
  
    배포 보안을 위해 설정 고 Adfs로 인증 기능에 대 한 추가 보호 기능을 사용할 수 있습니다. 이 설정은 federation 서버에서 지 원하는 인증에 대 한 연장된 차단 수준을 지정 합니다.  
  
    인증에 대 한 연장된 보호를 공격자 클라이언트 자격 증명을 차단 하 고 서버에 전달 남자 중간 (MITM) 공격 으로부터 보호할 수 있습니다. 이러한 공격 으로부터 보호 기능을 통해는 채널 구속력 토큰 CBT () 하거나 될 수 있는 중 하나가 필요한, 허용 하는 클라이언트와의 커뮤니케이션을 설정할 때 서버에서 필요 하지 수 있게 됩니다.  
  
    사용 하 여 확장된 보호 기능을 사용 하려면는 **ExtendedProtectionTokenCheck** 매개에는 **설정 ADFSProperties** cmdlet 합니다. 다음 표에 가능한 값 설정과 값을 제공 하는 보안 수준에이 대 한 설명 되어 있습니다.  
  
    |매개 값|보안 수준|보호 설정|  
    |-------------------|------------------|----------------------|  
    |필요|서버를 완전히 강화 된 합니다.|추가 보호 적용 되며 언제 든 지 필요한 수도 있습니다.|  
    |허용|서버는 강화 된 부분입니다.|추가 보호 기능을 지 원하는 관련 된 시스템을 패치 적용 된 적용 됩니다.|  
    |없음|서버 취약입니다.|추가 보호 적용 되지 않습니다.|  
  
-   **로그인 및 추적을 사용 하는 경우 모든 중요 한 정보가의 개인 정보를 확인 합니다.**  
  
    ADFS 하거나 하지 않는, 기본적으로 제공 Federation 서비스의 정상적인 동작 일부로 직접 (PII) 개인 식별 정보를 추적 합니다. 하지만 이벤트 로깅 및 디버그 추적 로깅 활성화 되어 있으면 adfs에서, 일부 클레임 구성한 클레임 정책에 따라 유형과 관련 된 값 포함 될 수 있습니다 ADFS 이벤트 또는 추적 로그에 기록 될 수 있는 PII 합니다.  
  
    따라서 ADFS 구성 하 고 로그 파일에 액세스 제어 적용는 것이 좋습니다. 이러한 정보를 볼 수를 하지 않을 경우 loggin를 사용 하지 않도록 설정 하거나 필터링 PII 또는 중요 한 데이터가 로그에 다른 사용자와 공유 하기 전에 해야 합니다.  
  
    다음 팁 로그 파일의 콘텐츠 실수로 노출 되지 않도록 방지할 수 있습니다.  
  
    -   ADFS 이벤트 로그 및 추적 로그 파일에 액세스 해야 하는 신뢰할 수 있는 관리자만에 대 한 액세스를 제한 하는 액세스 제어 목록 (ACL)으로 보호 되 고 있는지 확인 합니다.  
  
    -   복사 하거나 로그 파일 파일 확장명 또는 웹 요청을 사용 하 여 쉽게 처리할 수 있는 경로 사용 하 여 보관 하지 않습니다. 예를 들어 파일 이름 확장명.xml 안전 선택을 않습니다. 제공 될 수 있는 확장의 목록을 보려면 정보 IIS (인터넷 서비스) 관리 가이드를 확인할 수 있습니다.  
  
    -   경로를 로그 파일을 수정 하는 경우 웹 브라우저를 사용 하 여 외부에서 액세스 하 않도록 웹 호스트 가상 루트 (vroot) 공개 디렉터리 외 있어야 하 고 로그 파일 위치에 대 한 명확 경로를 지정할 해야 합니다.  

-   **광고 FS 엑스트라넷 잠금 보호**  
    
    웹 응용 프로그램 프록시를 통해 제공 되는 invalid(bad) 암호를 사용 하 여 인증 요청의 형태로 공격이 발생할 경우 ADFS 익스트라넷 잠금 ADFS 계정 잠금에서 사용자가 보호할 수 있습니다. 계정 잠금 Adfs에서 사용자를 보호 하는 것 외에도, ADFS 익스트라넷 잠금도 무단 암호 추측 공격 으로부터 보호 합니다.  자세한 내용은 참조 [광고 FS 엑스트라넷 잠금 보호](../../ad-fs/operations/Configure-AD-FS-Extranet-Lockout-Protection.md)합니다.  
  
## <a name="sql-serverspecific-security-best-practices-for-ad-fs"></a>SQL Server 관련 보안에 대 한 유용한 ADFS  
이러한 데이터베이스 기술을 ADFS 디자인 및 배포에서 데이터를 관리 하는 데 사용 된 경우 다음과 같은 보안 유용한 Microsoft SQL Server® 또는 Windows 내부 데이터베이스 (WID)의 사용에 적용 됩니다.  
  
> [!NOTE]  
> 이러한 권장은 확장을 있지만 대체 하지 SQL Server 제품 보안 가이드 하기 위한 것입니다. 보안 SQL Server 설치 계획에 대 한 자세한 내용은 참조 [보안 SQL 설치에 대 한 보안 고려](https://go.microsoft.com/fwlink/?LinkID=139831) (https://go.microsoft.com/fwlink/?LinkID=139831).  
  
-   **항상 실제로 안전한 네트워크 환경에서 방화벽이 SQL Server을 배포 합니다.**  
  
    SQL Server 설치 하는 인터넷을 바로 노출 하지 않아야 합니다. 내 데이터 센터에 컴퓨터만 체결 ADFS 지 SQL server 설치 해야 합니다. 자세한 내용은 참조 [최적의 보안 관행 검사 목록](https://go.microsoft.com/fwlink/?LinkID=189229) (https://go.microsoft.com/fwlink/?LinkID=189229).  
  
-   **기본 제공 시스템 서비스 계정을 사용 하는 대신 서비스 계정 SQL Server 실행 합니다.**  
  
    기본적으로 SQL Server 자주 설치 되 고 구성 로컬 시스템 또는 NetworkService 계정 같이 지원 되는 기본 제공 된 시스템 계정 중 하나를 사용 하도록 합니다. Adfs SQL Server 설치의 보안을 강화 하려면 가능한 SQL Server 서비스에 액세스 하기 위해 별도 서비스 계정을 사용 장소와 Kerberos 인증 Active Directory 배포에는 보안 SPN (사용자 이름)이이 계정에 등록 하 여 사용 합니다. 이 통해 클라이언트 및 서버 간의 상호 인증 합니다. SPN 등록 별도 서비스 계정, 없이 SQL Server 사용할지 NTLM for Windows 기반 인증 클라이언트는 인증 합니다.  
  
-   **Surface 영역 SQL server를 최소화 하세요.**  
  
    필요한 SQL Server 끝점만 사용 하도록 설정 합니다. 기본적으로 SQL Server 제거할 수 없는 단일 기본 TCP 끝점을 제공 합니다. Adfs,이 TCP 끝점 Kerberos 인증에 사용 해야 합니다. 사용자 정의 추가 TCP 포트 SQL 설치에 추가 되는 현재 TCP 끝점을 검토 하기 위해 사용할 수 있습니다의 "선택 * sys.tcp_endpoints에서" 쿼리 (T SQL)이 세션의 문 합니다. SQL Server 끝점 구성에 대 한 자세한 내용은 참조 [How To: 다중 TCP 포트에서 수신 하는 데이터베이스 엔진 구성](https://go.microsoft.com/fwlink/?LinkID=189231) (https://go.microsoft.com/fwlink/?LinkID=189231).  
  
-   **SQL 기반 인증을 사용 하지 않습니다.**  
  
    텍스트로 암호 네트워크를 통해 전송 또는 구성 설정에서 암호를 저장 하면 Windows 인증 SQL Server 설치 있는 경우에 사용 하 여 하지 않아도 됩니다. SQL Server 인증 레거시 인증 하는 모드입니다. (SQL 사용자 이름 및 암호) 구조적 쿼리 SQL (언어) 로그인 자격 증명 저장을 사용 중인 경우 SQL Server 인증 권장 되지 않습니다. 자세한 내용은 참조 [인증 모드](https://go.microsoft.com/fwlink/?LinkID=189232) (https://go.microsoft.com/fwlink/?LinkID=189232).  
  
-   **추가 채널 보안 SQL 설치에서에 대 한 필요성을 신중 하 게 평가 합니다.**  
  
    Kerberos 인증 된도 실제로 SQL Server 보안 지원 공급자 Interface (SSPI) 제공 하지 않습니다 채널 수준 보안. 그러나 설치용 있는 서버 안전 하 게에 있는 방화벽으로 보호 된 네트워크 SQL 통신 암호화 되지 않을 수 있습니다 필요 합니다.  
  
    암호화 보안을 강화 하는 유용한 도구를 수 있지만 하지 않을 모든 데이터 나 연결에 대 한 간주 됩니다. 암호화를 구현할 것인지 결정할 때에 사용자가 데이터 액세스 하는 방법을 하는 것이 좋습니다. 사용자가 공개 네트워크를 통해 데이터를 액세스 데이터가 암호화 보안을 강화 하기 필요할 수 있습니다. 그러나 ADFS 하 여 SQL 데이터에 대 한 모든 액세스 관련 보안 인트라넷 구성 경우 암호화 되지 필요할 수 있습니다. 암호화를 사용 한다고 키, 암호, 인증서 유지 관리 전략을 포함 해야 합니다.  
  
    모든 SQL 데이터 볼 수 또는 드라이버를 변조 했는지 네트워크를 통해를 사용 하 여 인터넷 프로토콜 보안 또는 소켓 SSL (Secure Layer) 보안 SQL 연결 문제가 있는 경우 합니다. 그러나이 영향 되거나 경우도 ADFS 성능이 제한 될 수 있는 SQL Server 성능 저하를 할 수 있습니다. 예를 들어, SQL 기반 속성 스토어에서 특성 조회는 토큰 발급에 대 한 중요 한 하면 토큰 발급에서 ADFS 성능이 저하 될 수 있습니다. 더 강력한 주변 보안 구성 하 여 위협 변조 SQL 제거할 수 있습니다. 예를 들어, 더 나은 SQL Server 설치를 보호 하기 위한 방법은 사용자가 인터넷에 액세스할 수 없는 상태를 유지 하 고 컴퓨터와 하는 계속 사용자 또는 컴퓨터 datacenter 환경에만 액세스할 수 있습니다.  
  
    자세한 내용은 참조 [SQL Server에 대 한 암호화 연결](https://go.microsoft.com/fwlink/?LinkID=189234) 또는 [SQL Server 암호화](https://go.microsoft.com/fwlink/?LinkID=189233)합니다.  
  
-   **저장된 프로시저를 사용 하 여 모든 SQL 기반 조회 AD SQL FS 저장 된 데이터 하 여 수행 하 여 설계 된 안전 하 게 액세스를 구성 합니다.**  
  
    더 나은 서비스와 데이터를 격리를 제공 하려면 모든 특성 스토어 조회 명령에 대해 수 없도록 만들 수 있습니다. 데이터베이스 역할 있는 다음 권한을 부여 하면 실행할 수 없도록 만들 수 있습니다. 이 데이터베이스 역할을 FS Windows 광고 서비스의 서비스 id를 할당 합니다. 광고 FS Windows 서비스는 특성 조회 하는 데 사용 된 저장된 적절 한 프로시저 이외의 다른 SQL 문의 실행할 수 없습니다. 상승 공격 위험을 감소 SQL Server 데이터베이스 이런 방식에서에 대 한 액세스를 중지 합니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
