---
ms.assetid: 777aab65-c9c7-4dc9-a807-9ab73fac87b8
title: AD FS 엑스트라넷 잠금 보호를 구성 합니다.
description: ''
author: billmath
ms.author: billmath
manager: mtilman
ms.date: 02/20/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 904b563da2f1404d873c7352db9eadb7bfe252f2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869764"
---
# <a name="ad-fs-extranet-lockout-and-extranet-smart-lockout"></a>AD FS 엑스트라넷 잠금 및 엑스트라넷 잠금

# <a name="overview"></a>개요

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

Windows Server 2012 R2에서 AD FS에서 호출 하는 보안 기능을 도입 했습니다 [엑스트라넷 소프트 잠금](configure-ad-fs-extranet-soft-lockout-protection.md)합니다.  이 기능을 사용 하 여 AD FS 기간에 대 한 사용자가 엑스트라넷에서 인증을 중지 합니다.  이렇게 하면 사용자 계정을 Active Directory에서 잠기지 않습니다. 사용자 AD 계정 잠금에서를 보호 하는 것 외에도 AD FS 엑스트라넷 잠금도 무차별 암호 추측 공격 으로부터 보호 합니다.

Windows Server 2016에서 AD FS 2018 년 6 월에에서 도입 **엑스트라넷 스마트 잠금 (ESL)** 합니다.  ESL AD Fs에서를 유효한 사용자 것 처럼 보이는 로그인 시도 공격자 수에서 로그인 구분할 수 있습니다. 결과적으로, AD FS는 유효한 사용자가 해당 계정을 사용 하 여 계속 하도록 허용 하는 동안 공격자가 out 잠글 수 있습니다. 이 사용자의 서비스 거부를 방지 하 고 "암호-스프레이" 공격과 같은 대상된 공격 으로부터 보호 합니다.  
ESL은 Windows Server 2016에서 AD FS에 대해 사용할 수 있으며 Windows Server 2019에서 AD FS에 빌드됩니다.

> [!NOTE]
> 이 기능에만 작동 합니다 **엑스트라넷 시나리오** 웹 응용 프로그램 프록시를 통해 제공 되는 인증 요청 및에 적용 됩니다 **사용자 이름 및 암호 인증**합니다.

## <a name="advantages-of-extranet-smart-lockout-in-ad-fs-2016"></a>AD FS 2016에서에서 엑스트라넷 잠금의 장점
다음과 같은 주요 이점을 제공 하는 AD FS 2012 r 2에서에서 엑스트라넷 소프트 잠금:
- 사용자 계정을 보호 **무차별 암호 대입 공격** 지속적으로 인증 요청을 전송 하 여 및에서 사용자의 암호를 추측 하려고 공격자의 **암호 스프레이 공격** 위치 공격자가 여러 서로 다른 계정으로 일반적인 암호를 사용 하려고 합니다.
- 사용자 계정을 보호 **Active Directory 계정 잠금** 잘못 된 암호를 사용 하 여 악의적인 인증 요청에서. 이 경우 엑스트라넷 액세스에 대 한 사용자 계정이 잠기게 됩니다, 있지만 사용자 수는 회사 네트워크에서 AD에 로그인 합니다. 이것을 **소프트 잠금**합니다.

다음을 추가 하 여 엑스트라넷 잠금 엑스트라넷 소프트 잠금의 장점에 기반 합니다.
- 사용자를 보호 하에서 발생 **엑스트라넷 계정 잠금** 악성 인증 요청에서.  스마트 잠금에서는 실제 사용자가 친숙 한 위치에서 엑스트라넷에서 로그온 할 수 있도록 하는 동안 알 수 없는 위치에서 잠재적으로 악의적인 요청을 차단 (위치는 사용자가 성공적으로 로그인 하기 전에).
- 시스템 계정을 사용 하지 않도록 설정 하지 않고 장점과 악성 signon 활동을 알 수 있도록 로그 전용 모드에

