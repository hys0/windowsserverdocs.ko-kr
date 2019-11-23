---
ms.assetid: 399a8bbe-3375-4bb0-b55b-5f46e7050028
title: 복제 오류 1396 로그온 실패 대상 계정 이름이 잘못됨
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: a8af10fd54f557e4f4a2127dbd1cc178d53d93a4
ms.sourcegitcommit: 214847318401cebdcb7f1924a731b4439c9d8a24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/19/2019
ms.locfileid: "71402488"
---
# <a name="replication-error-1396-logon-failure-the-target-account-name-is-incorrect"></a>복제 오류 1396 로그온 실패 대상 계정 이름이 잘못됨

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


<developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd"> <introduction>
    <para>이 문서에서는 1396 오류: &quot;Logon 실패: 대상 계정 이름이 잘못 되어 Active Directory 복제 실패를 해결 하는 방법, 원인 및 해결 방법에 대해 설명 합니다.&quot; </para>
    <list class="bullet"> <listItem>
        <para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Symptoms">증상</link>
        </para>
      </listItem> <listItem>
        <para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Causes">
        </link></para>
      </listItem> <listItem>
        <para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Resolutions">해상도</link>
        </para>
      </listItem>
    </list>
  </introduction>
  <section address="BKMK_Symptoms">
    <title>증상</title>
    <content>
      <para />
      <list class="ordered">
