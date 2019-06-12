---
title: AD FS 문제 해결
description: 이 문서에서는 AD FS의 다양 한 측면을 해결 하는 방법 설명
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/12/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6410d510085d1772ca6d8ced47226e00239a1a02
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443904"
---
# <a name="troubleshooting-ad-fs"></a>AD FS 문제 해결
AD FS 많은 이동 부분, 다른 많은 요소와 연결 및 많은 다른 종속성이 있습니다.  물론이를 낼 수 있습니다 다양 한 문제입니다.  이 문서는 이러한 문제 해결 시작 하도록 설계 되었습니다.  이 문서에서는 추가 정보 및 문제를 추적에 사용할 수 있는 다양 한 도구에 대 한 기능을 사용 하는 방법에 집중 해야 하는 일반적인 영역에 도입 됩니다.  

>[!NOTE]
>추가 정보를 참조 하세요. [ADFS 도움말](http://adfshelp.microsoft.com) 를 제공 하는 효과적인 도구 하나에 배치 하는 쉽게 사용자와 더 빠른 속도로 인증 문제를 해결 하는 관리자입니다. 


## <a name="what-to-check-first"></a>첫 번째 확인할 사항
자세한 문제 해결 살펴보기 전에 먼저 확인 해야 하는 몇 가지 있습니다.  구현되지 않은 것은 다음과 같습니다.
- **DNS 구성** -페더레이션 서비스의 이름을 확인할 수 있습니까?  이 두 부하 분산 장치의 IP 주소 또는 팜의 AD FS 서버 중 하나의 IP 주소를 확인 합니다.  자세한 내용은 참조 [AD FS 문제 해결-DNS](ad-fs-tshoot-dns.md)합니다.
- **AD FS 끝점** -AD FS 끝점을 찾아볼 수 있습니다.  이로 이동 하 여 AD FS 웹 서버는 요청에 응답 여부를 확인할 수 있습니다.  이 파일을 가져올 수 있습니다, 것을 알 수는 AD FS는 요청을 처리 443 제대로 초과 합니다.  자세한 내용은 참조 [AD FS 끝점 문제 해결-](ad-fs-tshoot-endpoints.md)합니다.
- **Sign On Idp에서 시작한** -로그인 서 Idp-Initiated Sign-on 페이지를 통해 인증할 수 있습니까?  기본적으로 비활성화 되어 있으므로이 페이지를 사용할 수 있도록 해야 합니다.  사용 하 여 `Set-AdfsProperties -EnableIdPInitiatedSignOn $true` 페이지를 사용 하도록 설정 합니다.  로그인 하 고 인증 하는 경우이 영역에 AD FS가 작동 하는지 알고 다음입니다.  자세한 내용은 참조 [AD FS 문제 해결-SignOn](ad-fs-tshoot-initiatedsignon.md)합니다.
  ##  <a name="common-troubleshooting-areas"></a>일반적인 문제 해결 영역

|이름|설명|
|-----|-----|
|[이벤트 로깅 및 감사](ad-fs-tshoot-logging.md)|높은 수준 및 정보를 보려면 하위 수준 관리 및 추적 로그를 통해 Windows 이벤트 로그를 사용 합니다.  보안 감사 보려는 데도 수 있습니다.|
|[SQL 연결](ad-fs-tshoot-sql.md)|AD FS 서버와 백 엔드 SQL 데이터베이스 간의 연결을 테스트 하는 방법|
|[클레임 발급](ad-fs-tshoot-claims-issuance.md)|AD FS 클레임 올바르게 발급 하는지 여부를 확인 하는 정보입니다.|
|[루프 검색](ad-fs-tshoot-loop.md)|결정 Idp와 RP 간에 앞뒤로 반송 중에서 사용자를 방지에 대 한 정보입니다.|
|[인증서](ad-fs-tshoot-certs.md)|발생할 수 있는 경우 인증서 문제|
|[Fiddler](ad-fs-tshoot-fiddler.md)|Fiddler를 사용 하 여 및 설치 하는 방법에 대 한 정보|
|[Fiddler 사용 하 여 Ws-federation](ad-fs-tshoot-fiddler-ws-fed.md)|WS-페더레이션 상호 작용 하는 자세한 Fiddler 추적|
|[클레임 규칙](ad-fs-tshoot-claims-rules.md)|클레임 규칙 및 구문의 문제 해결에 대 한 정보|
|[통합된 Windows 인증](ad-fs-tshoot-iwa.md)|통합된 인증 문제 해결에 대 한 정보입니다.|
|[Azure AD](ad-fs-tshoot-azure.md)|Azure AD 사용 하 여 AD FS 상호 작용 문제 해결에 대 한 정보입니다.|
|[AD FS 진단 분석기](ad-fs-diagnostics-analyzer.md)|AD FS 도움말 진단 분석기 진단 PowerShell 모듈을 사용 하는 기본 AD FS 검사를 수행 하는 데 도움이 됩니다. 