## <a name="additional-advantages-of-extranet-smart-lockout-in-ad-fs-2019"></a>AD FS 2019의에서 스마트 잠금 엑스트라넷의 추가적인 이점
AD FS 2019에서에서 엑스트라넷 잠금 추가 AD FS 2016에 비해 다음과 같은 이점이 있습니다.
- 알려진된 적절 한 위치에 사용자가 주의 대상 위치에서 요청 보다 오류에 대 한 더 많은 공간을 그려볼 수 있도록 친숙 하 고 알 수 없는 위치에 대 한 독립적인 잠금 임계값을 설정 합니다.
- 이전 소프트 잠금 동작을 적용 하면서 스마트 잠금에 대 한 감사 모드를 사용 하도록 설정

## <a name="pre-requisites-for-extranet-smart-lockout-in-ad-fs-2016"></a>AD FS 2016에서에서 엑스트라넷 잠금에 대 한 필수 조건
다음과 같은 필수가 ad FS 2019 ESL 필요 합니다.

### <a name="install-updates-on-all-nodes-in-the-farm"></a>팜의 모든 노드에서 업데이트를 설치 합니다.
먼저, 2018 년 6 월 Windows 업데이트를 기준으로 최신 상태입니다. 모든 Windows Server 2016 AD FS 서버 및 AD FS 2016 팜 2016 팜 동작 수준에서 실행 되 고 있는지 확인 합니다.

### <a name="update-artifact-database-permissions"></a>아티팩트 데이터베이스 권한을 업데이트합니다
엑스트라넷 잠금에는 AD FS 서비스 계정에 ADFS 아티팩트 데이터베이스에 새 테이블로 권한이 필요 합니다.  PowerShell 명령 창에서 다음 명령을 실행 하 여이 권한을 부여 합니다.
``` powershell
PS C:\>$cred = Get-Credential
PS C:\>Update-AdfsArtifactDatabasePermission -Credential $cred
```
여기서 `$cred` AD FS 관리자 권한이 있는 계정 (AD FS 관리자 권한은 변경이 데이터베이스를 확인 해야 합니다.)

>[!NOTE]
>WID 데이터베이스를 사용 하는 여러 서버 팜에서 위의 cmdlet은 모든 AD FS 서버는 Windows 원격 관리를 사용할 필요

AD FS 관리자 권한이 없으면 구성할 수 있습니다 데이터베이스 사용 권한을 수동으로 SQL 또는 WID AdfsArtifactStore 데이터베이스에 연결 하는 경우 다음 명령을 실행 하 여.
```
sp_addrolemember 'db_owner', 'db_genevaservice'
```
### <a name="ensure-ad-fs-security-audit-logging-is-enabled"></a>AD FS 보안 감사 로깅을 사용 하도록 설정 확인
이 기능을 사용 하면 모든 AD FS 서버의 로컬 정책을 비롯 하 여 AD FS에 따라서 감사 로그를 사용할 수 있어야 합니다 보안 감사를 사용 합니다.

## <a name="pre-requisites-for-extranet-smart-lockout-in-ad-fs-2019"></a>2019 AD fs에서 엑스트라넷 잠금에 대 한 필수 조건
다음과 같은 필수가 AD FS 2016을 사용 하 여 ESL 필요 합니다.

### <a name="ensure-ad-fs-security-audit-logging-is-enabled"></a>AD FS 보안 감사 로깅을 사용 하도록 설정 확인
이 기능을 사용 하면 모든 AD FS 서버의 로컬 정책을 비롯 하 여 AD FS에 따라서 감사 로그를 사용할 수 있어야 합니다 보안 감사를 사용 합니다.

## <a name="lockout-settings"></a>잠금 설정
엑스트라넷 잠금 신규 및 기존 AD FS 속성으로 제어 하는 새 기능 집합으로 구성 됩니다.

### <a name="extranet-lockout-enabled"></a>엑스트라넷 잠금 사용
엑스트라넷 잠금 이전에 "soft" 엑스트라넷 잠금 제어에 사용 된 동일한 AD FS 속성을 사용 합니다.  ExtranetLockoutEnabled 라고 속성과 Get-adfsproperties 통해 확인할 수 있습니다.

