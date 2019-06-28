---
ms.assetid: 0f21951c-b1bf-43bb-a329-bbb40c58c876
title: 복제 오류 1753 끝점 매퍼에서 사용할 수 있는 끝점이 더 이상 없음
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e7d2b47c9c14af22cdcf29fb388779e7639e38cb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442771"
---
# <a name="replication-error-1753-there-are-no-more-endpoints-available-from-the-endpoint-mapper"></a>복제 오류 1753 끝점 매퍼에서 사용할 수 있는 끝점이 더 이상 없음

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


<developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd"> <introduction>
    <para>이 항목에서는 증상, 원인 및 Active Directory 복제 오류 8524 The DSA 작업 DNS 조회 실패 때문에 계속할 수 없는 해결 하는 방법을 설명 합니다.</para>
    <list class="bullet">
      <listItem>
        <para>
          <link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_Symptoms">증상</link>
        </para>
      </listItem> <listItem>
        <para>
          <link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_Cause">Cause</link>
        </para>
      </listItem> <listItem>
        <para>
          <link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_Resolutions">해결 방법</link>
        </para>
      </listItem> <listItem>
        <para>
          <link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_MoreInfo">자세한 내용</link>
        </para>
      </listItem>
    </list>
  </introduction>
  <section address="BKMK_Symptoms">
    <title>증상</title>
    <content>
      <para>이 문서에서는 증상, 원인 설명 및 Win32 오류 1753 Active Directory 작업에 대 한 확인 단계: &quot;끝점 매퍼에서 사용할 수 있는 끝점이 더 이상 있습니다.&quot;</para>
      <list class="ordered">
        <listItem>
          <para>1753 오류로 실패 한 연결 테스트, Active Directory 복제 테스트 또는 KnowsOfRoleHolders 테스트 DCDIAG 보고서: &quot;끝점 매퍼에서 사용할 수 있는 끝점이 더 이상 있습니다.&quot;</para>
          <code>Testing server: &lt;site&gt;&lt;DC Name&gt;
Starting test: Connectivity
* Active Directory LDAP Services Check
* Active Directory RPC Services Check
[&lt;DC Name&gt;] <codeFeaturedElement>DsBindWithSpnEx() failed with error 1753,
There are no more endpoints available from the endpoint mapper..</codeFeaturedElement>
Printing RPC Extended Error Info:
Error Record 1, ProcessID is &lt;process ID&gt; (DcDiag) 
System Time is: &lt;date&gt; &lt;time&gt;
Generating component is 2 (RPC runtime)
Status is 1753: There are no more endpoints available from the endpoint mapper. Detection location is 500
NumberOfParameters is 4
Unicode string: ncacn_ip_tcp
Unicode string: &lt;source DC object GUID&gt;._msdcs.contoso.com
Long val: -481213899
Long val: 65537
Error Record 2, ProcessID is 700 (DcDiag) 
System Time is: &lt;date&gt; &lt;time&gt;
Generating component is 2 (RPC runtime)
<codeFeaturedElement>Status is 1753: There are no more endpoints available from the endpoint mapper.</codeFeaturedElement>
NumberOfParameters is 1
Unicode string: 1025
[Replications Check,&lt;DC Name&gt;] A recent replication attempt failed:
From &lt;source DC&gt; to &lt;destination DC&gt;
Naming Context: &lt;DN path of directory partition&gt;
The replication generated an error <codeFeaturedElement>(1753):
There are no more endpoints available from the endpoint mapper.</codeFeaturedElement> 
The failure occurred at &lt;date&gt; &lt;time&gt;.
The last success occurred at &lt;date&gt; &lt;time&gt;.
3 failures have occurred since the last success.
The directory on &lt;DC name&gt; is in the process.
of starting up or shutting down, and is not available.
Verify machine is not hung during boot.
</code>
        </listItem>
<listItem><para>REPADMIN 합니다. EXE 보고 1753 상태로 복제 시도가 실패 했습니다.</para><para>REPADMIN 1753 상태 포함 되지만 제한 되지는 않습니다 일반적으로 명시 하는 명령:</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><tbody><tr><TD><list class="bullet"><listItem><para>REPADMIN /REPLSUM</para></listItem><listItem><para>REPADMIN /SHOWREPL</para></listItem></list></TD><TD><list class="bullet"><listItem><para>REPADMIN /SHOWREPS</para></listItem><listItem><para>REPADMIN /SYNCALL</para></listItem></list></TD></tr></tbody></table><para>샘플 출력에서 &quot;REPADMIN /SHOWREPS&quot; CONTOSO-DC1 실패를 CONTOSO-d c 2에서 인바운드 복제를 보여 주는 합니다 &quot;복제 액세스가 거부 되었습니다&quot; 아래 오류가 표시 됩니다.</para><code>Default-First-Site-NameCONTOSO-DC1
DSA Options: IS_GC 
Site Options: (none)
DSA object GUID: b6dc8589-7e00-4a5d-b688-045aef63ec01
DSA invocationID: b6dc8589-7e00-4a5d-b688-045aef63ec01
==== INBOUND NEIGHBORS ======================================
DC=contoso,DC=com
Default-First-Site-NameCONTOSO-DC2 via RPC
DSA object GUID: 74fbe06c-932c-46b5-831b-af9e31f496b2
Last attempt @ &lt;date&gt; &lt;time&gt; failed, <codeFeaturedElement>result 1753 (0x6d9):
There are no more endpoints available from the endpoint mapper.</codeFeaturedElement>
&lt;#&gt; consecutive failure(s).
Last success @ &lt;date&gt; &lt;time&gt;.

