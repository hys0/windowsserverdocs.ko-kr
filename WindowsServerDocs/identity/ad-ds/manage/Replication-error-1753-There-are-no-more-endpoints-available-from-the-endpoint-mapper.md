---
ms.assetid: 0f21951c-b1bf-43bb-a329-bbb40c58c876
title: "복제 오류 1753는 사용할 수 있는 더 많은 끝점 끝점 맵 편집기에서 사용할 수 있는"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0e7412f5edc6c206888551fdc250883b5c0ced3e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="replication-error-1753-there-are-no-more-endpoints-available-from-the-endpoint-mapper"></a>복제 오류 1753는 사용할 수 있는 더 많은 끝점 끝점 맵 편집기에서 사용할 수 있는

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


<developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>이 항목에서는 원인 현상과 Active Directory 복제 오류 8524 The DSA 작업 DNS 조회 오류로 인해 진행 수 없으면 해결 하는 방법을 설명 합니다.</para>
    <list class="bullet">
      <listItem><para><link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_Symptoms">증상</link></para></listItem><listItem><para><link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_Cause">원인</link></para></listItem><listItem><para><link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_Resolutions">해상도</link></para></listItem><listItem><para><link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_MoreInfo">자세한 내용은</link></para></listItem>
    </list>
  </introduction>
  <section address="BKMK_Symptoms">
    <title>증상이</title>
    <content>
      <para>원인을 현상에 설명 하 고 해상도 1753 Win32 오류와 함께 실패 하는 Active Directory 작업에 대 한 단계: "가 없는 더 끝점 끝점 맵 편집기에서 사용할 수 있습니다." </para>
      <list class="ordered">
        <listItem>
          <para>연결 테스트, Active Directory 복제 테스트 또는 KnowsOfRoleHolders 테스트 1753 오류와 함께 실패 했다는 DCDIAG 보고서: "가 없는 더 끝점 끝점 맵 편집기에서 사용할 수 있습니다." </para>
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
<listItem><para>REPADMIN 합니다. EXE는 1753 상태로 해당 복제 시도가 실패를 보고 합니다. </para><para>1753 상태는 일반적으로 인용 REPADMIN 명령 포함 되어 있지만에 국한 되지 않습니다.</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><tbody><tr><TD><list class="bullet"><listItem><para>REPADMIN /REPLSUM</para></listItem><listItem><para>REPADMIN /SHOWREPL</para></listItem></list></TD><TD><list class="bullet"><listItem><para>REPADMIN /SHOWREPS</para></listItem><listItem><para>REPADMIN 가져오는</para></listItem></list></TD></tr></tbody></table><para>샘플 "REPADMIN /SHOWREPS"을 "복제 액세스할 수 없습니다" 오류가 발생 하 여 CONTOSO d c 1 실패 CONTOSO d c 2의 인바인드 복제가 아래 표시 결과:</para><code>Default-First-Site-NameCONTOSO-DC1
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

</code></listItem><listItem><para>는 <ui>복제 토폴로지 확인</ui> 명령 Active Directory 사이트 및 서비스에서 반환 "가 없는 더 끝점 끝점 맵 편집기에서 사용할 수 있습니다." </para><para>소스의 DC 연결 개체를 마우스 오른쪽 단추로 클릭 하 고 선택 <ui>복제 토폴로지 확인</ui> 실패 "가 없는 더 끝점 끝점 맵 편집기에서 사용할 수 있습니다." 오류 메시지는 다음과 같습니다 화면상:</para><para>대화 제목 텍스트: 복제 토폴로지 확인</para><para>대화 메시지 내용: </para><para>도메인 컨트롤러에 연결 하는 동안 다음과 같은 오류가 발생 한: 끝점 맵 편집기에서 사용할 수 없는 더 끝점은 합니다. </para></listItem><listItem><para>는 <ui>지금 복제</ui> Active Directory 사이트 및 서비스에서 명령 반환 "가 없는 더 끝점 끝점 맵 편집기에서 사용할 수 있습니다." </para><para>소스의 DC 연결 개체를 마우스 오른쪽 단추로 클릭 하 고 선택 <ui>지금 복제</ui> 실패 "가 없는 더 끝점 끝점 맵 편집기에서 사용할 수 있습니다." 오류 메시지는 다음과 같습니다 화면상:</para><para>대화 제목 텍스트: 지금 복제</para><para>대화 메시지 내용: 명명 컨텍스트를 동기화 하는 동안 다음과 같은 오류가 발생 한 &lt;% 디렉터리 파티션 이름&gt; 도메인 컨트롤러에서 &lt;소스 DC&gt; 도메인 컨트롤러에 &lt;대상 DC&gt;:</para><para>