### <a name="extranet-smart-lockout-mode"></a>엑스트라넷 잠금 모드
스마트 vs "soft" 잠금 동작을 제어 하려면 ExtranetLockoutMode 라는 새 AD FS 속성이 추가 되었습니다.  Set-adfsproperties 통해 설정할 수 있습니다 하 고 3 개의 값을 포함 합니다.

    - **ADPasswordCounter** – 레거시 위치에 따라 달라 지지 않습니다 ADFS "엑스트라넷 소프트 잠금" 모드입니다.  이것은 기본값입니다.

    - **ADFSSmartLockoutLogOnly** – 엑스트라넷 잠금 이지만 인증 요청을 거부 하는 대신 AD FS는 쓰기 관리 및 감사 이벤트에만 합니다.

    - **ADFSSmartLockoutEnforce** -엑스트라넷 잠금 임계값에 도달 하면 알 수 없는 요청을 차단 하는 것에 대 한 전체 지원입니다.

Ad FS 2019에서 해당 소프트 잠금 계속 스마트 잠금에 대 한 준비 하는 동안 적용 됩니다 있도록 ADPasswordCounter 및 ADFSSmartLockoutLogOnly 값을 결합할 수 있습니다.

### <a name="lockout-threshold-and-observation-window"></a>잠금 임계값 및 관찰 창
AD FS 2019의에서 스마트 잠금 사용 하 여 동일한 두 개의 AD FS 속성을 이전에 사용 되는 소프트 잠금: ExtranetObservationWindow 및 ExtranetLockoutThreshold 합니다.

- **ExtranetLockoutThreshold &lt;정수&gt;**  이 잘못 된 암호 시도의 최대 수를 정의 합니다. 임계값에 도달 ADFSSmartLockoutEnforce에서 AD FS 모드는 요청을 거부 엑스트라넷에서 관찰 창 경과할 때까지 합니다.  AD FS는 ADFSSmartLockoutLogOnly 모드로 로그 항목을 작성 합니다.  
- **ExtranetObservationWindow &lt;TimeSpan&gt;**  기간 사용자 이름 및 암호에 대 한 알 수 없는 위치에서 요청이 잠겨 지를 결정 합니다. AD FS는 창에 전달 되 면 사용자 이름 및 암호 인증을 다시 수행 하기 시작 합니다.

> [!NOTE]
> AD FS 엑스트라넷 잠금 AD 잠금 정책에서 독립적으로 작동 합니다. 설정 하는 것을 권장 합니다 **ExtranetLockoutThreshold** AD 계정 잠금 임계값 보다 작은 값으로 매개 변수 값입니다. 이렇게 하려면 실패 한 AD FS에서 Active Directory에서 잠긴 계정을 보호 하는 것으로 반환 됩니다. 

Ad FS 2019에서 알려진 좋은 위치로 특정 새 잠금 임계값을 도입 했습니다. ExtranetLockoutThresholdFamiliarLocation.
- **ExtranetLockoutThresholdFamiliarLocation &lt;정수&gt;**  이 익숙한 위치에서 잘못 된 암호 시도의 최대 수를 정의 합니다. Ad FS 2019에서 원래 매개 변수 ExtranetLockoutThreshold 알 수 없는 위치 (IP 주소 수를 알 수 없는)에 적용 됩니다.

### <a name="primary-domain-controller-requirement"></a>주 도메인 컨트롤러 요구 사항
AD FS 2016 PDC를 사용할 수 없는 경우 다른 도메인 컨트롤러에 대체 (fallback)를 허용 하는 매개 변수를 제공 합니다.

- **ExtranetLockoutRequirePDC &lt;부울&gt;**  엑스트라넷 잠금 주 도메인 컨트롤러 (PDC) 사용 하도록 설정 하는 경우 필요 합니다. 사용 하지 않도록 설정, 엑스트라넷 잠금 PDC를 사용할 수 없는 경우 다른 도메인 컨트롤러에 대체가 됩니다.

   다음 예제에서는 cmdlet을 사용 하지 않도록 설정 PDC 필요가 있는 잠금을 사용 하도록 설정 합니다.

    ```powershell
    Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow (new-timespan -Minutes 30) -ExtranetLockoutRequirePDC $false
    ```

## <a name="configuring-ad-fs-with-smart-lockout-in-log-only-mode"></a>스마트 잠금 로그 전용 모드에서를 사용 하 여 AD FS를 구성합니다.