<listItem><para>DCDIAG는 오류 1396: 로그온 실패: 대상 계정 이름이 잘못 되어 Active Directory 복제 테스트가 실패 한 것으로 보고 합니다.&quot;</para><code>Testing server: &lt;Site name&gt;&lt;DC Name&gt;
Starting test: Replications
[Replications Check,&lt;DC Name&gt;] A recent replication attempt failed:
From &lt;source DC&gt; to &lt;destination DC&gt;
Naming Context: CN=&lt;DN path of naming context&gt;
<codeFeaturedElement>The replication generated an error (1396):
Logon Failure: The target account name is incorrect.</codeFeaturedElement>
The failure occurred at &lt;date&gt; &lt;time&gt;.
The last success occurred at &lt;date&gt; &lt;time&gt;.
XX failures have occurred since the last success</code></listItem><listItem><para>REPADMIN. EXE는 마지막 복제 시도가 1396 상태와 함께 실패 한 것으로 보고 합니다.</para><para>일반적으로 1396 상태를 나타내는 REPADMIN 명령에는 다음이 포함 되지만이에 국한 되지 않습니다.</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><tbody><tr><TD><list class="bullet"><listItem><para>REPADMIN/ADD</para></listItem><listItem><para>REPADMIN/REPLSUM</para></listItem><listItem><para>REPADMIN/REHOST</para></listItem><listItem><para>REPADMIN/SHOWVECTOR/LATENCY</para></listItem></list></TD><TD><list class="bullet"><listItem><para>REPADMIN/SHOWREPS</para></listItem><listItem><para>REPADMIN/SHOWREPL</para></listItem><listItem><para>REPADMIN /SYNCALL</para></listItem></list></TD></tr></tbody></table><para>&quot;로그온 실패로 인해 CONTOSO-DC2에서 CONTOSO-DC1으로의 인바운드 복제를 보여 주는 &quot;REPADMIN/SHOWREPS&quot;의 샘플 출력: 대상 계정 이름이 올바르지 않습니다.&quot; 오류는 다음과 같습니다.</para><code>Default-First-Site-NameCONTOSO-DC1
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
</code></listItem><listItem><para>Active Directory 사이트 및 서비스의 <ui>지금 복제</ui> 명령은 &quot;로그온 실패를 반환 합니다. 대상 계정 이름이 잘못 되었습니다.&quot;</para><para>원본 DC에서 연결 개체를 마우스 오른쪽 단추로 클릭 하 고 <ui>지금 복제</ui> 를 선택 하면 &quot;로그온 실패: 대상 계정 이름이 올바르지 않습니다. 화면에 표시 되는 오류 메시지&quot; 다음과 같습니다.</para><para>대화 상자 제목 텍스트:</para><para>지금 복제</para><para>대화 메시지 텍스트: </para><para>도메인 컨트롤러 &lt;원본 DC&gt; 도메인 컨트롤러에서 도메인 컨트롤러로&gt; 파티션 DNS 경로 &lt;를 동기화 하는 동안 다음 오류가 발생 했습니다 &lt;: 로그온 실패: 대상 계정 이름이 잘못 되었습니다.&gt; 이 작업은 계속 되지 않습니다. </para></listItem><listItem><para>1396 상태를 포함 하는 ntds KCC, NTDS 일반 또는 Microsoft-Windows ActiveDirectory_DomainService 이벤트는 이벤트 뷰어의 디렉터리 서비스 로그에 기록 됩니다.</para><para>일반적으로 1396 상태를 명시 하는 Active Directory 이벤트에는 다음이 포함 되지만이에 국한 되지 않습니다.</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><thead><tr><TD><para>이벤트 ID</para></TD><TD><para>이벤트 원본</para></TD><TD><para>이벤트 문자열</para></TD></tr></thead><tbody><tr><TD><para>1125</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Active Directory Domain Services 설치 마법사 (Dcpromo)가 다음 도메인 컨트롤러와의 연결을 설정할 수 없습니다.</para></TD></tr><tr><TD><para>1645</para><para>이 이벤트는 세 부분으로 구성 된 SPN을 나열 합니다.</para></TD><TD><para>NTDS 복제</para></TD><TD><para>대상 도메인 컨트롤러에 대해 사용하려는 SPN(서비스 사용자 이름)이 SPN을 확인하는 키 배포 센터(KDC) 도메인 컨트롤러에 등록되지 않았으므로 Active Directory가 인증된 원격 프로시저 호출(RPC)을 다른 도메인 컨트롤러에 수행하지 못했습니다.</para></TD></tr><tr><TD><para>1655</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Active Directory Domain Services에서 다음 글로벌 카탈로그와 통신 하려고 시도 했지만 실패 했습니다.</para></TD></tr><tr><TD><para>2847</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>정보 일관성 검사기가 로컬 읽기 전용 디렉터리 서비스에 대 한 복제 연결을 찾아 다음 디렉터리 서비스 인스턴스에서 원격으로 업데이트 하려고 했습니다. 작업을 수행하지 못했습니다. 다시 시도 됩니다.</para></TD></tr><tr><TD><para>1925</para></TD><TD><para>NTDS KCC</para></TD><TD><para>다음 쓰기 가능한 디렉터리 파티션의 복제 링크를 설정 하려고 했으나 실패 했습니다.</para></TD></tr><tr><TD><para>1926</para></TD><TD><para>NTDS KCC</para></TD><TD><para>실패 하는 다음 매개 변수는 읽기 전용 디렉터리 파티션에 복제 링크를 설정 하려고 합니다.</para></TD></tr><tr><TD><para>5781</para></TD><TD><para>NETLOGON</para></TD><TD><para> 서버 이름을 DNS에 등록할 수 없습니다.</para></TD></tr></tbody></table></listItem><listItem><para>오류가 발생 하 여 DCPROMO가 실패 함</para><para>대화 상자 제목 텍스트:</para><para>Active Directory 설치 실패</para><para>대화 메시지 텍스트:</para><para>디렉터리 서비스가 서버 ReplicationSourceDC.contoso.com에서 CN = NTDS Settings, cn = ServerBeingPromoted, CN = Servers, CN = Site, CN = Sites, CN = Configuration, DC = contoso, DC = com에 대 한 서버 개체를 만들지 못했으므로 작업이 실패 했습니다. </para><para>제공 된 네트워크 자격 증명에 복제본을 추가할 수 있는 충분 한 액세스 권한이 있는지 확인 하세요. </para><para>
&quot;로그온 실패: 대상 계정 이름이 잘못 되었습니다. &quot;</para><para>이 경우 이벤트 ID 1645, 1168 및 1125은 승격할 서버에 기록 됩니다.</para></listItem><listItem><para><embeddedLabel>Net use</embeddedLabel>를 사용 하 여 드라이브를 매핑합니다.</para><code>C:&gt;net use z: &lt;server_name&gt;c$
System error 1396 has occurred.
Logon Failure: The target account name is incorrect.</code><para>이 경우 서버는 시스템 이벤트 로그에 이벤트 ID 333를 기록 하 고 SQL Server 같은 응용 프로그램에 대해 많은 양의 가상 메모리를 사용할 수도 있습니다.</para></listItem><listItem><para>DC 시간이 올바르지 않습니다.</para></listItem><listItem><para>RODC에 대 한 krbtgt 계정이 복원 된 후 삭제 된 rodc에서 KDC가 시작 되지 않습니다. 예를 들어 복원 후 오류 1396이 나타납니다. </para><para>
이벤트 ID 1645는 RODC에 기록 됩니다. </para><para>
또한 Dcdiag는 RODC krbtgt 계정을 업데이트할 수 없다는 오류를 보고 합니다. </para></listItem>
</list>
    </content>
  </section>
  <section address="BKMK_Causes">
    <title>
    <content>
      </title><para />
      <list class="ordered">
        <listItem>
          <para>SPN이 Kerberos를 사용 하 여 인증을 시도 하는 클라이언트를 대신 하 여 KDC에서 검색 한 글로벌 카탈로그에 없습니다.</para>
          <para>Active Directory 복제의 컨텍스트에서 Kerberos 클라이언트는 대상 DC입니다. SPN 조회를 수행 하는 KDC는 대상 DC 자체 이지만 원격 DC 일 수 있습니다.</para>
        </listItem>
        <listItem>
          <para>조회 되는 서비스 사용자 이름을 포함 해야 하는 사용자 또는 서비스 계정이 대상 DC를 대신 하 여 KDC에서 검색 한 글로벌 카탈로그에 없습니다.</para>
          <para>Active Directory 복제 컨텍스트에서 원본 DC 컴퓨터 계정은 인바운드 복제를 수행 하는 대상 DC 대신 DC에서 검색 한 글로벌 카탈로그에 존재 하지 않습니다.</para>
        </listItem>
        <listItem>
          <para>대상 DC에 원본 Dc 도메인에 대 한 LSA 암호가 없습니다.</para>
        </listItem>
        <listItem>
          <para>조회 중인 SPN이 원본 DC와 다른 컴퓨터 계정에 있습니다.</para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_Resolutions">
    <title>해결 방법</title>
    <content>
      <list class="ordered">
        <listItem>
          <para>대상 DC에서 NTDS 복제 이벤트 1645에 대 한 디렉터리 서비스 이벤트 로그를 확인 하 고 다음에 유의 하십시오.</para>
          <para>대상 DC의 이름</para>
          <para>조회 되는 SPN (E3514235-4B06-11D1-AB04-00C04FC2DCD2/&lt;&gt;원본 Dc NTDS 설정 개체에 대 한 개체 guid /&lt;대상 도메인&amp;amp; g t;&amp;amp; lt; tld&amp;amp; gt; @&lt;대상 도메인&gt;.&lt;&gt;</para>
          <para>대상 DC에서 사용 중인 KDC입니다.</para>
        </listItem>
        <listItem>
          <para>1 단계에서 식별 한 KDC의 콘솔에서 다음을 입력 합니다. </para>
          <code>nltest /dsgetdc &lt;forest root DNS domain name &gt; /gc</code>
          <para>대상 DC에서 1396 오류로 인해 실패 한 복제 시도 직후에 NLTEST 로케이터 테스트를 실행 합니다. </para>
          <para>KDC에서 SPN 조회를 수행 하는 GC를 식별 해야 합니다. </para>
          <para>KDC에서 검색 하는 GC가 Microsoft Windows-ActiveDirectory_DomainService 이벤트 1655에서 캡처될 수도 있습니다.</para>
        </listItem>
        <listItem>
          <para>2 단계에서 검색 한 글로벌 카탈로그에서 1 단계에서 검색 한 SPN을 검색 합니다.</para>
          <code>C:&gt;repadmin /showattr Server_Name DC=corp,DC=contoso,dc=com &lt;GC used by KDC&gt; &lt;DN path of forest root domain&gt; /filter:&quot;(serviceprincipalname=&lt;SPN cited in the NTDS Replication event 1645&gt;)&quot; /gc /subtree /atts:cn,serviceprincipalname</code>
          <para>또는</para>
          <code>C:&gt;dsquery * forestroot -scope subtree -filter &quot;(serviceprincipalname=E3514235-4B06-11D1-AB04-00C04FC2DCD2/65cead9f-4949-46a3-a49a-f1fbfe13d2b3*)&quot; -attr * -s Server_Name.europe.corp.contoso.com</code>
          <para>SPN에 대 한 호스트 개체가 있는지 확인 합니다.</para>
          <para>개체가 MY.CNF/충돌 하는지 여부를 포함 하 여 호스트 개체에 대 한 DN 경로를 확인 하거나 손실 및 발견 된 컨테이너에 상주 하는지 확인 합니다.</para>
          <para>원본 dc Active Directory 복제 SPN이 원본 Dc 컴퓨터 계정에만 등록 되어 있는지 확인 합니다.</para>
          <para>복제 SPN이 누락 된 경우 원본 DC가 자체 SPN을 등록 했는지 여부와 간단한 복제 대기 시간이 나 복제 실패로 인해 KDC에서 사용 하는 GC에 SPN이 없는지 여부를 확인 합니다.</para>
        </listItem>
        <listItem>
          <para>보안 채널 상태 및 신뢰 상태를 확인 합니다.</para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics>
    <externalLink> 
      <linkText>1396 오류로 인해 실패 하는 Active Directory 작업 문제 해결: 로그온 실패: 대상 계정 이름이 잘못 되었습니다.</linkText> 
      <linkUri><a href="https://support.microsoft.com/kb/2183411/en-gb" data-raw-source="https://support.microsoft.com/kb/2183411/en-gb">https://support.microsoft.com/kb/2183411/en-gb</a></linkUri> 
    </externalLink>
  </relatedTopics>
</developerConceptualDocument>