더 많은 끝점 없습니다는 끝점 맵 편집기를 제공 합니다. </para><para>계속 됩니다</para></listItem><listItem><para>NTDS KCC, NTDS 일반 또는 Microsoft-Windows-ActiveDirectory_DomainService 이벤트-2146893022 상태 이벤트 뷰어에 디렉터리 서비스 로그에 기록 됩니다. </para><para>일반적으로-2146893022 상태 인용 active Directory 이벤트 포함 되어 있지만에 국한 되지 않습니다.</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><thead><tr><TD><para>이벤트 ID</para></TD><TD><para>이벤트 소스</para></TD><TD><para>이벤트 문자열</para></TD></tr></thead><tbody><tr><TD><para>1655</para></TD><TD><para>NTDS 일반</para></TD><TD><para>다음 드와 통신 하 려 active Directory 하 고 시도 되지 않았습니다.</para></TD></tr><tr><TD><para>1925</para></TD><TD><para>NTDS KCC</para></TD><TD><para>다음 쓸 수 디렉터리 파티션에 대 한 복제 링크를 설정 하지 못했습니다.</para></TD></tr><tr><TD><para>1265</para></TD><TD><para>NTDS KCC</para></TD><TD><para>한 복제 계약 다음 디렉터리 파티션와 소스 도메인 컨트롤러에 대 한 추가 정보 일관성 검사 (KCC) 시도가 실패 했습니다.</para></TD></tr></tbody></table></listItem>
</list>
    </content>
  </section>
  <section address="BKMK_Cause">
    <title>원인</title>
    <content>
      <para>아래 다이어그램 표시 되 RPC 워크플로 RPC 클라이언트 7 단계에서를 클라이언트 응용 프로그램에서 서버 1 단계에서 RPC Endpoint 맵 편집기 (EPM)와 응용 프로그램의 등록 된 데이터를 전달 시작 합니다. </para>
      <para>&lt;ADDS_RPCWorkflow&gt;</para>
      <para>7 지도 다음과 같은 작업을 통해 1 단계:</para>
      <list class="ordered">
        <listItem>
          <para>서버 앱 등록 끝점 RPC Endpoint 맵 편집기 (EPM)와 </para>
        </listItem>
        <listItem>
          <para>클라이언트 RPC 통화에서 (사용자를 대신 하 여 운영 체제 또는 응용 프로그램 시작 작업) </para>
        </listItem>
        <listItem>
          <para>클라이언트 RPC 연락처 대상 컴퓨터 EPM 측면와 클라이언트 전화를 완료 하려면 끝점 요청 </para>
        </listItem>
        <listItem>
          <para>서버 컴퓨터의 EPM 끝점으로 응답 하지 않으면 </para>
        </listItem>
        <listItem>
          <para>클라이언트 측 RPC 연락처 서버 앱 </para>
        </listItem>
        <listItem>
          <para>서버 앱에서 호출 실행 결과 클라이언트를 반환 RPC </para>
        </listItem>
        <listItem>
          <para>클라이언트 측 RPC 클라이언트 응용 프로그램에 다시 결과 전달</para>
        </listItem>
      </list>
      <para>오류 1753 #3 단계와 4 사이의 오류도 생성 됩니다. 특히, 오류 1753 되 RPC 클라이언트 (대상 DC) 서버에 연결할 수 있는 RPC (소스 DC) 135 포트를 통해 있었지만 RPC (소스 DC) 서버에 EPM 관심 RPC 응용 프로그램을 찾을 수 없습니다 하며 서버 쪽 오류 1753 반환 의미 합니다. 되 RPC (대상 DC) 클라이언트는 서버 쪽 오류 응답 서버에서 받은 RPC (광고 복제 소스 DC) 네트워크를 통해 1753 오류를 나타냅니다. </para>
      <para>1753 오류에 대 한 특정 근본 원인으로는: </para>
      <list class="ordered">
        <listItem>
          <para>시작 되지 않음 서버 앱 (즉, 위에 있는 "추가 정보" 다이어그램 #1 단계를 시도 하지 않음). </para>
        </listItem>
        <listItem>
          <para>서버 앱 시작 했지만 RPC Endpoint 맵 편집기 (즉, 단계에서에서 1 위의 "추가 정보" 다이어그램 하려고 했지만 실패)로 등록 하지 못하도록 하는 초기화 하는 동안 일부 오류가 발생 했습니다. </para>
        </listItem>
        <listItem>
          <para>서버 앱 시작 되지만 이후 중지 합니다. (즉, 단계에서에서 1 위의 "추가 정보" 다이어그램 성공적으로 완료 된 했지만 없습니다 완료 나중 서버 죽 때문에). </para>
        </listItem>
        <listItem>
          <para>서버 앱 수동으로 등록 되지 않은 끝점 (의도적 있지만 3 유사 합니다. 하지 않을 가능성이 높은 하지만 완성도 포함 됩니다.) </para>
        </listItem>
        <listItem>
          <para>RPC 클라이언트 (대상 DC) 의도 한 IP 매핑 오류 DNS, WINS 또는 호스트/Lmhosts 파일의 이름 인해 보다 다른 RPC 서버에 연결 합니다. </para>
        </listItem>
      </list>
      <para>오류 1753는 아닙니다: </para>
      <list class="bullet">
        <listItem>
          <para>135 포트를 통해 RPC 클라이언트 (대상 DC)와 RPC 서버 (소스 DC) 네트워크 연결의 부족</para>
        </listItem>
        <listItem>
          <para>RPC 서버 (소스 DC) 네트워크 연결이 부족 포트 135 및 RPC (대상 DC) 클라이언트를 사용 하 여 임시 포트를 통해 합니다. </para>
        </listItem>
        <listItem>
          <para>Kerberos 암호화 패킷 암호를 해독 하려면 DC 원본으로 사용할 수 없음 또는 암호 일치 하지</para>
        </listItem>
      </list>
      <para></para>
    </content>
  </section>
  <section address="BKMK_Resolutions">
    <title>해상도</title>
    <content>
      <list class="ordered">
        <listItem>
          <para>
            <embeddedLabel>끝점 맵 편집기 해당 서비스에 등록 서비스를 시작 하는 확인</embeddedLabel>
          </para>
          <para>Windows 2000에 대 한 및 Windows Server 2003 Dc: 원본 DC 표준 모드로 부팅 되는 있는지 확인 합니다. </para>
          <para>Windows Server 2008 또는 Windows Server 2008 R2: 원본 DC 콘솔에서 관리자 (services.msc) 서비스를 시작 하 고 있는지 확인는 <embeddedLabel>Active Directory Domain Services</embeddedLabel> 서비스가 실행 되 고 있습니다. </para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>원하는 RPC 서버 (소스 DC)에 연결 된 해당 RPC 클라이언트 (대상 DC) 확인</embeddedLabel>
          </para>
          <para>_msdcs에 도메인 컨트롤러 CNAME 기록는 일반적인 Active Directory 숲 등록에 모든 Dc 합니다. &lt;이렇게&gt; 숲 내에 있는 것 어떤 도메인에 관계 없이 DNS 영역 합니다. DC CNAME 기록에서 파생 되는 <embeddedLabel>objectGUID</embeddedLabel> NTDS 설정을 개체 각 도메인 컨트롤러의 특성 합니다. </para>
          <para>대상 DC DNS 소스 Dc CNAME 기록에 대 한 쿼리 복제 하는 작업을 수행할 때입니다. CNAME 기록 원본 Dc IP 주소를 추출 하는 데 사용 되는 원본을 DC 정식된 컴퓨터 이름을 포함 DNS 클라이언트 캐시 조회 통해 개최 / LMHost 조회 호스트 A 파일 DNS, WINS에 AAAA 녹화 / 합니다. </para>
          <para>오래 된 NTDS 설정 및 DNS, WINS 호스트 및 LMHOST 파일 잘못 이름-TO-IP 매핑 잘못 RPC (소스 DC) 서버에 연결 하는 RPC 클라이언트 (대상 DC) 발생할 수 있습니다. 뿐만 아니라 잘못 이름을-TO-IP 매핑 관심 (이 경우 Active Directory 역할)가 설치 되어 있지는 않은 RPC 서버 응용 프로그램은 컴퓨터에 연결 하려면 RPC (대상 DC) 클라이언트를 발생할 수 있습니다. (예: d c 3 또는 회원 컴퓨터의 IP 주소를 포함 하는 오래 된 호스트 기록 2에 대 한). </para>
          <para>ObjectGUID Active Directory Dc 복사본 대상에 있는 DC 원본에 대 한 Active Directory Dc 복사본 원본에 저장 된 소스 DC objectGUID 일치 하는 확인 합니다. 일치 하지 않는 경우 repadmin 사용 하 여 /showobjmeta DC 소스의 마지막 프로 모션에 해당 하는 어떤 것을 볼 수 ntds 설정 개체 (힌트: NTDS 설정 개체 만든 날짜 로부터 대 한 날짜 스탬프 비교 /showobjmeta 소스 Dc dcpromo.log 파일의 마지막 프로 모션 날짜에 대해 합니다. 만든 DCPROMO DCPROMO.LOG 파일 자체). 개체 Guid 동일 하지 않을 가능성이 DC 대상에 오래 된 NTDS 설정에 대 한 개체 원본 DC CNAME 레코드 IP 매핑 잘못 이름의 호스트 레코드를 참조 것입니다. </para>
          <para>대상 DC 실행 IPCONFIG /ALL DNS 서버를 사용 하는 대상 DC 이름을 해상도 확인 하려면:</para>
          <code>c:&gt;ipconfig /all</code>
          <para>대상 DC 소스 Dc 정식된 DC CNAME 기록에 대해 NSLOOKUP 실행:</para>
          <code>c:&gt;nslookup -type=cname &lt;fully qualified cname of source DC&gt; &lt;destination DCs primary DNS Server IP &gt;
c:&gt;nslookup -type=cname &lt;fully qualified cname of source DC&gt; &lt;destination DCs secondary DNS Server IP&gt;</code>
          <para>있는지 NSLOOKUP에서 반환 IP 주소 "소유 하 고" 호스트 이름을 확인 / DC 소스의 보안 id:</para>

          <code>C:&gt;NBTSTAT -A &lt;IP address returned by NSLOOKUP in the step above&gt;</code>
          <para>또는</para>
          <para>원본 DC 본체에 로그온 명령 프롬프트에서 "IPCONFIG"을 실행 하 고 원본 DC 위의 NSLOOKUP 명령을 사용 하 여 반환 된 IP 주소를 소유 하 고 있는지 확인</para>
          <para>오래 된 / 중복 호스트 IP 매핑 DNS에를 확인</para>
          <code>NSLOOKUP -type=hostname &lt;single label hostname of source DC&gt; &lt;primary DNS Server IP on destination DC&gt;
NSLOOKUP -type=hostname &lt;single label hostname of source DC&gt; &lt;secondary DNS Server IP on destination DC&gt;

NSLOOKUP -type=hostname &lt;fully qualified computer name of source DC&gt; &lt;primary DNS Server IP on destination DC&gt;
NSLOOKUP -type=hostname &lt;fully qualified computer name of source DC&gt; &lt;secondary DNS Server IP on dest. DC&gt;</code>
<para>호스트 기록에 잘못 된 IP 주소 있으면 조사 여부 DNS 청소를 사용 하거나 올바르게 구성 되어 있습니다. </para><para>위의 테스트 또는 네트워크 추적 잘못 된 IP 주소를 반환 이름 쿼리 표시 되지 않으면, 호스트 파일 LMHOSTS 파일, WINS 서버에 오래 된 항목을 고려 합니다. 참고 WINS 대체 이름 확인을 수행 하 여 DNS 서버를 구성할 수도 있습니다. </para>
</listItem>
        <listItem>
          <para>
            <embeddedLabel>서버 응용 프로그램 (Active Directory 외.)가 RPC (소스 DC) 서버에 끝점 맵 편집기에 등록 확인</embeddedLabel>
          </para>
          <para>Active Directory를 함께 잘 알려지고 동적으로 등록 된 포트를 사용 합니다. 이 표에 유명 포트와 Active Directory 도메인 컨트롤러에서 사용 하는 프로토콜 있습니다.</para>
          <table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>RPC 서버 응용 프로그램</para>
                </TD>
                <TD>
                  <para>포트</para>
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
                  <para>Microsoft DS</para>
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
                  <para>드 서버</para>
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
                  <para>드 서버</para>
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
          <para>Well-known ports are NOT registered with the endpoint mapper. </para>
          <para>Active Directory and other applications also register services that receive dynamically assigned ports in the RPC ephemeral port range. Such RPC server applications are dynamically assigned TCP ports between 1024 and 5000 on Windows 2000 and Windows Server 2003 computers and ports between 49152 and 65535 range on Windows Server 2008 and Windows Server 2008 R2 computers. The RPC port used by replication can be hard-coded in the registry using the steps documented in <externalLink><linkText>KB article 224196</linkText><linkUri>https://support.microsoft.com/kb/224196</linkUri></externalLink>. Active Directory continues to register with the EPM when configured to use a hard coded port. </para>
          <para>Verify that the RPC Server application of interest has registered itself with the RPC endpoint mapper on the RPC Server (the source DC in the case of AD replication). </para>
          <para>There are a number of ways to accomplish this task but one is to install and run PORTQRY from an admin privileged CMD prompt on the console of the source DC using the syntax: </para>
          <code>c:\&gt;portquery -n &lt;source DC&gt; -e 135 &gt;file.txt</code>
          <para>In the portqry output, note the port numbers dynamically registered by the "MS NT Directory DRS Interface" (UUID = 351...) for the <embeddedLabel>ncacn_ip_tcp protocol</embeddedLabel>. The snippet below shows sample portquery output from a Windows Server 2008 R2 DC and the UUID / protocol pair specifically used by Active Directory highlighted in <embeddedLabel>bold</embeddedLabel>: </para>
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
          <para>Other possible ways to resolve this error:</para>
          <list class="ordered">
            <listItem>
              <para>Verify that the source DC is booted in normal mode and that the OS and DC role on the source DC have fully started.</para>
            </listItem>
            <listItem>
              <para>Verify that the Active Directory Domain Service is running. If the service is currently stopped or was not configured with default startup values, reset the default startup values, reboot the modified DC then retry the operation.</para>
            </listItem>
            <listItem>
              <para>Verify that the startup value and service status for RPC service and RPC Locator is correct for OS version of the RPC Client (destination DC) and RPC Server (source DC). If the service is currently stopped or was not configured with default startup values, reset the default startup values, reboot the modified DC then retry the operation.</para>
              <para>In addition, ensure that the service context matches default settings listed in the following table.</para>
              <table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11">
                <thead>
                  <tr>
                    <TD>
                      <para>서비스</para>
                    </TD>
                    <TD>
                      <para>기본 상태 (시작 유형) 이후와 Windows Server 2003 </para>
                    </TD>
                    <TD>
                      <para>Windows 2000 Server에서에서 기본 상태 (시작 유형)</para>
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
                      <para>원격 프로시저 호출 Locator</para>
                    </TD>
                    <TD>
                      <para>Null 중지 (수동) 또는</para>
                    </TD>
                    <TD>
                      <para>시작 (자동)</para>
                    </TD>
                  </tr>
                </tbody>
              </table>
            </listItem>
            <listItem>
              <para>Verify that the size of the dynamic port range has not been constrained. The Windows Server 2008 and Windows Server 2008 R2 NETSH syntax to enumerate the RPC port range is shown below:</para>
              <code>&gt;netsh int ipv4 show dynamicport tcp
&gt;netsh int ipv4 show dynamicport udp
&gt;netsh int ipv6 show dynamicport tcp
&gt;netsh int ipv6 show dynamicport udp</code>
            </listItem>
            <listItem>
              <para>Verify that hard coded port definitions defined in KB 224196 fall within the dynamic port range for source DCs OS version.</para>
              <para>Review <externalLink><linkText>KB article 224196</linkText><linkUri>https://support.microsoft.com/kb/224196</linkUri></externalLink> and ensure that the hard coded port falls within the ephemeral port range for the source DC's operating system version.</para>
            </listItem>
            <listItem>
              <para>Verify that the ClientProtocols key exists under HKLM\Software\Microsoft\Rpc and contains the following 5 default values:</para>
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
    <title>자세한 내용은</title>
    <content>
      <para>
        <embeddedLabel>매핑-2146893022 및 초래 RPC 오류 1753 ip 잘못 이름의 예:는 대상 사용자 이름이 잘못</embeddedLabel>
      </para>
      <para>contoso.com 도메인 d c 1 구성 되어 있으며 x.x.1.1 및 x.x.1.2 d c 2 ip 주소 합니다. 호스트 "A" / "AAAA" 기록 2에 대 한 모든 d c 1에 대해 구성 DNS 서버에 올바르게 등록 되어 있습니다. 또한 d c 1에서 호스트 파일 정식 DC2s 호스트 IP 주소 x.x.1.2 매핑하 항목이 포함 되어 있습니다. 나중에 2의 IP 주소에서에서 변경 내용은 X.X.1.2 X.X.1.3와 새 구성원 컴퓨터에 IP 주소 x.x.1.2 도메인에 연결 됩니다. 광고 복제 시도 발생 하 여는 <ui>지금 복제</ui> 추적 아래에 표시 된 대로 Active Directory 사이트 및 서비스 스냅인 명령이 실패 1753 오류:</para>
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
      <para>프레임 <embeddedLabel>10</embeddedLabel>, DC 목적지에 대 한 Active Directory 복제 서비스 클래스 UUID E351 135 포트를 통해 소스 Dc 종료 지점을 맵 편집기 쿼리... </para>
      <para>프레임에서 <embeddedLabel>11</embeddedLabel>,이 원본 DC, DC 역할 아직 호스트 하지 않는 하 고 E351 등록 되지 않은 구성원 컴퓨터 경우... 해당 지역 EPM와 복제 서비스에 대 한 UUID "가 더 많은 없는 끝점 끝점 맵 편집기에서 사용할 수 있는" 소수점 오류 1753, hex 오류 0x6d9 및 오류 매핑하 EP_S_NOT_REGISTERED 기호 오류가 발생 하 여 응답 합니다. </para>
      <para>복제본 contoso.com 도메인에 있는 "MayberryDC"로 IP 주소 x.x.1.2 회원 컴퓨터 수준을 올린가 나중에 있습니다. 다시의 <ui>지금 복제</ui> 이 이번와 함께 실패 있지만 명령을 복제 시작 하는 데 사용 되는 화상 오류 "대상 사용자 이름 올바르지 않습니다." 해당 네트워크 어댑터가 IP 할당 된 컴퓨터 x.x.1.2 주소 <placeholder>는</placeholder> 도메인 컨트롤러 현재 표준 모드로 부팅 되 고... E351 등록 복제 서비스와의 로컬 EPM 하지만 UUID d c 2의 이름이 나 보안 id 소유 하지 않는 및 요청 이제 오류와 함께 실패 "대상 사용자 이름이 잘못있지 않습니다." 하므로 d c 1 Kerberos 요청한 해제할 수는 없습니다 오류 소수점 오류-2146893022 지도 오류 0x80090322 hex / 합니다. </para>
      <para>이러한 잘못 된 호스트-TO-IP 매핑 호스트의 오래 된 항목으로 원인이 lmhost 파일 호스트 A / / DNS, WINS에 AAAA 등록 합니다. </para>
      <para>요약:이 이때 (이 경우 호스트 파일)에 잘못 된 호스트-TO-IP 매핑 SPN 등록 되지 않은 복제와 원본 1753 오류를 반환 DC "소스" DC Active Directory Domain Services 되어 있지 않은 실행 서비스 (또는 해당 문제에 대 한도 설치 된)에 지금 확인 하도록 대상 DC 발생 하기 때문에 실패 했습니다. (다시 호스트 파일)에 잘못 된 호스트-TO-IP 매핑 발생 대상 DC 복제 SPN,이 E351... 등록 DC에 연결 하려면 두 번째 경우에서 했지만 해당 소스 다른 호스트 이름 및 보안 id 의도 소스 DC 보다 시도해-2146893022 오류로 하므로: 대상 사용자 이름이 잘못 하지 않습니다.</para>
    </content>
  </section>
  <relatedTopics>
    <externalLink>
      <linkText>Troubleshooting Active Directory operations that fail with error 1753: There are no more endpoints available from the endpoint mapper.</linkText>
      <linkUri>https://support.microsoft.com/kb/2089874</linkUri>
    </externalLink>
<externalLink><linkText>KB article 839880 Troubleshooting RPC Endpoint Mapper errors using the Windows Server 2003 Support Tools from the product CD</linkText><linkUri>https://support.microsoft.com/kb/839880</linkUri></externalLink>
<externalLink><linkText>KB article 832017 Service overview and network port requirements for the Windows Server system</linkText><linkUri>https://support.microsoft.com/kb/832017/</linkUri></externalLink>
<externalLink><linkText>KB article 224196 Restricting Active Directory replication traffic and client RPC traffic to a specific port</linkText><linkUri>https://support.microsoft.com/kb/224196/</linkUri></externalLink>
<externalLink><linkText>KB article 154596 How to configure RPC dynamic port allocation to work with firewalls</linkText><linkUri>https://support.microsoft.com/kb/154596</linkUri></externalLink><externalLink><linkText>How RPC Works</linkText><linkUri>https://msdn.microsoft.com/library/aa373935(VS.85).aspx</linkUri></externalLink><externalLink><linkText>How the Server Prepares for a Connection</linkText><linkUri>https://msdn.microsoft.com/library/aa373938(VS.85).aspx</linkUri></externalLink>
<externalLink><linkText>How the Client Establishes a Connection</linkText><linkUri>https://msdn.microsoft.com/library/aa373937(VS.85).aspx</linkUri></externalLink><externalLink><linkText>Registering the Interface</linkText><linkUri>https://msdn.microsoft.com/library/aa375357(VS.85).aspx</linkUri></externalLink><externalLink><linkText>Making the Server Available on the Network</linkText><linkUri>https://msdn.microsoft.com/library/aa373974(VS.85).aspx</linkUri></externalLink><externalLink><linkText>Registering Endpoints</linkText><linkUri>https://msdn.microsoft.com/library/aa375255(VS.85).aspx</linkUri></externalLink><externalLink><linkText>Listening for Client Calls</linkText><linkUri>https://msdn.microsoft.com/library/aa373966(VS.85).aspx</linkUri></externalLink><externalLink><linkText>How the Client Establishes a Connection</linkText><linkUri>https://msdn.microsoft.com/library/aa373937(VS.85).aspx</linkUri></externalLink><externalLink><linkText>Restricting Active Directory replication traffic and client RPC traffic to a specific port</linkText><linkUri>https://support.microsoft.com/kb/224196</linkUri></externalLink><externalLink><linkText>SPN for a Target DC in AD DS</linkText><linkUri>https://msdn.microsoft.com/library/dd207688(PROT.13).aspx</linkUri></externalLink></relatedTopics>
</developerConceptualDocument>