### <a name="ad-fs-2016"></a>AD FS 2016
다음 cmdlet을 실행 하 여만 기록 잠금 동작을 먼저 설정 하는 것이 좋습니다.

 ```powershell
PS C:\>Set-AdfsProperties -ExtranetLockoutMode AdfsSmartlockoutLogOnly
 ```

이 모드에서는 AD FS 보안 감사 이벤트를 기록 하며 모든 요청을 차단 하지 않습니다 사용자 친숙 한 위치 정보를 채웁니다.  이 모드는 스마트 잠금 실행 되 고 AD를 사용 하도록 설정 하려면 사용자에 대 한 친숙 한 위치를 사용 하도록 설정 하기 전에 "알아보려면" FS "강제 적용" 모드는 유효성 검사에 사용 됩니다.
AD FS 학습 하는 대로 저장 사용자별 로그인 작업 (로그 전용 모드에서 든 또는 강제 적용 모드). 

>[!NOTE]
>구성 `ExtranetLockoutMode` 하 `AdfsSmartlockoutLogOnly` 적용 되어 더 이상 레거시 AD FS "엑스트라넷 소프트 잠금" 동작 하면 경우에는 `EnableExtranetLockout` 속성이 True로 설정 됩니다.  이 친숙 한 또는 알 수 없는 IP 주소에서의 잠금 임계값을 초과 하는 사용자가 잠기지 않도록 AD FS에 대 한 스마트 잠금에 의해 것을 의미 합니다. 그러나 온-프레미스 AD 잠금 여기에 구성을 기반으로 사용자를 수 있습니다.   참조 하세요 [계정 잠금 정책](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/account-lockout-policy) 알아보려면 어떻게 온-프레미스 AD 잠금 사용자 수 있습니다. "  이 임시 상태 시스템 다시 새 스마트 잠금 동작을 사용 하 여 잠금 적용을 소개 하기 전에 로그인 동작을 알 수 있도록 할 것입니다.

적용 하려면 새 모드에서는 팜의 모든 노드에서 AD FS 서비스를 다시 시작
  
  ``` powershell
PS C:\>Restart-service adfssrv
  ```
스마트 잠금 사용 하 여 설정할 수 있습니다. 모드를 구성한 후의 `EnableExtranetLockout` 매개 변수


``` powershell
PS C:\>Set-AdfsProperties -EnableExtranetLockout $true
```

잠금 해제 하려면 동일한 cmdlet을 사용할 수 있습니다 note

예: 잠금 해제

``` powershell
PS C:\>Set-AdfsProperties -EnableExtranetLockout $false
```
### <a name="ad-fs-2019"></a>AD FS 2019
현재 AD FS 엑스트라넷 소프트 잠금을 사용 하지 않는 경우 AD FS 2016 위의 경우와 동일한 지침을 따르는 것이 좋습니다.
소프트 잠금을 사용 하는 경우 좋습니다 소프트 잠금 적용을 사용 하 여 유지 하지만 스마트 잠금에 대 한 로그를 AD FS 2019 잠금 동작을 설정 하는 아래 powershell:

 ```powershell
PS C:\>Set-AdfsProperties -ExtranetLockoutMode 3
 ```

이 cmdlet을 실행 하면 ExtranetLockoutMode AD FS 속성의 값을 쿼리할 Get-adfsproperties 사용할 수 있습니다.  ADPasswordCounter 및 ADFSSmartLockoutLogOnly의 조합에 해당 값이 업데이트 되었는지를 표시 됩니다.

## <a name="observing-audit-events"></a>감사 이벤트를 관찰합니다.
AD FS 엑스트라넷 잠금 이벤트는 보안 감사 로그에 작성 합니다.
-   사용자가 차단 하는 경우 아웃 (실패 한 로그인 시도 대 한 잠금 임계값에 도달)
-   AD FS 잠금 상태에서 이미 사용자에 대 한 로그인 시도 수신 하는 경우

로그 전용 모드에서 작업 하는 동안 잠금 이벤트에 대 한 보안 감사 로그를 확인할 수 있습니다.  찾을 수 있는 이벤트에 대 한 잠금이 발생 한 경우 두 번 확인 하는 친숙 한 또는 알 수 없는 IP 주소에서 해당 사용자에 대 한 친숙 한 IP 주소 목록을 결정할 ADFSAccountActivity Get cmdlet을 사용 하 여 사용자 상태를 확인할 수 있습니다.