</code></listItem><listItem><para>합니다 <ui>복제 토폴로지 확인</ui> Active Directory 사이트 및 서비스에서 명령이 반환 &quot;가지 끝점이 더 이상 끝점 매퍼에서 사용할 수 있습니다.&quot;</para><para>원본 DC에서에서 연결 개체를 마우스 오른쪽 단추로 클릭 하 고 선택 <ui>복제 토폴로지 확인</ui> 되면서 &quot;가지 끝점이 더 이상 끝점 매퍼에서 사용할 수 있습니다.&quot; 화면에 나타나는 오류 메시지는 다음과 같습니다.</para><para>대화 상자 제목 텍스트: 복제 토폴로지를 확인 합니다.</para><para>대화 메시지 텍스트: </para><para>도메인 컨트롤러에 연결 하는 동안 다음 오류가 발생 했습니다. 끝점 매퍼에서 사용할 수 있는 끝점이 더 이상 있습니다.</para></listItem><listItem><para>합니다 <ui>지금 복제</ui> Active Directory 사이트 및 서비스에서 명령이 반환 &quot;가지 끝점이 더 이상 끝점 매퍼에서 사용할 수 있습니다.&quot;</para><para>원본 DC에서에서 연결 개체를 마우스 오른쪽 단추로 클릭 하 고 선택 <ui>지금 복제</ui> 되면서 &quot;가지 끝점이 더 이상 끝점 매퍼에서 사용할 수 있습니다.&quot; 화면에 나타나는 오류 메시지는 다음과 같습니다.</para><para>대화 상자 제목 텍스트: 이제 복제</para><para>대화 메시지 텍스트: 명명 컨텍스트를 동기화 하려고 하는 동안 다음 오류가 발생 했습니다 &lt;% 디렉터리 파티션 이름&gt; 도메인 컨트롤러 로부터 &lt;원본 DC&gt; 도메인 컨트롤러에 &lt;대상 DC&gt;:</para><para>

