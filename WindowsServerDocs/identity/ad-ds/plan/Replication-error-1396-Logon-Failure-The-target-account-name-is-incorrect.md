---
ms.assetid: 399a8bbe-3375-4bb0-b55b-5f46e7050028
title: 복제 오류 1396 로그온 실패 대상 계정 이름이 잘못됨
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ef3da06dd348b804f538d37cafbfabdd8bf45beb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844504"
---
# <a name="replication-error-1396-logon-failure-the-target-account-name-is-incorrect"></a>복제 오류 1396 로그온 실패 대상 계정 이름이 잘못됨

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


<developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd"> <introduction>
    <para>이 문서에서는 설명 증상, 원인 및 1396 Win32 오류로 인해 실패 한 Active Directory 복제 문제 해결 방법: "로그온 실패: 대상 계정 이름이 잘못 되었습니다. " </para>
    <list class="bullet">
      <listItem>
        <para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Symptoms">증상</link>
        </para>
      </listItem> <listItem>
        <para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Causes">원인</link>
        </para>
      </listItem> <listItem>
        <para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Resolutions">해결 방법</link>
        </para>
      </listItem>
    </list>
  </introduction>
  <section address="BKMK_Symptoms">
    <title>증상</title>
    <content>
      <para />
      <list class="ordered">