예제 이벤트:
```
Log Name:      Security
Source:        AD FS Auditing
Date:          5/21/2018 12:55:59 AM
Event ID:      1210
Task Category: (3)
Level:         Information
Keywords:      Classic,Audit Failure
User:          CONTOSO\adfssvc
Computer:      ADFS2016FS1.corp.contoso.com
Description:
An extranet lockout event has occurred. See XML for failure details. 

Activity ID: fa7a8052-0694-48f0-84e2-b51cde40ac3d 

Additional Data 
XML: <?xml version="1.0" encoding="utf-16"?>
<AuditBase xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="ExtranetLockoutAudit">
  <AuditType>ExtranetLockout</AuditType>
  <AuditResult>Failure</AuditResult>
  <FailureType>ExtranetLockoutError</FailureType>
  <ErrorCode>AccountRestrictedAudit</ErrorCode>
  <ContextComponents>
    <Component xsi:type="ResourceAuditComponent">
      <RelyingParty>http://fs.contoso.com/adfs/services/trust</RelyingParty>
      <ClaimsProvider>N/A</ClaimsProvider>
      <UserId>CONTOSO\user</UserId>
    </Component>
    <Component xsi:type="RequestAuditComponent">
      <Server>N/A</Server>
      <AuthProtocol>WSFederation</AuthProtocol>
      <NetworkLocation>Extranet</NetworkLocation>
      <IpAddress>64.187.173.10</IpAddress>
      <ForwardedIpAddress>64.187.173.10</ForwardedIpAddress>
      <ProxyIpAddress>N/A</ProxyIpAddress>
      <NetworkIpAddress>N/A</NetworkIpAddress>
      <ProxyServer>ADFS2016PROXY2</ProxyServer>
      <UserAgentString>Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36</UserAgentString>
      <Endpoint>/adfs/ls/</Endpoint>
    </Component>
    <Component xsi:type="LockoutConfigAuditComponent">
      <CurrentBadPasswordCount>5</CurrentBadPasswordCount>
      <ConfigBadPasswordCount>5</ConfigBadPasswordCount>
      <LastBadAttempt>05/21/2018 00:55:05</LastBadAttempt>
      <LockoutWindowConfig>00:30:00</LockoutWindowConfig>
    </Component>
  </ContextComponents>
</AuditBase>
Event Xml:
<Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event">
  <System>
    <Provider Name="AD FS Auditing" />
    <EventID Qualifiers="0">1210</EventID>
    <Level>0</Level>
    <Task>3</Task>
    <Keywords>0x8090000000000000</Keywords>
    <TimeCreated SystemTime="2018-05-21T00:55:59.921880300Z" />
    <EventRecordID>35521235</EventRecordID>
    <Channel>Security</Channel>
    <Computer>ADFS2016FS1.contoso.com</Computer>
    <Security UserID="S-1-5-21-1156273042-1594504307-2076964089-1104" />
  </System>
  <EventData>
    <Data>fa7a8052-0694-48f0-84e2-b51cde40ac3d</Data>
    <Data><?xml version="1.0" encoding="utf-16"?>
<AuditBase xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="ExtranetLockoutAudit">
  <AuditType>ExtranetLockout</AuditType>
  <AuditResult>Failure</AuditResult>
  <FailureType>ExtranetLockoutError</FailureType>
  <ErrorCode>AccountRestrictedAudit</ErrorCode>
  <ContextComponents>
    <Component xsi:type="ResourceAuditComponent">
      <RelyingParty>http://fs.contoso.com/adfs/services/trust</RelyingParty>
      <ClaimsProvider>N/A</ClaimsProvider>
      <UserId>CONTOSO\user</UserId>
    </Component>
    <Component xsi:type="RequestAuditComponent">
      <Server>N/A</Server>
      <AuthProtocol>WSFederation</AuthProtocol>
      <NetworkLocation>Extranet</NetworkLocation>
      <IpAddress>64.187.173.10</IpAddress>
      <ForwardedIpAddress>64.187.173.10</ForwardedIpAddress>
      <ProxyIpAddress>N/A</ProxyIpAddress>
      <NetworkIpAddress>N/A</NetworkIpAddress>
      <ProxyServer>ADFS2016PROXY2</ProxyServer>
      <UserAgentString>Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36</UserAgentString>
      <Endpoint>/adfs/ls/</Endpoint>
    </Component>
    <Component xsi:type="LockoutConfigAuditComponent">
      <CurrentBadPasswordCount>5</CurrentBadPasswordCount>
      <ConfigBadPasswordCount>5</ConfigBadPasswordCount>
      <LastBadAttempt>05/21/2018 00:55:05</LastBadAttempt>
      <LockoutWindowConfig>00:30:00</LockoutWindowConfig>
    </Component>
  </ContextComponents>
</AuditBase></Data>
  </EventData>
</Event>
```

