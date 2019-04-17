---
ms.assetid: 155abe09-6360-4913-8dd9-7392d71ea4e6
title: "문제 해결을 위해 컴퓨터 구성"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 915b8d1133b3bee050f5eedce9e7ac445f833048
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="configuring-a-computer-for-troubleshooting"></a>문제 해결을 위해 컴퓨터 구성

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


<developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>고급 문제 해결 방법을 확인 하 고 Active Directory 문제 해결을 사용 하기 전에 문제 해결을 위해 컴퓨터를 구성 합니다. 기본적으로 알고 있어야 <token>nextref_longhorincludes > 개념, 절차 및 도구 문제를 해결 합니다. </para>
    <para>Windows Server 2008 용 모니터링 도구에 대 한 정보를 참조 하세요.는 Step-by-Step 성능 및 안정성 Windows Server 2008에서 모니터링 가이드 (<externalLink><linkText>https://go.microsoft.com/fwlink/?LinkId=123737</linkText><linkUri>https://go.microsoft.com/fwlink/?LinkId=123737</linkUri></externalLink>).</para>
  </introduction>
  <section>
    <title>문제 해결에 대 한 구성 작업</title>
    <content>
      <para>Active Directory Domain Services (AD DS)의 문제 해결을 위해 컴퓨터를 구성 하려면 다음과 같은 작업을 수행:</para>
      <para>
        <link xlink:href="#BKMK_2">AD DS에 대 한 원격 서버 관리 도구를 설치</link>
      </para>
      <para>
        <link xlink:href="#BKMK_3">구성 안정성 및 성능이 모니터</link>
      </para>
      <para>
        <link xlink:href="#BKMK_4">로깅 수준을 설정할</link>
      </para>
    </content>
    <sections>
      <section address="BKMK_2">
        <title>AD DS에 대 한 원격 서버 관리 도구를 설치</title>
        <content>
          <para>AD DS 만드는 도메인 컨트롤러를 설치 하면 관리 도구 AD DS 관리를 사용 하는 자동으로 설치 됩니다. 실행 중인 구성원 서버에 관리 도구를 설치할 수는 도메인 컨트롤러 된 컴퓨터에서 도메인 컨트롤러를 원격으로 관리 하려면 <token>nextref_longhorincludes > 또는 Windows Vista 서비스 팩 1 (SP1)을 실행 하는 컴퓨터에서 합니다. 실행 중인 구성원 서버의 <token>nextref_longhorincludes >, 기능을 사용 하면 원격 서버 관리 도구 RSAT () 서버 관리자의 Active Directory Domain Services 도구를 설치 해야 합니다. RSAT은 Windows Server 2003에서 Windows 지원 도구를 대체합니다. Windows Vista 서비스 팩 1 (SP1)을 실행 하는 컴퓨터에 대 한 Active Directory Domain Services 도구 해당 컴퓨터에 도구를 다운로드 하 여 설치할 수도 있습니다.</para>
          <para>RSAT 설치에 대 한 정보를 참조 하세요. <link xlink:href="610ba7d9-51b5-4e14-9232-0510a9091aba">AD DS에 대 한 원격 서버 관리 도구를 설치</link>합니다.</para>
        </content>
      </section>
      <section address="BKMK_3">
        <title>안정성 및 성능이 모니터 구성</title>
        <content>
          <para>Windows의 안정성 및은 이전 독립 실행형 도구를 성능 로그 및 알림, 서버 성능을 관리자 시스템 모니터 등의 기능을 결합 하는 Microsoft Management Console (MMC) 스냅인 성능 모니터, Windows Server 2008 포함 됩니다. 이 스냅인 수집기 데이터 집합 및 이벤트 추적 세션을 사용자 지정 하기 위한는 그래픽 GUI (사용자 인터페이스)을 제공 합니다.</para>
          <para>안정성 및 성능이 모니터도 포함 되어 있는 MMC 스냅인 시스템 변경 사항을 추적 하 고 시스템 안정성을 높이고의 변경을 비교 안정성 모니터와의 관계의 그래픽 보기를 제공 합니다.</para>
        </content>
      </section>
      <section address="BKMK_4">
        <title>로깅 수준을 설정</title>
        <content>
          <para>이벤트 뷰어에서 디렉터리 서비스 로그에 수신 되는 정보 문제 해결에 대 한 충분 하지 않은 경우 로그인 수준에서 적절 한 레지스트리 항목이 활성화 된를 사용 하 여 올리기 <embeddedLabel>HKEY_LOCAL_MACHINESYSTEMCurrentControlSetServicesNTDSDiagnostics</embeddedLabel>합니다.</para>
          <para>기본적으로 모든 항목에 대 한 로그인 수준을 설정 <embeddedLabel>0</embeddedLabel>, 최소한의 정보를 제공 하는 합니다. 최상위 로깅은 <embeddedLabel>5</embeddedLabel>합니다. 항목에 대 한 수준을 높이 이벤트가 추가 디렉터리 서비스 이벤트 로그에 기록 됩니다.</para>
          <para>진단 항목에 대해 로깅을 수준을 변경 하려면 다음 절차를 사용할 수 있습니다.</para>
          <alert class="caution">
            <para>는 편집 하지 않으면 직접 레지스트리 다른 대안이 않는 것이 좋습니다. 레지스트리에 대 한 수정 하지 유효성을 검사는 레지스트리 편집기 또는 Windows를 적용 되기 전에 결과적으로, 잘못 된 값 저장할 수 있습니다. 이 시스템에서 복구할 수 없는 오류가 발생할 수 있습니다. 가능 하면 레지스트리 직접 편집 하는 것이 아니라 작업을 수행할 수 그룹 정책 또는 MMC 스냅인와 같은 다른 Windows 도구를 사용 합니다. 레지스트리를 편집 해야 하는 경우 주의 합니다.</para>
          </alert>
          <para>
            <embeddedLabel>요구</embeddedLabel>
          </para>
          <list class="bullet">
            <listItem>
              <para><embeddedLabel>도메인 관리자</embeddedLabel>, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다. <token>review_detailincludes ></para>
            </listItem>
            <listItem>
              <para>도구: Regedit.exe</para>
            </listItem>
          </list>
          <procedure>
            <title>진단 항목에 대해 로깅을 수준을 변경 하려면</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>클릭 <ui>시작</ui>, 클릭 <ui>실행</ui>, 입력 <userInput>regedit</userInput>, 클릭 한 다음 <ui>확인</ui>합니다.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>로그인 설정 하려는 항목을 탐색 <embeddedLabel>HKEY_LOCAL_MACHINESYSTEMCurrentControlSetServicesNTDSDiagnostics</embeddedLabel>합니다.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>에서 항목 두 번의 <embeddedLabel>자료</embeddedLabel>, 클릭 <embeddedLabel>소수점</embeddedLabel>합니다.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>에서 <embeddedLabel>값</embeddedLabel>에서 정수 입력 <embeddedLabel>0</embeddedLabel> 통해 <embeddedLabel>5</embeddedLabel>를 차례로 클릭 하 고 <ui>확인</ui>합니다.</para>
                </content>
              </step>
            </steps>
          </procedure>
        </content>
      </section>
    </sections>
  </section>
  <relatedTopics />
</developerConceptualDocument>


