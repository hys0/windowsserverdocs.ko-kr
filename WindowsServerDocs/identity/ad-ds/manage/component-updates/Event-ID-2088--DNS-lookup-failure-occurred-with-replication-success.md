---
ms.assetid: 0fd7b6aa-3e50-45a3-a3a6-56982844363e
title: 이벤트 ID 2088-복제 성공 시 DNS 조회 오류가 발생 함
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: d51cbcc93a8decbcb72a1e91854a09345507511d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71368914"
---
# <a name="event-id-2088-dns-lookup-failure-occurred-with-replication-success"></a>이벤트 ID 2088: 복제 성공과 함께 DNS 조회 실패가 발생함

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

    
    <developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
      <introduction>
    <para>When a destination domain controller running Windows Server 2003 with Service Pack 1 (SP1) receives Event ID 2088 in the Directory Service event log, attempts to resolve the globally unique identifier (GUID) in the alias (CNAME) resource record to an IP address for the source domain controller failed. However, the destination domain controller tried other means to resolve the name and succeeded by using either the fully qualified domain name (FQDN) or the NetBIOS name of the source domain controller. Although replication was successful, the Domain Name System (DNS) problem should be diagnosed and resolved. </para>
    <para>The following is an example of the event text: </para>
    <code>Log Name: Directory Service

    Source: Microsoft-Windows-ActiveDirectory_DomainService
    Date: 3/15/2008  9:20:11 AM
    Event ID: 2088
    Task Category: DS RPC Client 
    Level: Warning
    Keywords: Classic
    User: ANONYMOUS LOGON
    Computer: DC3.contoso.com
    Description:
    Active Directory could not use DNS to resolve the IP address of the 
    source domain controller listed below. To maintain the consistency 
    of Security groups, group policy, users and computers and their passwords, 
    Active Directory Domain Services successfully replicated using the NetBIOS 
    or fully qualified computer name of the source domain controller. 

잘못 된 DNS 구성은 로그온 인증 또는 네트워크 리소스에 대 한 액세스를 포함 하 여이 Active Directory Domain Services 포리스트의 구성원 컴퓨터, 도메인 컨트롤러 또는 응용 프로그램 서버에 대 한 다른 필수 작업에 영향을 줄 수 있습니다. 

이 도메인 컨트롤러가 DNS를 사용 하 여 원본 도메인 컨트롤러의 IP 주소를 확인할 수 있도록이 DNS 구성 오류를 즉시 해결 해야 합니다. 

대체 서버 이름: DC1 실패 DNS 호스트 이름: 4a8717eb-8e58-456c-995a-c92e4add7e8e. _msdcs. .com. 

참고: 기본적으로 10 개 이상의 오류가 발생 하더라도 지정 된 12 시간 동안 최대 10 개의 DNS 오류가 표시 됩니다.  모든 개별 오류 이벤트를 기록 하려면 다음 진단 레지스트리 값을 1로 설정 합니다. 

레지스트리 경로: HKLM\System\CurrentControlSet\Services\NTDS\Diagnostics\22 DS RPC 클라이언트 

사용자 작업: 

1) 원본 도메인 컨트롤러가 더 이상 작동 하지 않거나 다른 컴퓨터 이름 또는 NTDSDSA 개체 GUID를 사용 하 여 해당 운영 체제를 다시 설치한 경우 MSKB 문서에 설명 된 단계를 사용 하 여 ntdsutil을 사용 하 여 원본 도메인 컨트롤러의 메타 데이터를 제거 합니다. 216498. 

2) 원본 도메인 컨트롤러가 Active Directory 실행 중이 고 "net view \\&lt;원본 DC 이름&gt;" 또는 "ping &lt;원본 DC 이름&gt;"을 입력 하 여 네트워크에서 액세스할 수 있는지 확인 합니다. 

3) 원본 도메인 컨트롤러에서 dns 서비스에 올바른 DNS 서버를 사용 하 고 있는지, 그리고 DNS 강화 버전의 DCDIAG를 사용 하 여 원본 도메인 컨트롤러의 호스트 레코드 및 CNAME 레코드가 올바르게 등록 되었는지 확인 합니다. <https://www.microsoft.com/dns>에서 사용할 수 있는 EXE 

dcdiag/test: dns 

4) 이 대상 도메인 컨트롤러가 dns 강화 버전의 DCDIAG를 실행 하 여 DNS 서비스용 올바른 DNS 서버를 사용 하 고 있는지 확인 합니다. 다음과 같이 대상 도메인 컨트롤러의 콘솔에서 EXE 명령을 실행 합니다. 

dcdiag/test: dns 

5) DNS 오류 오류에 대 한 추가 분석은 KB 824449: <https://support.microsoft.com/?kbid=824449>을 참조 하세요. 

추가 데이터 오류 값: 11004 요청 된 이름이 올바르지만 요청 된 형식의 데이터를 찾을 수 없습니다</code> </introduction>
  <section>
    <title>진단</title>
    <content>
      <para>Dns의 별칭 (CNAME) 리소스 레코드를 사용 하 여 원본 도메인 컨트롤러 이름을 확인 하는 데 실패 하는 이유는 dns를 잘못 사용 하거나 DNS 데이터 전파의 지연이 원인일 수 있습니다.</para>
    </content>
  </section>
  <section>
    <title>해상도</title>
    <content>
      <para>&quot;<link xlink:href="85b1d179-f53e-4f95-b0b8-5b1c096a8076">이벤트 ID 2087: dns 조회 실패로 인해 복제가 실패</link>했습니다 .에 설명 된 대로 dns 테스트를 진행 합니다.&quot;</para>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>