## <a name="observing-user-activity"></a>사용자 활동을 관찰합니다.
AD FS 사용자 계정 활동 데이터 보기 및 관리 하는 powershell cmdlet을 제공 합니다.  사용자 계정에 대 한 현재 계정 활동을 읽습니다.  아래 cmdlet를 사용 합니다.

``` powershell
PS C:\>Get-ADFSAccountActivity user@contoso.com
```

예제 출력
```
Identifier             : CONTOSO\user
BadPwdCountFamiliar    : 0
BadPwdCountUnknown     : 0
LastFailedAuthFamiliar : 1/1/0001 12:00:00 AM
LastFailedAuthUnknown  : 1/1/0001 12:00:00 AM
FamiliarLockout        : False
UnknownLockout         : False
FamiliarIps            : {}
```

현재 활동 출력에는 다음 데이터가 포함 됩니다.

**식별자**:이 사용자 이름

**BadPwdCountFamiliar**:이 값은 잘못 된 암호 로그인 시도 시도 시 "FamiliarIps" 목록에는 IP 주소에서의 현재 개수

**BadPwdCountUnknown**:이 값은 잘못 된 암호 로그인 시도 되지 않은 "FamiliarIps" 목록에서 시도 시 IP 주소에서의 현재 개수

**LastFailedAuthFamiliar**: 시도 시 "FamiliarIps" 목록에 있는 IP 주소의 마지막 잘못 된 암호 로그인 시도의 시간

**LastFailedAuthUnknown**: 시도 시 "FamiliarIps" 목록에 없는 IP 주소에서 마지막 잘못 된 암호 로그인 시도의 시간

**FamiliarLockout**:이 경우 사용자가 현재 잠금 상태에서 올바른 암호 "FamiliarIps" 목록에 IP 주소에서 시도 대 한 나타냅니다 

**UnknownLockout**:이 경우 사용자가 현재 잠금 상태에서 올바른 암호 "FamiliarIps" FamiliarIps의 목록에 없는 IP 주소에서 시도 대 한 나타냅니다: 현재 사용자에 대 한 친숙 한 IP 주소의 목록

## <a name="adjust-threshold-and-window"></a>조정 임계값 및 창
일단 로그인 위치에 알아보려면 AD FS에 대 한 충분 한 기간에 대 한 실행 로그 전용 모드에서 되었습니다, 기본 설정에서 임계값 또는 관찰 창을 조정할 수도 있습니다.  이렇게 사용 하 여 `Set-AdfsProperties` 아래 예제와 같이:

관찰 창을 사용 하 여 설정 됩니다 `ExtranetObservationWindow`:

예: 

``` powershell
PS C:\>Set-AdfsProperties -ExtranetObservationWindow ( new-timespan -minutes 30 )
```

값은 TimeSpan

### <a name="setting-threshold-value-in-ad-fs-2016"></a>AD FS 2016에서에서 임계값을 설정합니다.
AD FS 2016에서는 임계값 ExtranetLockoutThreshold를 사용 하 여 설정 됩니다.

예:

``` powershell
PS C:\>Set-AdfsProperties -ExtranetLockoutThreshold 5
```

### <a name="setting-threshold-values-in-ad-fs-2019"></a>AD FS 2019에서에서 임계값을 설정합니다.
AD FS 2019에에서는 알려진된 좋은 및 알 수 없는 위치에 대 한 고유한 임계값

