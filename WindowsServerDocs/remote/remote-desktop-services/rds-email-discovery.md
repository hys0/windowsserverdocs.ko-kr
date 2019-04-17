---
title: 전자 메일 검색 공급 하 여 RDS를 구독할 수 설정
description: RDS 배포에 Azure AD 도메인 서비스를 통합 하는 방법에 알아봅니다.
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 3/27/2018
ms.localizationpriority: medium
ms.topic: article
author: christianmontoya
ms.openlocfilehash: 5b3f162b8eee70fbc452b7400b737454c3fffb59
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "1691672"
---
# <a name="set-up-email-discovery-to-subscribe-to-your-rds-feed"></a>전자 메일 검색 공급 하 여 RDS를 구독할 수 설정

적이 피드에서 누락 된 단일 문자로 인해 하나는 게시 된 RDS 피드에 연결 된 최종 사용자에 게 시작 하는데 문제가 URL 또는 URL이 포함 된 전자 메일을 손실 하기 때문에 있습니까? 거의 모든 원격 데스크톱 클라이언트 응용 프로그램 보다 훨씬 더 Remoteapp 및 데스크톱에 연결 된 사용자가 쉽게 전자 메일 주소를 입력 하 여 구독 찾기 (영문)를 지원 합니다.

>[!IMPORTANT]
>Microsoft 원격 데스크톱 앱 Microsoft 저장소에는 지금은 전자 메일 주소 구독을 지원 하지 않습니다.

전자 메일 검색을 설정 하기 전에 다음을 수행 합니다.

- 연관 된 전자 메일 도메인에 TXT 레코드를 추가할 수 있는 권한이 있는지 확인 (등 사용자에 게 있으면 @contoso.com 전자 메일 주소를 contoso.com 도메인에 대 한 사용 권한이 필요 합니다)
- 피드 URL RD 웹 만들 (< rdweb dns name\ > https://\.domain/RDWeb/Feed/webfeed.aspx와 같은https://rdweb.contoso.com/RDWeb/Feed/webfeed.aspx)

이제 다음이 단계를 사용 하 여 전자 메일 검색을 설정 하려면:

1. 브라우저에서 도메인 등록 되어 있는 도메인 이름 등록자의 웹사이트에 연결 합니다.
2. 보고, 추가, 하 고 수 있는 DNS 레코드를 편집할 등록 된 도메인에 대 한 적절 한 페이지로 이동 합니다.
3. 다음 속성을 갖는 새 DNS 레코드를 입력 합니다.
   - **호스트:** _msradc
   - **텍스트:** \ < RD 웹 URL\를 피드 >
   - **TTL:** 300

   도메인 이름 등록자에서 DNS 레코드 필드의 이름을 달라질 수 있지만이 프로세스 _msradc. 라는 TXT 레코드에 발생 합니다 \ < domain_name\ > (예: _msradc.contoso.com)이 설치 된 전체 RD 웹 피드의 값입니다.

그거에요! 이제, 장치에서 원격 데스크톱 응용 프로그램을 시작 하 고 사용자가 직접 구독!