끝점 매퍼에서 사용할 수 있는 끝점이 더 이상 있습니다.</para><para>작업을 진행할 수 없습니다.</para></listItem><listItem><para>-2146893022 상태와 함께 NTDS KCC, NTDS 일반 또는 Microsoft-Windows-ActiveDirectory_DomainService 이벤트는 이벤트 뷰어에서 디렉터리 서비스 로그에 기록 됩니다.</para><para>일반적으로-2146893022 상태를 명시 하는 active Directory 이벤트를 포함 하지만에 제한 되지 않습니다.</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><thead><tr><TD><para>이벤트 ID</para></TD><TD><para>이벤트 원본</para></TD><TD><para>이벤트 문자열</para></TD></tr></thead><tbody><tr><TD><para>1655</para></TD><TD><para>NTDS 일반</para></TD><TD><para>Active Directory가 다음 글로벌 카탈로그와 통신 하려고 하 고는 시도 되지 않았습니다.</para></TD></tr><tr><TD><para>1925</para></TD><TD><para>NTDS KCC</para></TD><TD><para>다음 쓰기 가능한 디렉터리 파티션의 복제 링크를 설정 하려고 했으나 실패 했습니다.</para></TD></tr><tr><TD><para>1265</para></TD><TD><para>NTDS KCC</para></TD><TD><para>지식 일관성 검사기 (KCC)에서 다음 디렉터리 파티션과 원본 도메인 컨트롤러에 대 한 복제 계약을 추가 하지 못했습니다.</para></TD></tr></tbody></table></listItem>
</list>
    </content>
  </section>
  <section address="BKMK_Cause">
    <title>Cause</title>
    <content>
      <para>아래 다이어그램에는 7 단계에서 클라이언트 응용 프로그램에 RPC 클라이언트에서 데이터를 전달 하려면 1 단계에서 RPC 끝점 매퍼 (EPM) 사용 하 여 서버 응용 프로그램의 등록을 사용 하 여 시작 RPC 워크플로를 보여 줍니다. </para>
      <para>&lt;ADDS_RPCWorkflow&gt;</para>
      <para>1 단계 7 맵을 통해 다음 작업을 합니다.</para>
      <list class="ordered">
        <listItem>
          <para>서버 앱 RPC 끝점 매퍼 (EPM)를 사용 하 여 해당 끝점을 등록 </para>
        </listItem>
        <listItem>
          <para>클라이언트는 RPC 호출 (사용자를 대신 하 여 OS 또는 응용 프로그램 시작 작업) </para>
        </listItem>
        <listItem>
          <para>클라이언트 쪽 RPC EPM 대상 컴퓨터에 연결 하 고 클라이언트 호출을 완료 하려면 끝점에 대 한 요청 </para>
        </listItem>
        <listItem>
          <para>서버 컴퓨터&#39;s EPM 끝점을 사용 하 여 응답 </para>
        </listItem>
        <listItem>
          <para>서버 앱을 연결 하는 클라이언트 쪽 RPC </para>
        </listItem>
        <listItem>
          <para>서버 앱 호출을 실행, RPC 클라이언트에 결과 반환 합니다. </para>
        </listItem>
        <listItem>
          <para>클라이언트 쪽 RPC 클라이언트 앱에 다시 결과 전달</para>
        </listItem>
      </list>
      <para>단계 #3 및 4 사이 오류로 인해 오류 1753 생성 됩니다. 특히 오류 1753는 RPC 클라이언트 (대상 DC)에서 포트 135 통해 RPC 서버 (원본 DC)에 연결할 수 있지만 (원본 DC) RPC 서버의 EPM 관심 RPC 응용 프로그램을 찾을 수 없습니다 및 서버 쪽 오류 1753 반환을 의미 합니다. 1753 오류는 RPC 클라이언트 (대상 DC) 응답을 받은 서버 쪽 오류 RPC 서버 (AD 복제 원본 DC)에서 네트워크를 통해 나타냅니다. </para>
      <para>1753 오류에 대 한 특정 근본 원인은 다음과 같습니다. </para>
      <list class="ordered">
        <listItem>
          <para>적이 서버 앱 (예: #1 단계는 &quot;자세한 내용은&quot; 다이어그램 위에 시도한 되지).</para>
        </listItem>
        <listItem>
          <para>서버 앱을 시작 했지만 RPC 끝점 매퍼를 사용 하 여 등록을 방해 하는 초기화 하는 동안 일부 오류가 발생 했습니다 (예: #1 단계는 &quot;자세한 내용은&quot; 위의 다이어그램 하려고 했지만 실패 했습니다).</para>
        </listItem>
        <listItem>
          <para>서버 앱을 시작 했지만 이후에 종료 합니다. (예: #1 단계는 &quot;자세한 내용은&quot; 위의 다이어그램 성공적으로 완료 했지만 완료 나중에 서버를 종료 하기 때문에).</para>
        </listItem>
        <listItem>
          <para>서버 앱을 수동으로 (의도적 이지만 3 비슷합니다 해당 끝점을 등록 취소. 희박 하지만 완전성을 위해 포함 됩니다.)</para>
        </listItem>
        <listItem>
          <para>RPC 클라이언트 (대상 DC) IP 매핑 오류 DNS, WINS 또는 호스트/Lmhosts 파일의 이름으로 인해 의도 된 것 이외의 다른 RPC 서버를 연결합니다.</para>
        </listItem>
      </list>
      <para>오류 1753 원인은 아닙니다. </para>
      <list class="bullet">
        <listItem>
          <para>포트 135 통해 RPC 클라이언트 (대상 DC)와 RPC 서버 (원본 DC) 간에 네트워크 연결이 부족</para>
        </listItem>
        <listItem>
          <para>RPC 서버 (원본 DC) 간에 네트워크 연결이 부족 하면 포트 135 및 RPC 클라이언트 (대상 DC)를 사용 하 여 사용 후 삭제 포트를 통해. </para>
        </listItem>
        <listItem>
          <para>암호가 일치 하지 않습니다 또는 Kerberos 암호 해독 원본 DC에서 하지 못하는 암호화 패킷 </para>
        </listItem>
      </list>
      <para> </para>
    </content>
  </section>
  <section address="BKMK_Resolutions">
    <title>해결 방법</title>
    <content>
      <list class="ordered">
        <listItem>
          <para>
            <embeddedLabel>끝점 매퍼를 사용 하 여 해당 서비스를 등록 하는 서비스가 시작 되었는지 확인</embeddedLabel>
          </para>
          <para>Windows 2000 및 Windows Server 2003 Dc: 원본 DC를 표준 모드로 부팅 되는 확인 합니다. </para>
          <para>
Windows Server 2008 또는 Windows Server 2008 R2에 대 한: 원본 DC의 콘솔에서 서비스 관리자 (services.msc)를 시작 하 고 있는지 확인 합니다 <embeddedLabel>Active Directory Domain Services</embeddedLabel> 서비스가 실행 되 고 있습니다. </para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>의도 한 RPC 서버 (원본 DC)에 연결 하는 RPC 클라이언트 (대상 DC)를 확인 합니다.</embeddedLabel>
          </para>
          <para>일반적인 Active Directory 포리스트에서 모든 Dc _msdcs에서 CNAME 레코드는 도메인 컨트롤러를 등록합니다. &lt;포리스트 루트 도메인&gt; 도메인 포리스트 내에 있는 것에 관계 없이 DNS 영역입니다. DC CNAME 레코드에서 파생 되는 <embeddedLabel>objectGUID</embeddedLabel> 각 도메인 컨트롤러에 대 한 NTDS 설정 개체의 특성입니다. </para>
          <para>복제 기반 작업을 수행할 때 대상 DC를 원본 Dc CNAME 레코드에 대 한 DNS 쿼리 합니다. CNAME 레코드는 원본 Dc IP 주소를 파생 하는 데 사용 되는 원본 DC 정규화 된 컴퓨터 이름을 포함 DNS 클라이언트 캐시 조회를 통해 호스트 / LMHost 파일 조회, 호스트 A / AAAA 레코드 DNS 또는 WINS에 있습니다. </para>
          <para>NTDS 설정 개체를 부실 하 고 DNS, WINS, 호스트 및 LMHOST 파일에 잘못 된 이름-IP 매핑이 잘못 된 RPC 서버 (원본 DC)에 연결할 RPC 클라이언트 (대상 DC) 발생할 수 있습니다. 또한 잘못 된 이름-IP 매핑 대상 (이 경우 Active Directory 역할) 설치의 RPC 서버 응용 프로그램이 없는 컴퓨터에 연결할 RPC 클라이언트 (대상 DC) 발생할 수 있습니다. (예: DC2에 대 한 오래 된 호스트 레코드 DC3 또는 멤버 컴퓨터의 IP 주소를 포함). </para>
          <para>Active Directory의 대상 Dc 복사본에에서 있는 원본 DC에 대 한 objectGUID 원본 Active Directory Dc 복사본에에서 저장 된 원본 DC objectGUID 일치 하는지 확인 합니다. 일치 하지 않는 경우를 사용 하 여 repadmin /showobjmeta ntds 설정 개체에 해당 하는 원본 DC의 마지막 프로 모션을 참조 하세요. (힌트: 마지막 프로 모션 날짜에 대해 /showobjmeta에서 만든 날짜 NTDS 설정 개체에 대 한 날짜 스탬프를 비교 합니다 원본 Dc dcpromo.log 파일입니다. 마지막으로 수정 / DCPROMO의 만든 날짜를 해야 합니다. 로그 파일 자체)입니다. 개체 Guid 동일 하지 않은 경우 대상 DC 가능성이 부실 NTDS 설정 개체를 원본 DC에 대 한 IP 매핑에 잘못 된 이름으로 호스트 레코드를 해당 CNAME 레코드가 참조에 있습니다. </para>
          <para>대상 DC에서 실행 IPCONFIG /ALL DNS 서버를 확인 하려면 DC 이름 확인을 위해 사용 하는 대상:</para>
          <code>c:&gt;ipconfig /all</code>
          <para>대상 DC에서 원본 Dc 정규화 된 DC CNAME 레코드에 대해 NSLOOKUP을 실행 합니다.</para>
          <code>c:&gt;nslookup -type=cname &lt;fully qualified cname of source DC&gt; &lt;destination DCs primary DNS Server IP &gt;
c:&gt;nslookup -type=cname &lt;fully qualified cname of source DC&gt; &lt;destination DCs secondary DNS Server IP&gt;</code>
          <para>NSLOOKUP 반환한 IP 주소를 확인 &quot;소유&quot; 호스트 이름 / 원본 DC의 보안 id:</para>
          <code>C:&gt;NBTSTAT -A &lt;IP address returned by NSLOOKUP in the step above&gt;</code>
          <para>로 구분하거나 여러</para>
          <para>원본 DC로 실행의 콘솔에 로그온 &quot;IPCONFIG&quot; CMD에서 메시지를 표시 하 고 원본 DC 위의 NSLOOKUP 명령에서 반환 된 IP 주소를 소유 하는지 확인</para>
          <para>오래 된 / 중복 IP 매핑 DNS에서 호스트에 대 한 확인</para>
          <code>NSLOOKUP -type=hostname &lt;single label hostname of source DC&gt; &lt;primary DNS Server IP on destination DC&gt;
NSLOOKUP -type=hostname &lt;single label hostname of source DC&gt; &lt;secondary DNS Server IP on destination DC&gt;

NSLOOKUP -type=hostname &lt;fully qualified computer name of source DC&gt; &lt;primary DNS Server IP on destination DC&gt;
NSLOOKUP -type=hostname &lt;fully qualified computer name of source DC&gt; &lt;secondary DNS Server IP on dest. DC&gt;</code>
<para>잘못 된 IP 주소가 호스트 레코드에 있는 경우 조사 여부를 DNS 청소 기능을 활성화 하 고 올바르게 구성 합니다. </para><para>위의 테스트 또는 네트워크 추적 하지 않습니다 하는 경우&#39;표시 안 잘못 된 IP 주소를 반환 하 여 이름 쿼리는 호스트 파일, LMHOSTS 파일 및 WINS 서버에서 부실 항목 것이 좋습니다. 참고 WINS 대체 (fallback) 이름 확인을 수행 하려면 DNS 서버를 구성할 수도 있습니다.</para>
</listItem>
        <listItem>
          <para>
            <embeddedLabel>RPC 서버 (원본 DC)에 끝점 매퍼를 사용 하 여 서버 응용 프로그램 (Active Directory et al)에 등록 되었는지 확인</embeddedLabel>
          </para>
          <para>Active Directory는 다양 한 잘 알려진 및 동적으로 등록 된 포트를 사용합니다. 이 표에서 잘 알려진 포트 및 Active Directory 도메인 컨트롤러에서 사용 되는 프로토콜을 나열 합니다.</para>
          <table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>RPC 서버 응용 프로그램</para>
                </TD>
                <TD>
                  <para>Port</para>
                </TD>
                <TD>
                  <para>TCP</para>
                </TD>
                <TD>
                  <para>UDP</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>DNS 서버</para>
                </TD>
                <TD>
                  <para>53</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Kerberos</para>
                </TD>
                <TD>
                  <para>88</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>LDAP 서버</para>
                </TD>
                <TD>
                  <para>389</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Microsoft-DS</para>
                </TD>
                <TD>
                  <para>445</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>LDAP SSL</para>
                </TD>
                <TD>
                  <para>636</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>글로벌 카탈로그 서버</para>
                </TD>
                <TD>
                  <para>3268</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
                <TD>
                  <para />
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>글로벌 카탈로그 서버</para>
                </TD>
                <TD>
                  <para>3269</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
                <TD>
                  <para />
                </TD>
              </tr>
            </tbody>
          </table>
          <para>잘 알려진 포트 끝점 매퍼를 사용 하 여 등록 되지 않습니다. </para>
          <para>Active Directory 및 기타 응용 프로그램 RPC 사용 후 삭제 포트 범위에서 동적으로 할당 된 포트를 수신 하는 서비스를 등록할 수도 있습니다. 이러한 RPC 서버 응용 프로그램은 1024-5000 Windows 2000 및 Windows Server 2003 컴퓨터에서 TCP 포트 및 Windows Server 2008 및 Windows Server 2008 R2 컴퓨터에서 49152와 65535 범위의 포트에 동적으로 할당 됩니다. 복제에서 사용 되는 RPC 포트 수 하드 코드 된에서 설명 하는 단계를 사용 하 여 레지스트리에 <externalLink> <linkText>기술 자료 문서 224196</linkText> <linkUri> <a href="https://support.microsoft.com/kb/224196" data-raw-source="https://support.microsoft.com/kb/224196"> https://support.microsoft.com/kb/224196 </a> </linkUri> </externalLink>. Active Directory 하드 코드 된 포트를 사용 하도록 구성 된 경우 EPM을 사용 하 여 등록을 계속 합니다. </para>
          <para>관심 RPC 서버 응용 프로그램이 등록 된 RPC 서버 (원본 DC AD 복제의 경우)의 RPC 끝점 매퍼를 확인 합니다. </para>
          <para>이 작업을 수행 하는 방법의 수는 있지만 하나 설치 하 고 원본 DC의 구문을 사용 하 여 콘솔에서 관리자 권한 CMD 프롬프트에서 PORTQRY를 실행 하는 것: </para>
          <code>c:&amp;gt;portquery -n &lt;source DC&gt; -e 135 &gt;file.txt</code>
          <para>Portqry 출력에 의해 동적으로 등록 된 포트 번호를 확인 합니다 &quot;MS NT 디렉터리 DRS 인터페이스&quot; (UUID 351... =)에 대 한 합니다 <embeddedLabel>ncacn_ip_tcp 프로토콜</embeddedLabel>합니다. 아래 코드 조각은 Windows Server 2008 R2 DC를 UUID portquery 출력 예제를 보여 줍니다. / Active Directory에서 특별히 사용 되는 프로토콜 쌍으로 강조 표시 <embeddedLabel>굵게</embeddedLabel>: </para>
          <code>UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_np:CONTOSO-DC01[\pipe\lsass] 
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_np:CONTOSO-DC01[\PIPE\protected_storage] 
<codeFeaturedElement>UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_ip_tcp:CONTOSO-DC01[49156]</codeFeaturedElement> 
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_http:CONTOSO-DC01[49157] 
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_http:CONTOSO-DC01[6004]</code>
          <para />
        </listItem>
        <listItem>
          <para>이 오류를 해결 하는 다른 가능한 방법:</para>
          <list class="ordered">
            <listItem>
              <para>원본 DC 표준 모드로 부팅 되는 원본 DC에서 OS 및 DC 역할을 완벽 하 게 시작 하 고 확인 합니다.</para>
            </listItem>
            <listItem>
              <para>Active Directory 도메인 서비스를 실행 중인지 확인 합니다. 서비스가 현재 중지 되어 기본 시작 값으로 구성 되지 않았습니다, 기본 시작 값 다시 설정, 수정 된 DC를 다시 부팅 경우 작업을 다시 시도 합니다.</para>
            </listItem>
            <listItem>
              <para>RPC 서비스 RPC 로케이터에 대 한 시작 값 및 서비스 상태를 RPC 클라이언트 (대상 DC) 및 RPC 서버 (원본 DC)의 OS 버전에 대해 올바른지 확인 합니다. 서비스가 현재 중지 되어 기본 시작 값으로 구성 되지 않았습니다, 기본 시작 값 다시 설정, 수정 된 DC를 다시 부팅 경우 작업을 다시 시도 합니다.</para>
              <para>또한 서비스 컨텍스트에 다음 표에 나열 된 기본 설정을 일치 하는지 확인 합니다.</para>
              <table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11">
                <thead>
                  <tr>
                    <TD>
                      <para>서비스</para>
                    </TD>
                    <TD>
                      <para>기본 상태 (시작 유형)에서 Windows Server 2003 이상 </para>
                    </TD>
                    <TD>
                      <para>Windows Server 2000에서 기본 상태 (시작 형식)</para>
                    </TD>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <TD>
                      <para>원격 프로시저 호출</para>
                    </TD>
                    <TD>
                      <para>시작 (자동)</para>
                    </TD>
                    <TD>
                      <para>시작 (자동)</para>
                    </TD>
                  </tr>
                  <tr>
                    <TD>
                      <para>원격 프로시저 호출 로케이터</para>
                    </TD>
                    <TD>
                      <para>Null 또는 중지 (수동)</para>
                    </TD>
                    <TD>
                      <para>시작 (자동)</para>
                    </TD>
                  </tr>
                </tbody>
              </table>
            </listItem>
            <listItem>
              <para>동적 포트 범위의 크기를 제한 되지를 확인 합니다. RPC 포트 범위를 열거 하는 Windows Server 2008 및 Windows Server 2008 R2 NETSH 구문은 다음과 같습니다.</para>
              <code>&gt;netsh int ipv4 show dynamicport tcp
&gt;netsh int ipv4 show dynamicport udp
&gt;netsh int ipv6 show dynamicport tcp
&gt;netsh int ipv6 show dynamicport udp</code>
            </listItem>
            <listItem>
              <para>원본 Dc OS 버전에 대해 동적 포트 범위 내에 하드 코드 된 포트 정의 KB 224196에 정의 된가 속한 확인 합니다.</para>
              <para>검토 <externalLink> <linkText>기술 자료 문서 224196</linkText> <linkUri> <a href="https://support.microsoft.com/kb/224196" data-raw-source="https://support.microsoft.com/kb/224196"> https://support.microsoft.com/kb/224196 </a> </linkUri> </externalLink> 하드 코드 된 포트에 대 한 임시 포트 범위에 속하는지 확인 합니다. 원본 DC&#39;s 운영 체제 버전입니다.</para>
            </listItem>
            <listItem>
              <para>ClientProtocols 키 HKLM\Software\Microsoft\Rpc 아래 있고 다음 5 개 기본 값이 들어 있는지 확인 합니다.</para>
              <code>ncacn_http REG_SZ rpcrt4.dll
ncacn_ip_tcp REG_SZ rpcrt4.dll
<codeFeaturedElement>ncacn_nb_tcp REG_SZ rpcrt4.dll</codeFeaturedElement>
ncacn_np REG_SZ rpcrt4.dll
ncacn_ip_udp REG_SZ rpcrt4.dll</code>
            </listItem>
          </list>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_MoreInfo">
    <title>자세한 내용</title>
    <content>
      <para>
        <embeddedLabel>매핑-2146893022 및 발생 시키는 RPC 오류 1753 IP에 잘못 된 이름의 예: 대상 사용자 이름이 올바르지 않습니다.</embeddedLabel>
      </para>
      <para>IP 주소 x.x.1.1와 x.x.1.2 DC1과 DC2의 contoso.com 도메인 구성 됩니다. 호스트 &quot;A&quot; / &quot;AAAA&quot; DC2에 대 한 레코드는 모든 DC1에 대해 구성 된 DNS 서버에 올바르게 등록 합니다. 또한 DC1에서 호스트 파일 DC2s 정규화 된 호스트 이름 IP 주소 x.x.1.2 매핑 항목을 포함 합니다. 나중에, DC2&#39;의 IP 주소에서 X.X.1.2 X.X.1.3 바뀌고 구성원 컴퓨터는 새 IP 주소 x.x.1.2 사용 하 여 도메인에 가입 되어 있습니다. AD 복제 시도 의해 트리거되는 <ui>지금 복제</ui> 추적 아래에 표시 된 것과 같이 Active Directory 사이트 및 서비스 스냅인에서 명령을 1753 오류로 인해 실패 합니다.</para>
      <code>F# SRC    DEST    Operation 
1 x.x.1.1 x.x.1.2 ARP:Request, x.x.1.1 asks for x.x.1.2
2 x.x.1.2 x.x.1.1 ARP:Response, x.x.1.2 at 00-13-72-28-C8-5E
3 x.x.1.1 x.x.1.2 TCP:Flags=......S., SrcPort=50206, DstPort=DCE endpoint resolution(135)
4 x.x.1.2 x.x.1.1 ARP:Request, x.x.1.2 asks for x.x.1.1
5 x.x.1.1 x.x.1.2 ARP:Response, x.x.1.1 at 00-15-5D-42-2E-00
6 x.x.1.2 x.x.1.1 TCP:Flags=...A..S., SrcPort=DCE endpoint resolution(135)
7 x.x.1.1 x.x.1.2 TCP:Flags=...A...., SrcPort=50206, DstPort=DCE endpoint resolution(135)
8 x.x.1.1 x.x.1.2 MSRPC:c/o Bind: UUID{E1AF8308-5D1F-11C9-91A4-08002B14A0FA} EPT(EPMP) 
9 x.x.1.2 x.x.1.1 MSRPC:c/o Bind Ack: Call=0x2 Assoc Grp=0x5E68 Xmit=0x16D0 Recv=0x16D0 
<codeFeaturedElement>10</codeFeaturedElement> x.x.1.1 x.x.1.2 EPM:Request: ept_map: NDR, DRSR(DRSR) {E3514235-4B06-11D1-AB04-00C04FC2DCD2} [DCE endpoint resolution(135)]
<codeFeaturedElement>11</codeFeaturedElement> x.x.1.2 x.x.1.1 EPM:Response: ept_map: 0x16C9A0D6 - EP_S_NOT_REGISTERED
</code>
      <para>프레임 <embeddedLabel>10</embeddedLabel>, 대상 DC UUID E351 Active Directory 복제 서비스 클래스에 대 한 포트 135 통해 원본 Dc 종점 매퍼를 쿼리 하는 중... </para>
      <para>프레임에서 <embeddedLabel>11</embeddedLabel>, 원본 DC,이 경우 DC 역할을 아직 호스트 하지 않습니다는 E351 등록 되지 않았습니다 하는 구성원 컴퓨터 중... UUID 기호화 된 10 진수 오류 1753 년에 매핑되는 EP_S_NOT_REGISTERED 오류로 응답 하는 해당 로컬 EPM 사용 하 여 복제 서비스에 대 한 16 진수 오류 0x6d9 및 친숙 한 오류 &quot;끝점 매퍼에서 사용할 수 있는 끝점이 더 이상 가지&quot; .</para>
      <para>IP 주소 x.x.1.2 멤버 컴퓨터 복제본으로 승격 될 나중 &quot;MayberryDC&quot; contoso.com 도메인의 합니다. 다시 합니다 <ui>지금 복제</ui> 복제를 트리거하려면 명령을 사용 하지만이 이번와 함께 실패는 화면의 오류 &quot;대상 사용자 이름이 올바르지 않습니다.&quot; 해당 네트워크 어댑터 IP 할당은 한 컴퓨터 주소 x.x.1.2 <placeholder>는</placeholder> 도메인 컨트롤러를 현재 표준 모드로 부팅 되 고 E351를 등록 하는 중... 복제 서비스는 로컬 EPM 것 같지만 UUID DC2의 이름 또는 보안 id를 소유 하지 않는 한 요청은 이제 오류로 실패 DC1에서 Kerberos 요청을 암호 해독할 수 없습니다 &quot;대상 사용자 이름이 올바르지 않습니다.&quot; 오류 10 진수 오류-2146893022 매핑됩니다 오류 0x80090322 hex /입니다. </para>
      <para>이러한 잘못 된 호스트 IP 매핑 호스트에서 부실 항목으로 발생할 수 있습니다 / lmhost 파일인 호스트 A / AAAA DNS 또는 WINS 등록 합니다. </para>
      <para>요약: (이 경우 호스트 파일)에 잘못 된 호스트 IP 매핑이 발생 대상 DC를 해결 하려면 없으므로이 예제는 &quot;원본&quot; Active Directory Domain Services 서비스를 실행 하지 않은 (또는 설치 하는 DC 해당 부분의) SPN 아직 등록 되지 않은 복제 하 고 원본 DC 1753 오류를 반환 합니다. 후자의 경우 (호스트 파일)에 다시는 잘못 된 호스트 IP 매핑 대상 DC를 E351이 등록 하는 DC에 연결할 발생 하는 중... SPN 복제 하지만 해당 원본에 오류-2146893022 사용 하 여 실패 한 시도 하므로 다른 호스트 이름 및 보안 id를 원하는 원본 DC 보다 있었습니다. 대상 사용자 이름이 올바르지 않습니다.</para>
    </content>
  </section>
  <relatedTopics>
    <externalLink>
      <linkText>1753 오류로 실패 하는 Active Directory 작업 문제 해결: 끝점 매퍼에서 사용할 수 있는 끝점이 더 이상 있습니다. </linkText> 
      <linkUri> <a href="https://support.microsoft.com/kb/2089874" data-raw-source="https://support.microsoft.com/kb/2089874"> https://support.microsoft.com/kb/2089874 </a> </linkUri> 
    </externalLink> 
<externalLink> <linkText>KB 문서는 Windows Server 2003 지원을 사용 하 여 839880 문제 해결 RPC 끝점 매퍼 오류 제품 CD에서 도구</linkText><linkUri><a href="https://support.microsoft.com/kb/839880" data-raw-source="https://support.microsoft.com/kb/839880">https://support.microsoft.com/kb/839880</a></linkUri></externalLink>
<externalLink><linkText>KB 문서 832017 서비스 개요 및 네트워크 포트 Windows Server 시스템 요구 사항</linkText><linkUri><a href="https://support.microsoft.com/kb/832017/" data-raw-source="https://support.microsoft.com/kb/832017/">https://support.microsoft.com/kb/832017/</a></linkUri></externalLink>
<externalLink><linkText>KB 문서 224196 Active 제한 디렉터리 복제 트래픽 및 클라이언트 RPC 트래픽을 특정 포트로</linkText><linkUri><a href="https://support.microsoft.com/kb/224196/" data-raw-source="https://support.microsoft.com/kb/224196/">https://support.microsoft.com/kb/224196/</a></linkUri></externalLink>
<externalLink><linkText>기술 자료 문서 154596 RPC 동적 포트 할당 방화벽을 사용 하 여 작업을 구성 하는 방법을</linkText><linkUri><a href="https://support.microsoft.com/kb/154596" data-raw-source="https://support.microsoft.com/kb/154596">https://support.microsoft.com/kb/154596</a></linkUri></externalLink><externalLink><linkText>RPC 하는 방법 Works</linkText><linkUri><a href="https://msdn.microsoft.com/library/aa373935(VS.85).aspx" data-raw-source="https://msdn.microsoft.com/library/aa373935(VS.85).aspx">https://msdn.microsoft.com/library/aa373935(VS.85).aspx</a></linkUri></externalLink><externalLink><linkText>연결에 대 한 서버 준비 하는 방법을</linkText> <linkUri> <a href="https://msdn.microsoft.com/library/aa373938(VS.85).aspx" data-raw-source="https://msdn.microsoft.com/library/aa373938(VS.85).aspx"> https://msdn.microsoft.com/library/aa373938(VS.85).aspx </a> </linkUri> </externalLink> 
<externalLink> <linkText>클라이언트에서 연결을 설정 하는 방법을</linkText> <linkUri> <a href="https://msdn.microsoft.com/library/aa373937(VS.85).aspx" data-raw-source="https://msdn.microsoft.com/library/aa373937(VS.85).aspx"> https://msdn.microsoft.com/library/aa373937(VS.85).aspx </a> </linkUri> </externalLink> <externalLink> <linkText>인터페이스를 등록</linkText> <linkUri> <a href="https://msdn.microsoft.com/library/aa375357(VS.85).aspx" data-raw-source="https://msdn.microsoft.com/library/aa375357(VS.85).aspx"> https://msdn.microsoft.com/library/aa375357(VS.85).aspx </a> </linkUri> </externalLink> <externalLink> <linkText>네트워크에서 서버를 사용할 수 있도록</linkText> <linkUri> <a href="https://msdn.microsoft.com/library/aa373974(VS.85).aspx" data-raw-source="https://msdn.microsoft.com/library/aa373974(VS.85).aspx"> https://msdn.microsoft.com/library/aa373974(VS.85).aspx </a> </linkUri> </externalLink> <externalLink> <linkText>끝점 등록</linkText> <linkUri> <a href="https://msdn.microsoft.com/library/aa375255(VS.85).aspx" data-raw-source="https://msdn.microsoft.com/library/aa375255(VS.85).aspx"> https://msdn.microsoft.com/library/aa375255(VS.85).aspx </a> </linkUri> </externalLink> <externalLink> <linkText>클라이언트 호출을 수신 대기</linkText> <linkUri> <a href="https://msdn.microsoft.com/library/aa373966(VS.85).aspx" data-raw-source="https://msdn.microsoft.com/library/aa373966(VS.85).aspx"> https://msdn.microsoft.com/library/aa373966(VS.85).aspx </a> </linkUri> </externalLink> <externalLink> <linkText>클라이언트 연결을 설정 하는 방법</linkText><linkUri><a href="https://msdn.microsoft.com/library/aa373937(VS.85).aspx" data-raw-source="https://msdn.microsoft.com/library/aa373937(VS.85).aspx">https://msdn.microsoft.com/library/aa373937(VS.85).aspx</a></linkUri></externalLink><externalLink><linkText>Active Directory 복제 트래픽 및 클라이언트 RPC 트래픽을 특정 포트로 제한</linkText><linkUri><a href="https://support.microsoft.com/kb/224196" data-raw-source="https://support.microsoft.com/kb/224196">https://support.microsoft.com/kb/224196</a></linkUri></externalLink><externalLink><linkText>AD DS의 대상 DC에 대한 SPN</linkText><linkUri><a href="https://msdn.microsoft.com/library/dd207688(PROT.13).aspx" data-raw-source="https://msdn.microsoft.com/library/dd207688(PROT.13).aspx">https://msdn.microsoft.com/library/dd207688(PROT.13).aspx</a></linkUri></externalLink></relatedTopics>
</developerConceptualDocument>