알 수 없는 위치에 대 한 임계값을 설정 하려면 위의 AD FS 2016에 사용 되는 동일한 속성을 사용 합니다.

예:

``` powershell
PS C:\>Set-AdfsProperties -ExtranetLockoutThreshold 5
```

알려진된 적절 한 위치에 대 한 임계값을 설정 하려면 아래 예제 에서처럼 ExtranetLockoutThresholdFamiliarLocation, 새 속성을 사용 합니다.

예:

``` powershell
PS C:\>Set-AdfsProperties -ExtranetLockoutThresholdFamiliarLocation 10
```


## <a name="enable-enforce-mode"></a>강제 적용 모드 사용
AD FS 로그인 위치에 알아보려면 및 모든 잠금 동작을 관찰 하기에 충분 한 시간에 대 한 로그 전용 모드에서 실행 했습니다 후 스마트 잠금 모드를 사용 하 여 "적용"로 이동할 수 있습니다 잠금 임계값 및 관찰 창을 사용 하 여 편리 하 게 控 制 합니다 아래 PSH cmdlet:

``` powershell
PS C:\>Set-AdfsProperties -ExtranetLockoutMode AdfsSmartLockoutEnforce
```

적용 하려면 새 모드에서는 팜의 모든 노드에서 AD FS 서비스를 다시 시작

``` powershell
PS C:\>Restart-service adfssrv
```


## <a name="manage-user-account-activity"></a>사용자 계정 활동 관리
AD FS 사용자 계정 활동 데이터를 관리 하는 3 개의 cmdlet을 제공 합니다.  이러한 cmdlet은 마스터 역할을 보유 하는 팜에 있는 노드를 자동으로 연결 (전달 하 여이 동작을 재정의할 수 있지만-Server 매개 변수).

> [!NOTE] 
> 이러한 cmdlet을 사용 하 여에 대 한 권한을 위임에 대 한 내용은 참조 [대리자 AD FS Powershell Commandlet에 대 한 액세스 비관리자 사용자](delegate-ad-fs-pshell-access.md)

이러한 cmdlet은:

`Get-ADFSAccountActivity`

사용자 계정에 대 한 현재 계정 활동을 읽습니다.  Cmdlet은 항상 자동으로 마스터에 연결 하는 팜 계정 활동 REST 끝점을 사용 하 여 모든 데이터가 항상 일치 해야

``` powershell
Get-ADFSAccountActivity user@contoso.com
```
`
Set-ADFSAccountActivity
`

사용자 계정에 대 한 계정 활동을 업데이트 합니다.  이 새 친숙 한 위치를 추가 하 여 모든 계정에 대 한 상태를 지울 수 있습니다.

``` powershell
Set-ADFSAccountActivity user@upnsuffix.com -FamiliarLocation “1.2.3.4”
```
`Reset-ADFSAccountLockout`

사용자 계정 잠금 카운터를 다시 설정

``` powershell
Reset-ADFSAccountLockout user@upnsuffix.com -Familiar
```

## <a name="troubleshooting-esl"></a>ESL 문제 해결
다음 도움이 될 수 있습니다 엑스트라넷 스마트 잠금 기능 문제를 해결 합니다.

### <a name="updating-database-permissions-for-esl"></a>ESL에 대 한 데이터베이스 사용 권한 업데이트
오류에서 반환 되는 경우는 `Update-AdfsArtifactDatabasePermission` cmdlet에서 다음을 확인 합니다

1.  팜 노드 목록이 정확있지 않습니다.  노드는 AD FS 팜은 되지만 활성 패치 확인에 실패 하는 더 이상.  실행 하 여이 문제를 해결할 수 있습니다. `remove-adfsnode <node name >`
2.  패치를는 팜의 모든 노드에서 배포 되었는지 확인
3.  Ad fs 아티팩트 데이터베이스 스키마의 소유자를 수정할 수 있는 권한이 cmdlet으로 전달 하는 자격 증명을 확인 합니다.  

### <a name="logging--auditing"></a>로깅/감사
AD FS 작성 계정 잠금 임계값을 초과 하기 때문에 인증 요청이 거부 되는 경우는 `ExtranetLockoutEvent` 보안 감사 스트림에 합니다.  