<listItem><para>오류 1396 사용 하 여 Active Directory 복제 테스트에 실패 한 DCDIAG 보고서: 로그온 실패: 대상 계정 이름이 잘못 되었습니다. "</para><code>Testing server: &lt;Site name&gt;&lt;DC Name&gt;
Starting test: Replications
[Replications Check,&lt;DC Name&gt;] A recent replication attempt failed:
From &lt;source DC&gt; to &lt;destination DC&gt;
Naming Context: CN=&lt;DN path of naming context&gt;
<codeFeaturedElement>The replication generated an error (1396):
Logon Failure: The target account name is incorrect.</codeFeaturedElement>
The failure occurred at &lt;date&gt; &lt;time&gt;.
The last success occurred at &lt;date&gt; &lt;time&gt;.
XX failures have occurred since the last success</code></listItem><listItem><para>REPADMIN 합니다. EXE는 1396 상태를 사용 하 여 마지막 복제 시도 실패 했음을 보고 합니다.</para><para>REPADMIN 1396 상태 포함 되지만 제한 되지는 않습니다 일반적으로 명시 하는 명령:</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><tbody><tr><TD><list class="bullet"><listItem><para>REPADMIN /ADD</para></listItem><listItem><para>REPADMIN /REPLSUM</para></listItem><listItem><para>REPADMIN /REHOST</para></listItem><listItem><para>REPADMIN /SHOWVECTOR /LATENCY</para></listItem></list></TD><TD><list class="bullet"><listItem><para>REPADMIN /SHOWREPS</para></listItem><listItem><para>REPADMIN /SHOWREPL</para></listItem><listItem><para>REPADMIN /SYNCALL</para></listItem></list></TD></tr></tbody></table><para>출력 "REPADMIN /SHOWREPS" CONTOSO-DC1 실패를 CONTOSO-d c 2에서 인바운드 복제를 보여 주는 예제는 "로그온 실패: 대상 계정 이름이 잘못 되었습니다. " 오류는 다음과 같습니다:</para><code>Default-First-Site-NameCONTOSO-DC1
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
</code></listItem><listItem><para>합니다 <ui>지금 복제</ui> Active Directory 사이트 및 서비스에서 명령이 반환 "로그온 실패: 대상 계정 이름이 잘못 되었습니다. "</para><para>원본 DC에서에서 연결 개체를 마우스 오른쪽 단추로 클릭 하 고 선택 <ui>지금 복제</ui> 실패 "로그온 실패: 대상 계정 이름이 잘못 되었습니다. " 화면에 나타나는 오류 메시지는 다음과 같습니다.</para><para>대화 상자 제목 텍스트:</para><para>이제 복제</para><para>대화 메시지 텍스트: </para><para>명명 컨텍스트를 동기화 하려고 하는 동안 다음 오류가 발생 했습니다 &lt;파티션 DNS 경로&gt; 도메인 컨트롤러 로부터 &lt;원본 DC&gt; 도메인 컨트롤러에 &lt;대상 DC&gt;: 로그온 실패: 대상 계정 이름이 올바르지 않습니다. 이 작업을 진행할 수 없습니다. </para></listItem><listItem><para>1396 상태와 함께 NTDS KCC, NTDS 일반 또는 Microsoft-Windows-ActiveDirectory_DomainService 이벤트는 이벤트 뷰어에서 디렉터리 서비스 로그에 기록 됩니다.</para><para>일반적으로 1396 상태를 명시 하는 active Directory 이벤트를 포함 하지만에 제한 되지 않습니다.</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><thead><tr><TD><para>이벤트 ID</para></TD><TD><para>이벤트 원본</para></TD><TD><para>이벤트 문자열</para></TD></tr></thead><tbody><tr><TD><para>1125</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Active Directory 도메인 서비스 설치 마법사 (Dcpromo) 다음 도메인 컨트롤러에 연결할 수 없습니다.</para></TD></tr><tr><TD><para>1645</para><para>이 이벤트는 세 부분으로 이루어진 SPN을 나열합니다.</para></TD><TD><para>NTDS 복제</para></TD><TD><para>대상 도메인 컨트롤러에 대해 사용하려는 SPN(서비스 사용자 이름)이 SPN을 확인하는 키 배포 센터(KDC) 도메인 컨트롤러에 등록되지 않았으므로 Active Directory가 인증된 원격 프로시저 호출(RPC)을 다른 도메인 컨트롤러에 수행하지 못했습니다.</para></TD></tr><tr><TD><para>1655</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Active Directory Domain Services가 다음 글로벌 카탈로그와 통신 하려고 하 고는 시도 되지 않았습니다.</para></TD></tr><tr><TD><para>2847</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>지식 일관성 검사기 로컬 읽기 전용 디렉터리 서비스에 대 한 복제 연결을 찾아 다음 디렉터리 서비스 인스턴스에 대해 원격으로 업데이트 하려고 합니다. 작업을 수행하지 못했습니다. 다시 시도 됩니다.</para></TD></tr><tr><TD><para>1925</para></TD><TD><para>NTDS KCC</para></TD><TD><para>다음 쓰기 가능한 디렉터리 파티션의 복제 링크를 설정 하려고 했으나 실패 했습니다.</para></TD></tr><tr><TD><para>1926</para></TD><TD><para>NTDS KCC</para></TD><TD><para>실패 하는 다음 매개 변수는 읽기 전용 디렉터리 파티션에 복제 링크를 설정 하려고 합니다.</para></TD></tr><tr><TD><para>5781</para></TD><TD><para>NETLOGON</para></TD><TD><para> 서버는 DNS에서 해당 이름을 등록할 수 없습니다.</para></TD></tr></tbody></table></listItem><listItem><para>DCPROMO 화면 오류로 인해 실패</para><para>대화 상자 제목 텍스트:</para><para>Active Directory 설치 하지 못했습니다.</para><para>대화 메시지 텍스트:</para><para>작업에 실패 했습니다. 디렉터리 서비스에서 CN에 대 한 서버 개체를 만들지 못했습니다 NTDS 설정, CN = ServerBeingPromoted, CN = Servers, CN = 사이트, CN = sites, CN = Configuration, DC = contoso, DC ReplicationSourceDC.contoso.com 서버의 = com입니다. </para><para>제공 된 네트워크 자격 증명에는 복제본을 추가 하려면 충분 한 액세스 권한이 있는지 확인 하십시오. </para><para>
"로그온 실패: 대상 계정 이름이 올바르지 않습니다. "</para><para>이 경우 이벤트 ID 1645, 1168, 및 1125 승격 되는 서버에 기록 됩니다.</para></listItem><listItem><para>사용 하 여 드라이브를 매핑할 <embeddedLabel>사용 하 여 net</embeddedLabel>:</para><code>C:&gt;net use z: &lt;server_name&gt;c$
System error 1396 has occurred.
Logon Failure: The target account name is incorrect.</code><para>이 경우에 시스템 이벤트 로그에서 이벤트 ID 333 로깅 서버 수 및 SQL Server와 같은 응용 프로그램에 대 한 높은 크기의 가상 메모리를 사용 하 여 합니다.</para></listItem><listItem><para>DC에 올바르지 않습니다.</para></listItem><listItem><para>KDC 시작 되지 않습니다 RODC에 krbtgt 계정 복원 후 rodc를 삭제 했습니다. 예를 들어, 복원 후 오류 1396 나타납니다. </para><para>
이벤트 ID 1645 RODC에 기록 됩니다. </para><para>
Dcdiag는 또한 RODC krbtgt 계정을 업데이트할 수 없다는 오류를 보고 합니다. </para></listItem>
</list>
    </content>
  </section>
  <section address="BKMK_Causes">
    <title>원인</title>
    <content>
      <para />
      <list class="ordered">
        <listItem>
          <para>SPN은 Kerberos를 사용 하 여 인증을 시도 하는 클라이언트를 대신 하 여 KDC에서 검색 하는 글로벌 카탈로그에 존재 하지 않습니다.</para>
          <para>Active Directory 복제의 컨텍스트에서 Kerberos 클라이언트 대상 DC를 SPN 조회를 수행 하는 KDC는 대상 DC 자체 것 이지만 원격 DC를 수 있습니다.</para>
        </listItem>
        <listItem>
          <para>사용자 또는 서비스 계정을 조회 되는 서비스 사용자 이름에 포함 해야 하는 대상 복제를 시도 하는 DC 대신 하 여 KDC에서 검색 하는 글로벌 카탈로그에 존재 하지 않습니다.</para>
          <para>Active Directory 복제의 컨텍스트에서 글로벌 카탈로그 DC에서 수행 하 고 대상 DC 인바운드 복제를 대신 하 여 검색에서 원본 DC 컴퓨터 계정이 존재 하지 않습니다.</para>
        </listItem>
        <listItem>
          <para>대상 DC에는 LSA 암호로 원본 Dc 도메인에 대 한 부족합니다.</para>
        </listItem>
        <listItem>
          <para>SPN 조회 되는 원본 DC 보다 다양 한 컴퓨터 계정에 존재 합니다.</para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_Resolutions">
    <title>해결 방법</title>
    <content>
      <list class="ordered">
        <listItem>
          <para>대상 DC NTDS 복제 이벤트 1645에 따라 디렉터리 서비스 이벤트 로그를 확인 하 고 다음에 유의 하세요.</para>
          <para>대상 DC의 이름</para>
          <para>조회 되는 SPN (E3514235-4B06-11D1-AB04-00C04FC2DCD2 /&lt;원본 Dc NTDS 설정 개체에 대 한 guid 개체&gt;/&lt;대상 도메인&gt;.&lt; tld&gt;@&lt;대상 도메인&gt;.&lt; tld&gt;</para>
          <para>대상 DC에서 사용 하 고 KDC</para>
        </listItem>
        <listItem>
          <para>1 단계에서 식별 하는 KDC의 콘솔에서 다음을 입력 합니다. </para>
          <code>nltest /dsgetdc &lt;forest root DNS domain name &gt; /gc</code>
          <para>대상 DC의 1396 오류로 실패 하는 복제 시도 직후 NLTEST 로케이터 테스트를 실행 합니다. </para>
          <para>이 대해 SPN 조회를 수행 하 고 KDC는 해당 GC를 식별 해야 합니다. </para>
          <para>GC는 kdc 검색 중인 Microsoft-Windows-ActiveDirectory_DomainService 이벤트 1655도 캡처할 수 있습니다.</para>
        </listItem>
        <listItem>
          <para>2 단계에서 발견 된 글로벌 카탈로그에 대해 1 단계에서 검색 된 SPN 검색 합니다.</para>
          <code>C:&gt;repadmin /showattr Server_Name DC=corp,DC=contoso,dc=com &lt;GC used by KDC&gt; &lt;DN path of forest root domain&gt; /filter:"(serviceprincipalname=&lt;SPN cited in the NTDS Replication event 1645&gt;)" /gc /subtree /atts:cn,serviceprincipalname</code>
          <para>또는</para>
          <code>C:&gt;dsquery * forestroot -scope subtree -filter "(serviceprincipalname=E3514235-4B06-11D1-AB04-00C04FC2DCD2/65cead9f-4949-46a3-a49a-f1fbfe13d2b3*)" -attr * -s Server_Name.europe.corp.contoso.com</code>
          <para>SPN에 대 한 호스트 개체가 있는지 확인 합니다.</para>
          <para>개체가 CNF / 충돌 손상 되었거나 lost and found 컨테이너 여부 호스트 개체를 포함 하는 것에 대 한 DN 경로 확인 합니다.</para>
          <para>원본 Dc 컴퓨터 계정에만 원본 Dc Active Directory 복제 SPN이 등록 되었는지 확인 합니다.</para>
          <para>복제 SPN가 없는 경우에 원본 DC가 자체를 사용 하 여 해당 SPN을 등록 하는 경우 및 단순 복제 대기 시간 또는 복제 오류로 인해 KDC에서 사용 하는 GC에서 누락 된 SPN이 있는지 여부를 결정 합니다.</para>
        </listItem>
        <listItem>
          <para>보안 채널 상태를 확인 하 고 상태를 신뢰 합니다.</para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics>
    <externalLink>
      <linkText>1396 오류로 실패 하는 Active Directory 작업 문제 해결: 로그온 실패: 대상 계정 이름이 올바르지 않습니다.</linkText>
      <linkUri>https://support.microsoft.com/kb/2183411/en-gb</linkUri>
    </externalLink>
  </relatedTopics>
</developerConceptualDocument>


