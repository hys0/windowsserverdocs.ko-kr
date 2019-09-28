---
title: NTLM 개요
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: b8dec2877646fd2bfe00da9d5c9047e8edfd6f1d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386264"
---
# <a name="ntlm-overview"></a>NTLM 개요

>적용 대상: Windows Server(반기 채널), Windows Server 2016

IT 전문가를 위한이 항목에서는 NTLM, 기능의 변경 내용에 대해 설명 하 고 windows Server 2012 및 이전 버전에 대 한 Windows 인증 및 NTLM에 대 한 기술 리소스 링크를 제공 합니다.

## <a name="BKMK_OVER"></a>기능 설명
NTLM 인증은 Windows Msv1\_0.dll에 들어 있는 인증 프로토콜 제품군입니다. NTLM 인증 프로토콜에는 LAN Manager 버전 1, 2 및 NTLM 버전 1, 2가 포함됩니다. NTLM 인증 프로토콜은 사용자가 계정과 연결 된 암호를 알고 있음을 서버나 도메인 컨트롤러에 증명 하는 챌린지 @ no__t-0response 메커니즘을 기반으로 사용자와 컴퓨터를 인증 합니다. NTLM 프로토콜을 사용하는 경우 리소스 서버는 다음 작업 중 하나를 수행하여 새 액세스 토큰이 필요할 때마다 컴퓨터 또는 사용자의 ID를 확인해야 합니다.

-   계정이 도메인 계정인 경우 도메인 컨트롤러의 도메인 인증 서비스에 컴퓨터 또는 사용자의 계정 도메인을 문의합니다.

-   계정이 로컬 계정인 경우 로컬 계정 데이터베이스에서 컴퓨터 또는 사용자의 계정을 조회합니다.

## <a name="BKMK_APP"></a>현재 응용 프로그램
NTLM 인증은 계속 지원되며, 이는 작업 그룹 구성원으로 구성된 시스템에서 Windows 인증 시 사용되어야 합니다. NTLM 인증은 비 @ no__t-0domain 컨트롤러의 로컬 로그온 인증에도 사용 됩니다. Kerberos 버전 5 인증은 Active Directory 환경을 위한 기본 인증 방법 이지만 @ no__t-0Microsoft 또는 Microsoft 응용 프로그램에서 NTLM을 계속 사용할 수 있습니다.

IT 환경에서 NTLM 프로토콜 사용을 줄이려면 NTLM을 기반으로 배포된 애플리케이션 요구 사항에 대한 지식과 기타 프로토콜을 사용하도록 컴퓨팅 환경을 구성하는 데 필요한 전략 및 단계가 필요합니다. 선택적으로 NTLM 트래픽을 제한하기 위해 NTLM 사용 방법을 검색하도록 도와주는 새로운 도구 및 설정이 추가되었습니다. 환경에서 NTLM 사용을 분석 및 제한하는 방법에 대한 자세한 내용은 [NTLM 인증 제한 사항 소개](https://technet.microsoft.com/library/dd560653(v=ws.10).aspx) 를 참조하여 NTLM 사용 감사 및 제한 가이드에 액세스하세요.

## <a name="BKMK_NEW"></a>새로운 기능 및 변경 된 기능
Windows Server 2012에 대 한 NTLM 기능은 변경 되지 않았습니다.

## <a name="BKMK_DEP"></a>제거 되었거나 더 이상 사용 되지 않는 기능
Windows Server 2012에 대 한 NTLM에는 제거 되었거나 더 이상 사용 되지 않는 기능이 없습니다.

## <a name="BKMK_INSTALL"></a>서버 관리자 정보
서버 관리자에서는 NTLM을 구성할 수 없습니다. 보안 정책 설정 또는 그룹 정책을 사용하여 컴퓨터 시스템 간의 NTLM 인증 사용을 관리할 수 있습니다. 도메인의 기본 인증 프로토콜은 Kerberos입니다.

## <a name="BKMK_LINKS"></a>참고 항목
다음 표에서는 NTLM 및 기타 Windows 인증 기술 관련 리소스를 제공합니다.

|콘텐츠 형식|참조|
|--------|-------|
|**제품 평가**|[NTLM 인증 제한 사항 소개](https://technet.microsoft.com/library/dd560653.aspx)<br /><br />[NTLM 인증의 변경 내용](https://technet.microsoft.com/library/dd566199.aspx)|
|**계획**|[IT 인프라 위협 모델링 가이드](https://technet.microsoft.com/library/dd941826.aspx)<br /><br />[Threats 및 대책: Windows Server 2003 및 Windows XP의 보안 설정 @ no__t-0<br /><br />[Threats 및 대책 가이드: Windows Server 2008 및 Windows Vista @ no__t의 보안 설정-0<br /><br />[Threats 및 대책 가이드: Windows Server 2008 R2 및 Windows 7 @ no__t의 보안 설정-0|
|**배포**|[인증에 대한 확장된 보호](https://support.microsoft.com/kb/968389)<br /><br />[NTLM 사용 가이드 감사 및 제한](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)<br /><br />[ 디렉터리 서비스 팀에 문의: NTLM 차단 및 사용자: Windows 7 @ no__t의 응용 프로그램 분석 및 감사 방법론-0<br /><br />[Windows 인증 블로그](https://blogs.technet.com/authentication/)<br /><br />[NTLM pass @ no__t-1through 인증에 대 한 MaxConcurrentAPI 구성](https://social.technet.microsoft.com/wiki/contents/articles/9759.configuring-maxconcurrentapi-for-ntlm-pass-through-authentication.aspx)|
|**개발**|[Microsoft NTLM \(Windows @ no__t-2](https://msdn.microsoft.com/library/aa378749(VS.85).aspx)<br /><br />[ @ NO__T-1MS @ NO__T-2NLMP @ NO__T-3: NT LAN Manager \(NTLM @ no__t 인증 프로토콜 사양 @ no__t-2<br /><br />[ @ NO__T-1MS @ NO__T-2NNTP @ NO__T-3: NT LAN Manager \(NTLM @ no__t 인증: 네트워크 뉴스 전송 프로토콜 \(NNTP @ no__t-1 Extension @ no__t-2<br /><br />[ @ NO__T-1MS @ NO__T-2NTHT @ NO__T-3: NTLM Over HTTP 프로토콜 사양 @ no__t-0|
|**문제 해결**|아직 사용할 수 없음|
|**커뮤니티 리소스**|[은이 목마는 아직 비활성화 되어 있습니다. NTLM 병목 상태 및 RPC 런타임 @ no__t-0|



