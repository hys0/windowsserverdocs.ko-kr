---
title: "NTLM 개요"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-kerberos
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 773909fd-c0bc-498a-95fc-bb452ec04d90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 523fb71304ae55d17203cab4d1c5a17551bf8fdf
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="ntlm-overview"></a>NTLM 개요

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

IT 전문가 위한이 항목 NTLM, 기능, 모든 변경에 설명 하 고 Windows 및 Windows Server 2012 용 NTLM 인증과에 이전 버전 기술 리소스에 대 한 링크를 제공 합니다.

## <a name="BKMK_OVER"></a>기능 설명
NTLM 인증은 가족의 Windows Msv1\_0.dll에 포함 되는 인증 프로토콜 합니다. NTLM 인증 프로토콜 LAN Manager 버전 1, 2, 및 NTLM 1과 2 버전 포함 합니다. NTLM 인증 프로토콜 사용자와 사용자 계정과 연결 된 암호를 알고 있는 도메인 컨트롤러 서버 또는 입증 하는 challenge\/응답 메커니즘을 기반으로 컴퓨터를 인증 합니다. NTLM 프로토콜을 사용 하는 경우 리소스 서버 새 액세스 토큰 필요할 때마다 컴퓨터 또는 사용자의 신원을 확인 하는 다음 작업 중 하나를 수행 해야 합니다.

-   계정을 도메인 계정인 경우 도메인 컨트롤러에서 도메인 인증 서비스를 컴퓨터 또는 사용자의 계정 도메인에 문의 하세요.

-   계정에서 로컬 계정인 경우 컴퓨터의 또는 사용자의 계정에서 로컬 계정 데이터베이스를 우러러 보세요.

## <a name="BKMK_APP"></a>현재 응용 프로그램
NTLM 인증 여전히 지원 및 작업 그룹의 회원으로 구성 된 시스템 함께 Windows 인증에 사용 해야 합니다. 도 NTLM 인증 non\ 도메인 컨트롤러에서 로컬 로그온 인증을 위해 사용 됩니다. Kerberos 5 버전 인증 Active Directory 환경에 대 한 기본 설정된 인증 방법을 있지만 non\ Microsoft 또는 Microsoft application NTLM 사용 계속 될 수 있습니다.

IT 환경에서 NTLM 프로토콜 사용량을 줄이기 NTLM, 전략 및에 컴퓨팅 환경 구성에 필요한 단계 다른 프로토콜을 사용 하 여 요구 사항을 배포 응용 프로그램 둘 다 기술이 필요 합니다. 선택적 NTLM 교통량을 제한 하려면 NTLM를 사용 하는 방법을 찾을 수 있도록 새로운 도구 및 설정을 추가 되었습니다. 분석 하 고 사용자 환경에서 NTLM 사용을 제한 하는 방법에 대 한 정보를 참조 하세요. [NTLM 제한 인증 소개](https://technet.microsoft.com/library/dd560653(v=ws.10).aspx) 의 감사 NTLM 사용 가이드 제한 하 고 액세스할 수 있습니다.

## <a name="BKMK_NEW"></a>새로운 기능과 변경 된 기능
Windows Server 2012 용 NTLM에 대 한 기능에 없음 변경 사항이 있습니다.

## <a name="BKMK_DEP"></a>제거 하거나 사용 하지 않는 기능
Windows Server 2012 용 NTLM 없는 제거 하거나 사용 하지 않는 기능이 있습니다.

## <a name="BKMK_INSTALL"></a>서버 관리자 정보
NTLM 서버 관리자에서 구성할 수 없습니다. 보안 정책 설정 또는 그룹 정책을 컴퓨터 시스템 간에 NTLM 인증 사용량 관리를 사용할 수 있습니다. 도메인 Kerberos 기본 인증 프로토콜을입니다.

## <a name="BKMK_LINKS"></a>참조 하십시오
다음 표에서 NTLM 및 기타 Windows 인증 기술에 대 한 관련 리소스 보여 줍니다.

|콘텐츠 종류|참조|
|--------|-------|
|**제품 평가**|[NTLM 인증 제한 소개](https://technet.microsoft.com/library/dd560653.aspx)<br /><br />[인증 NTLM 변경](https://technet.microsoft.com/library/dd566199.aspx)|
|**계획**|[IT 인프라 위협 모델링 가이드](https://technet.microsoft.com/library/dd941826.aspx)<br /><br />[위협과 대책: Windows XP 및 Windows Server 2003에 대 한 보안 설정](https://technet.microsoft.com/library/dd162275.aspx)<br /><br />[위협과 대책 가이드: Windows Server 2008 및 Windows Vista의 보안 설정](https://technet.microsoft.com/library/dd349791.aspx)<br /><br />[위협과 대책 가이드: Windows Server 2008 R2 및 Windows 7의 보안 설정](https://technet.microsoft.com/library/hh125921.aspx)|
|**배포**|[인증에 대 한 연장된 보호](https://support.microsoft.com/kb/968389)<br /><br />[감사 및 NTLM 사용 가이드 제한](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)<br /><br />[디렉터리 서비스 팀에 게 물어보기: NTLM 차단 하 고: 응용 프로그램 분석 및 Windows 7에서에서 방법론 감사](https://blogs.technet.com/askds/archive/2009/10/08/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7.aspx)<br /><br />[Windows 인증 블로그](https://blogs.technet.com/authentication/)<br /><br />[MaxConcurrentAPI NTLM pass\ 쓰루 인증에 대 한 구성](https://social.technet.microsoft.com/wiki/contents/articles/9759.configuring-maxconcurrentapi-for-ntlm-pass-through-authentication.aspx)|
|**개발**|[Microsoft NTLM \(Windows\)](https://msdn.microsoft.com/library/aa378749(VS.85).aspx)<br /><br />[\[MS\-NLMP\]: NT LAN Manager \(NTLM\) 인증 프로토콜 사양](https://msdn.microsoft.com/library/cc236621(PROT.10).aspx)<br /><br />[\[MS\-NNTP\]: NT LAN Manager \(NTLM\) 인증: 뉴스 Transfer Protocol \(NNTP\) 확장 네트워크](https://msdn.microsoft.com/library/cc236774(PROT.10).aspx)<br /><br />[\[MS\-NTHT\]: HTTP 프로토콜에 사양 NTLM](https://msdn.microsoft.com/library/cc237488(PROT.10).aspx)|
|**문제 해결**|아직 사용할 수 없음|
|**커뮤니티 리소스**|[아직 작동 하지 않는이 말이은: NTLM 병목 및 RPC 런타임](http://blogs.technet.com/b/askds/archive/2011/09/15/is-this-horse-dead-yet-ntlm-bottlenecks-and-the-rpc-runtime.aspx)|