예제 이벤트:

엑스트라넷 잠금 이벤트 발생 했습니다. 오류 세부 정보에 대 한 XML을 참조 하세요. 

**활동 ID: 172332e1-1301-4e56-0e00-0080000000db**

```
Additional Data 
XML: <?xml version="1.0" encoding="utf-16"?>
<AuditBase xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="ExtranetLockoutAudit">
  <AuditType>ExtranetLockout</AuditType>
  <AuditResult>Failure</AuditResult>
  <FailureType>ExtranetLockoutError</FailureType>
  <ErrorCode>AccountRestrictedAudit</ErrorCode>
  <ContextComponents>
    <Component xsi:type="ResourceAuditComponent">
      <RelyingParty>http://contoso.com/adfs/services/trust</RelyingParty>
      <ClaimsProvider>N/A</ClaimsProvider>
      <UserId>TQDFTD\Administrator</UserId>
    </Component>
    <Component xsi:type="RequestAuditComponent">
      <Server>N/A</Server>
      <AuthProtocol>WSFederation</AuthProtocol>
      <NetworkLocation>Intranet</NetworkLocation>
      <IpAddress>4.4.4.4</IpAddress>
      <ForwardedIpAddress />
      <ProxyIpAddress>1.2.3.4</ProxyIpAddress>
      <NetworkIpAddress>1.2.3.4</NetworkIpAddress>
      <ProxyServer>N/A</ProxyServer>
      <UserAgentString>Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.132 Safari/537.36</UserAgentString>
      <Endpoint>/adfs/ls</Endpoint>
    </Component>
    <Component xsi:type="LockoutConfigAuditComponent">
      <CurrentBadPasswordCount>5</CurrentBadPasswordCount>
      <ConfigBadPasswordCount>5</ConfigBadPasswordCount>
      <LastBadAttempt>02/07/2018 21:47:44</LastBadAttempt>
      <LockoutWindowConfig>00:30:00</LockoutWindowConfig>
    </Component>
  </ContextComponents>
</AuditBase>

```

## <a name="banned-ip-addresses"></a>금지 된 IP 주소
엑스트라넷 스마트 잠금 기능 외에 AD FS 2018 년 6 월 업데이트를 구성할 수 있습니다 IP 주소 집합을 전체적으로 AD FS에서 또는 해당 IP 주소에서 들어오는 요청 해당 IP 주소를 가질 수 있도록는 **x-전달 기능에 대 한**  나 **x-ms-전달-클라이언트-ip** 헤더, AD FS에서 차단 됩니다.

##### <a name="adding-banned-ips"></a>Ip 차단 추가
전역 목록에 금지 된 Ip를 추가 하려면 사용는 아래 Powershell cmdlet:

``` powershell
PS C:\ >Set-AdfsProperties -AddBannedIps "1.2.3.4", "::3", "1.2.3.4/16"
```

허용 된 형식

1.  IPv4
2.  IPv6
3.  IPv4 또는 v6을 사용 하 여 CIDR 형식
4.  IPv4 또는 v6을 사용 하 여 IP 범위 (예: 1.2.3.4-1.2.3.6)

#### <a name="removing-banned-ips"></a>Ip 차단 제거
전역 목록에서 금지 된 Ip를 제거 하려면 사용는 아래 Powershell cmdlet:

``` powershell
PS C:\ >Set-AdfsProperties -RemoveBannedIps "1.2.3.4"
```

#### <a name="read-banned-ips"></a>Ip를 차단 하는 읽기
금지 된 IP 주소의 현재 집합을 읽으려면 사용은 아래 Powershell cmdlet:

``` powershell
PS C:\ >Get-AdfsProperties 
```

출력의 예:

```
BannedIpList                   : {1.2.3.4, ::3,1.2.3.4/16}
```



## <a name="additional-references"></a>추가 참조  
[Active Directory Federation Services 보안에 대 한 모범 사례](../../ad-fs/deployment/best-practices-securing-ad-fs.md)

[Set-AdfsProperties](https://technet.microsoft.com/itpro/powershell/windows/adfs/set-adfsproperties)

[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)

    
