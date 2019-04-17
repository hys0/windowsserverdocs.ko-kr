---
ms.assetid: 399a8bbe-3375-4bb0-b55b-5f46e7050028
title: "복제 오류 1396 로그온 실패 대상 계정 이름을 잘못 되었습니다."
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 84799de26e1260f914d9b959357d5eed6fef62f6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="replication-error-1396-logon-failure-the-target-account-name-is-incorrect"></a>복제 오류 1396 로그온 실패 대상 계정 이름을 잘못 되었습니다.

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


<developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>이 문서는 증상에 설명 인과 해결 Active Directory 복제 1396 Win32 오류와 함께 실패 하는 방법: "로그온 실패: 대상 계정 이름이 정확 하지 않습니다." </para><list class="bullet"><listItem><para><link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Symptoms">증상</link></para></listItem><listItem><para><link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Causes">인해</link></para></listItem><listItem><para><link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Resolutions">해상도</link></para></listItem></list>
  </introduction>
  <section address="BKMK_Symptoms">
    <title>증상이</title>
    <content>
      <para />
      <list class="ordered">
<listItem><para>Active Directory 복제 테스트 1396 오류와 함께 실패 했다는 DCDIAG 보고서: 로그온 실패: 대상 계정 이름이 정확 하지 않습니다. " </para><code>Testing server: &lt;Site name&gt;&lt;DC Name&gt;
Starting test: Replications
[Replications Check,&lt;DC Name&gt;] A recent replication attempt failed:
From &lt;source DC&gt; to &lt;destination DC&gt;
Naming Context: CN=&lt;DN path of naming context&gt;
<codeFeaturedElement>The replication generated an error (1396):
Logon Failure: The target account name is incorrect.</codeFeaturedElement>
The failure occurred at &lt;date&gt; &lt;time&gt;.
The last success occurred at &lt;date&gt; &lt;time&gt;.
XX failures have occurred since the last success</code></listItem><listItem><para>REPADMIN 합니다. 마지막 시도한 복제 1396 상태로 실패 했다는 EXE 보고서 합니다. </para><para>일반적으로 1396 상태 인용 REPADMIN 명령 포함 되어 있지만에 국한 되지 않습니다.</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><tbody><tr><TD><list class="bullet"><listItem><para>REPADMIN /ADD</para></listItem><listItem><para>REPADMIN /REPLSUM</para></listItem><listItem><para>REPADMIN /REHOST</para></listItem><listItem><para>REPADMIN /SHOWVECTOR /LATENCY</para></listItem></list></TD><TD><list class="bullet"><listItem><para>REPADMIN /SHOWREPS</para></listItem><listItem><para>REPADMIN /SHOWREPL</para></listItem><listItem><para>REPADMIN 가져오는</para></listItem></list></TD></tr></tbody></table><para>CONTOSO d c 2의 인바인드 복제가와 실패 d-c 1 CONTOSO에 표시 "REPADMIN /SHOWREPS" 출력 샘플는 "로그온 실패: 대상 계정 이름이 올바른지." 오류는 다음과 같습니다:</para><code>Default-First-Site-NameCONTOSO-DC1
DSA Options: IS_GC 
Site Options: (none)
DSA object GUID: b6dc8589-7e00-4a5d-b688-045aef63ec01
DSA invocationID: b6dc8589-7e00-4a5d-b688-045aef63ec01
==== INBOUND NEIGHBORS ======================================
DC=contoso,DC=com
Default-First-Site-NameCONTOSO-DC2 via RPC
DSA object GUID: 74fbe06c-932c-46b5-831b-af9e31f496b2
Last attempt @ &lt;date&gt; &lt;time&gt; failed, <codeFeaturedElement>result 1396 (0x574):
Logon Failure: The target account name is incorrect.</codeFeaturedElement>
&lt;#&gt; consecutive failure(s).
Last success @ &lt;date&gt; &lt;time&gt;.
</code></listItem><listItem><para>는 <ui>지금 복제</ui> 명령 Active Directory 사이트 및 서비스에서 반환 "로그온 실패: 대상 계정 이름이 올바른지." </para><para>소스의 DC 연결 개체를 마우스 오른쪽 단추로 클릭 하 고 선택 <ui>지금 복제</ui> 실패 "로그온 실패: 대상 계정 이름이 올바른지." 오류 메시지는 다음과 같습니다 화면상:</para><para>대화 제목 텍스트:</para><para>지금 복제</para><para>대화 메시지 내용: </para><para>명명 컨텍스트를 동기화 하는 동안 다음과 같은 오류가 발생 한 &lt;파티션 DNS 경로&gt; 도메인 컨트롤러에서 &lt;DC 소스&gt; 도메인 컨트롤러에 &lt;대상 DC&gt;: 로그온 실패: 대상 계정 이름이 올바른지 합니다. 이 작업을 계속 하지 않습니다. </para></listItem><listItem><para>NTDS KCC, NTDS 일반 또는 Microsoft-Windows-ActiveDirectory_DomainService 이벤트 1396 상태 이벤트 뷰어에 디렉터리 서비스 로그에 기록 됩니다. </para><para>일반적으로 1396 상태 인용 active Directory 이벤트 포함 되어 있지만에 국한 되지 않습니다.</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><thead><tr><TD><para>이벤트 ID</para></TD><TD><para>이벤트 소스</para></TD><TD><para>이벤트 문자열</para></TD></tr></thead><tbody><tr><TD><para>1125</para></TD><TD><para>Microsoft에서 Windows-ActiveDirectory_DomainService</para></TD><TD><para>Active Directory Domain Services 설치 마법사 (Dcpromo) 다음 도메인 컨트롤러에 연결할 수 없습니다.</para></TD></tr><tr><TD><para>1645</para><para>이 이벤트 3 부 SPN 보여 줍니다.</para></TD><TD><para>NTDS 복제</para></TD><TD><para>대상 도메인 컨트롤러에 대 한 서비스를 원하는 사용자 이름 (SPN) SPN 문제를 해결 하는 키 메일 센터 (KDC) 도메인 컨트롤러에 등록 되지 않아 active Directory 다른 도메인 컨트롤러에 인증된 원격 프로시저 호출 RPC ()을 수행 하지 못했습니다.</para></TD></tr><tr><TD><para>1655</para></TD><TD><para>Microsoft에서 Windows-ActiveDirectory_DomainService</para></TD><TD><para>다음 드와 통신 하 려 Active Directory Domain Services 하 고 시도 되지 않았습니다.</para></TD></tr><tr><TD><para>2847</para></TD><TD><para>Microsoft에서 Windows-ActiveDirectory_DomainService</para></TD><TD><para>기술 일관성 검사 로컬 읽기 전용 디렉터리 서비스에 대 한 복제 연결 있으며 다음 디렉터리 서비스 인스턴스에 원격으로 업데이트 했습니다. 작업이 실패 했습니다. 다시 시도 합니다.</para></TD></tr><tr><TD><para>1925</para></TD><TD><para>NTDS KCC</para></TD><TD><para>다음 쓸 수 디렉터리 파티션에 대 한 복제 링크를 설정 하지 못했습니다.</para></TD></tr><tr><TD><para>1926</para></TD><TD><para>NTDS KCC</para></TD><TD><para>다음 매개 실패 읽기 전용 디렉터리 파티션에 복제 링크를 설정 하려고 합니다.</para></TD></tr><tr><TD><para>5781</para></TD><TD><para>NETLOGON</para></TD><TD><para> 서버 이름 DNS에 등록할 수 없습니다.</para></TD></tr></tbody></table></listItem><listItem><para>DCPROMO 화면 오류와 함께 실패</para><para>대화 제목 텍스트:</para><para>Active Directory 설치에 실패</para><para>메시지 대화 텍스트:</para><para>작업이 실패 한: 디렉터리 서비스 CN 서버 개체 만들려면 실패 CN NTDS 설정 = CN ServerBeingPromoted = = CN 서버 = 사이트, CN = CN 사이트 = 구성, DC DC contoso = ReplicationSourceDC.contoso.com 서버의 com = 합니다. </para><para>제공 네트워크 자격 증명 복제 추가 대 한 액세스 권한이 있는지 확인 합니다.</para><para> "로그온 실패: 대상 계정 이름이 정확 하지 않습니다." </para><para>이 경우 이벤트 ID 1645, 1168, 및 1125 올렸습니다 서버에 기록 됩니다. </para></listItem><listItem><para>지도 사용 하 여 드라이브를 <embeddedLabel>사용 net</embeddedLabel>:</para><code>C:&gt;net use z: &lt;server_name&gt;c$
System error 1396 has occurred.
Logon Failure: The target account name is incorrect.</code><para>이 이벤트 ID 333 이벤트 시스템 로그에 기록 서버 수 있는 경우 하 고 SQL Server 등의 응용 프로그램에 대 한 가상 메모리 높은 금액을 사용 합니다. </para></listItem><listItem><para>The DC 시간 잘못 되었습니다. </para></listItem><listItem><para>The KDC에 시작 되지 것입니다 RODC krbtgt 계정 복구 후 삭제 하는 rodc 합니다. 예를 들어 복원 후 1396 오류가 표시 됩니다. </para><para>이벤트 ID 1645 RODC에 기록 됩니다. </para><para>Dcdiag RODC krbtgt 계정을 업데이트할 수 없다는 오류 보고도 있습니다.</para></listItem>
</list>
    </content>
  </section>
  <section address="BKMK_Causes">
    <title>인해</title>
    <content>
      <para />
      <list class="ordered">
        <listItem>
          <para>The SPN 드 KDC Kerberos 사용 하 여 인증을 시도 클라이언트를 대표 하 여 검색에 존재 하지 않습니다.</para>
          <para>Active Directory 복제의 컨텍스트에서 Kerberos 클라이언트 대상 SPN 조회 수행 KDC DC 대상인 가능성이 자체 DC 이지만 원격 DC 될 수 있습니다.</para>
        </listItem>
        <listItem>
          <para>드 KDC DC 복제 하 고 목적지를 대표 하 여 검색에서 조회 사용자 이름 되는 서비스를 포함 해야 하는 사용자 또는 서비스 계정이 존재 하지 않습니다.</para>
          <para>Active Directory 복제의 컨텍스트에서 DC 컴퓨터 계정 소스 드 대상 DC 수행 인바인드 복제가 대신 DC로 검색에 존재 하지 않습니다.</para>
        </listItem>
        <listItem>
          <para>대상 DC 소스 Dc 도메인에 대 한 LSA 시크릿 부족 합니다.</para>
        </listItem>
        <listItem>
          <para>조회 되는 SPN 원본 DC 아닌 다른 컴퓨터 계정에 있습니다.</para>
        </listItem>
      </list>
    </content> 
  </section>
  <section address="BKMK_Resolutions">
    <title>해상도</title>
    <content>
      <list class="ordered">
        <listItem>
          <para>디렉터리 서비스 이벤트 로그온 대상 DC 1645 NTDS 복제 이벤트에 대 한 확인 하 고 다음:</para>
          <para>대상 DC 이름</para>
          <para>조회 The SPN 되 (E3514235-4B06-11D1-AB04-00C04FC2DCD2 /&lt;개체 소스 Dc NTDS 설정을 개체 guid&gt;/&lt;대상 도메인&gt;.&lt; tld&gt;@&lt;대상 도메인&gt;합니다. &lt;tld&gt;</para>
          <para>대상 DC에서 사용 되는 KDC</para>
        </listItem>
        <listItem>
          <para>1 단계에서 식별 KDC 콘솔에서 입력: </para>
          <code>nltest /dsgetdc &lt;forest root DNS domain name &gt; /gc</code>
          <para>바로 복제 시도 DC 대상에 1396 오류와 함께 실패 다음 NLTEST locator 테스트를 실행 합니다. </para>
          <para>이 KDC SPN 조회에 대해 수행 되는 GC 확인 해야 합니다. </para>
          <para>The GC KDC로 검색 되 고 Microsoft-Windows-ActiveDirectory_DomainService 이벤트 1655에에서도 캡처될 수 있습니다. </para>
        </listItem>
        <listItem>
          <para>2 단계에서 발견 된 드에 1 단계에서 발견 된 SPN 검색 합니다. </para>
          <code>C:&gt;repadmin /showattr Server_Name DC=corp,DC=contoso,dc=com &lt;GC used by KDC&gt; &lt;DN path of forest root domain&gt; /filter:"(serviceprincipalname=&lt;SPN cited in the NTDS Replication event 1645&gt;)" /gc /subtree /atts:cn,serviceprincipalname</code>
          <para>또는</para>
          <code>C:&gt;dsquery * forestroot -scope subtree -filter "(serviceprincipalname=E3514235-4B06-11D1-AB04-00C04FC2DCD2/65cead9f-4949-46a3-a49a-f1fbfe13d2b3*)" -attr * -s Server_Name.europe.corp.contoso.com</code>
          <para>spn 호스트 개체 있는지 확인 합니다. </para>
          <para>개체를 CNF / 충돌 손상 또는 분실 컨테이너에 여부 호스트 개체 등에 대 한 DN 경로 확인 합니다. </para>
          <para>소스 Dc Active Directory 복제 SPN만 소스 Dc 컴퓨터 계정에 등록 되어 있는지 확인 합니다. </para>
          <para>복제 SPN 누락 된 경우 확인 소스가 DC 자신과, 그 SPN 등록 SPN 간단한 복제 지연 또는 복제 오류 때문 KDC에서 사용 하는 GC에서 누락 된 여부. </para>
        </listItem>
        <listItem>
          <para>보안 채널 상태를 확인 하 고 건강 신뢰 합니다.</para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics>
    <externalLink>
      <linkText>1396 오류와 함께 실패 하는 문제를 해결 Active Directory 작업: 로그온 실패: 대상 계정 이름이 정확 하지 않습니다.</linkText>
      <linkUri>https://support.microsoft.com/kb/2183411/en-gb</linkUri>
    </externalLink>
  </relatedTopics>
</developerConceptualDocument>


