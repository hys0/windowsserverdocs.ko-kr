---
title: AD FS 문제 해결
description: 이 문서에서는 AD FS의 다양 한 측면을 해결 하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/12/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 5fc5c2384a6d8d13f807a1ce99c5db78bee5b108
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950136"
---
# <a name="troubleshooting-ad-fs"></a>AD FS 문제 해결
AD FS 많은 부분이 이동 하 고 다양 한 작업을 수행 하며 다양 한 종속성이 있습니다.  이렇게 하면 다양 한 문제를 쉽게 파악할 수 있습니다.  이 문서는 이러한 문제 해결을 시작할 수 있도록 설계 되었습니다.  이 문서에서는 초점을 맞춘 일반적인 영역, 추가 정보를 위해 기능을 사용 하도록 설정 하는 방법, 문제를 추적 하는 데 사용할 수 있는 다양 한 도구를 소개 합니다.  

>[!NOTE]
>자세한 내용은 사용자와 관리자가 더 빨리 인증 문제를 더 쉽게 해결할 수 있도록 하는 단일 위치에서 효과적인 도구를 제공 하는 [ADFS 도움말](https://adfshelp.microsoft.com) 을 참조 하세요. 


## <a name="what-to-check-first"></a>먼저 확인 해야 할 사항
심층 문제 해결에 대해 자세히 살펴보기 전에 먼저 확인 해야 할 몇 가지 사항이 있습니다.  채널은 다음과 같습니다.
- **DNS 구성** -페더레이션 서비스의 이름을 확인할 수 있나요?  이는 팜의 AD FS 서버 중 하나의 ip 주소 또는 부하 분산 장치의 ip 주소로 확인 되어야 합니다.  자세한 내용은 [AD FS 문제 해결-DNS](ad-fs-tshoot-dns.md)를 참조 하십시오.
- **AD FS 끝점** -AD FS 끝점을 찾을 수 있나요?  이를 검색 하 여 AD FS 웹 서버가 요청에 응답 하 고 있는지 여부를 확인할 수 있습니다.  이 파일에 액세스할 수 있는 경우 AD FS는 443 이상으로 요청을 처리 하는 것을 알 수 있습니다.  자세한 내용은 [AD FS 문제 해결-끝점](ad-fs-tshoot-endpoints.md)을 참조 하세요.
- **Idp에서 시작 된 로그인** -Idp 시작 로그온 페이지를 통해 로그인 하 고 인증할 수 있나요?  이 페이지는 기본적으로 사용 하지 않도록 설정 되어 있는지 확인 해야 합니다.  `Set-AdfsProperties -EnableIdPInitiatedSignOn $true`를 사용 하 여 페이지를 사용 하도록 설정 합니다.  로그인 하 고 인증할 수 있는 경우 AD FS이이 영역에서 작동 하 고 있음을 알 수 있습니다.  자세한 내용은 [AD FS 문제 해결-SignOn](ad-fs-tshoot-initiatedsignon.md)을 참조 하세요.
  ##  <a name="common-troubleshooting-areas"></a>일반적인 문제 해결 영역

|Name(이름)|설명|
|-----|-----|
|[이벤트 로깅 및 감사](ad-fs-tshoot-logging.md)|Windows 이벤트 로그를 사용 하 여 관리자 및 추적 로그를 통해 높은 수준 및 낮은 수준의 정보를 볼 수 있습니다.  이를 사용 하 여 보안 감사를 볼 수도 있습니다.|
|[SQL 연결](ad-fs-tshoot-sql.md)|AD FS 서버와 백 엔드 SQL 데이터베이스 간의 연결 테스트에 대 한 정보|
|[클레임 발급](ad-fs-tshoot-claims-issuance.md)|AD FS에서 클레임을 올바르게 발급 하는지 여부를 확인 하는 방법에 대 한 정보입니다.|
|[루프 검색](ad-fs-tshoot-loop.md)|사용자를 확인 하 고 Idp RP 간에 반송 됨 하는 것을 방지 하는 방법에 대 한 정보입니다.|
|[인증서](ad-fs-tshoot-certs.md)|발생할 수 있는 typcial 인증서 문제|
|[Fiddler](ad-fs-tshoot-fiddler.md)|Fiddler를 설치 하 고 사용 하는 방법에 대 한 정보|
|[Fiddler를 사용 하는 WS-FEDERATION](ad-fs-tshoot-fiddler-ws-fed.md)|WS-FEDERATION 상호 작용에 대 한 자세한 Fiddler 추적|
|[클레임 규칙](ad-fs-tshoot-claims-rules.md)|클레임 규칙 및 해당 구문 문제 해결에 대 한 정보|
|[통합 Windows 인증](ad-fs-tshoot-iwa.md)|통합 인증 문제 해결에 대 한 정보입니다.|
|[Azure AD](ad-fs-tshoot-azure.md)|Azure AD와의 상호 작용 AD FS 문제 해결에 대 한 정보입니다.|
|[AD FS 진단 분석기](ad-fs-diagnostics-analyzer.md)|AD FS 진단 분석기는 진단 PowerShell 모듈을 사용 하 여 기본 AD FS 검사를 수행 하는 데 도움이 됩니다. 