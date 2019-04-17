---
ms.assetid: 0fd7b6aa-3e50-45a3-a3a6-56982844363e
title: "이벤트 ID 2088-복제 성공적으로 DNS 조회 오류가 발생 했습니다."
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4f223f075775f942f83a1962da28a77e85e89aa0
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="event-id-2088-dns-lookup-failure-occurred-with-replication-success"></a>이벤트 ID 2088: DNS 조회 오류가 발생 복제 성공

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

잘못 된 DNS 구성 구성원 컴퓨터에서 도메인 컨트롤러 또는 응용 프로그램 서버 로그온 인증 또는 네트워크 리소스에 대 한 액세스를 포함 하 여이 Active Directory Domain Services 숲 속의 중요 한 작업 영향을 줄 수 있습니다. 

즉시이 도메인 컨트롤러 DNS 사용 하 여 원본 도메인 컨트롤러의 IP 주소를 해결할 수 있도록이 DNS 구성 오류를 해결 해야 합니다. 

암호 확인용 서버 이름: d c 1 실패 DNS 호스트 이름: 4a8717eb-8e58-456 c-995a-c92e4add7e8e._msdcs. contoso.com 

참고: 기본적으로 최대 10 DNS 오류가 표시 되 12 지정 된 시간 동안 10 개 이상의 오류가 발생 하는 경우에 있습니다.  모든 개별 오류 이벤트를 기록 하려면 다음과 같은 진단 레지스트리 값으로 설정 1: 

레지스트리 경로: HKLM\System\CurrentControlSet\Services\NTDS\Diagnostics\22 DS RPC 클라이언트 

사용자 문제 해결: 

1) 원본 도메인 컨트롤러 더 긴 경우 다른 컴퓨터 이름으로 다시 설치 작동 또는 운영 체제 또는 NTDSDSA GUID 개체 제거 ntdsutil.exe 메타 데이터 소스 도메인 컨트롤러의 216498 MSKB 문서에서 설명한 단계를 사용 하 여 합니다. 

2) 원본 도메인 컨트롤러 Active Directory를 실행 하 고는 입력 하 여 네트워크에 액세스할 수 있는지 확인 "보기 net \\&lt;소스 DC 이름&gt;" 또는 "ping &lt;소스 DC 이름&gt;" 합니다. 

3) Verify that the source domain controller is using a valid DNS server for DNS services, and that the source domain controller's host record and CNAME record are correctly registered, using the DNS Enhanced version of DCDIAG.EXE available on https://www.microsoft.com/dns 

Dcdiag /test: dns 

4) 이 목적지 도메인 컨트롤러에 사용 하는 올바른 DNS 서버를 DNS 서비스 DCDIAG.EXE 명령을 실행 대상 도메인 컨트롤러의 콘솔 다음과 같습니다. 

Dcdiag /test: dns 

5) For further analysis of DNS error failures see KB 824449: https://support.microsoft.com/?kbid=824449 

추가 데이터 오류 값: 11004 요청된 이름이 올바른지 하지만 요청 형식의 데이터를 찾지 못했습니다</code>
  </introduction>
  <section>
    <title>진단</title>
    <content>
      <para>DNS (CNAME) 별칭 리소스 레코드를 사용 하 여 원본 도메인 컨트롤러의 이름을 확인 실패 DNS 구성 오류 또는 DNS 데이터 전파에 지연 될 수 있습니다.</para>
    </content>
  </section>
  <section>
    <title>해상도</title>
    <content>
      <para>DNS에 설명 된 대로 테스트를 통해 계속 "<link xlink:href="85b1d179-f53e-4f95-b0b8-5b1c096a8076">2087 이벤트 ID: DNS 조회 오류가 발생 복제가 실패할</link>."</para>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>


