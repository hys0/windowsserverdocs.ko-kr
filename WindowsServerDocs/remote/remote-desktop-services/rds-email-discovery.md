---
title: 전자 메일 검색 피드 RDS를 구독할 수 설정
description: RDS 배포에 Azure AD Domain Services를 통합 하는 방법에 알아봅니다.
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 3/27/2018
ms.localizationpriority: medium
ms.topic: article
author: christianmontoya
ms.openlocfilehash: 5b3f162b8eee70fbc452b7400b737454c3fffb59
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878324"
---
# <a name="set-up-email-discovery-to-subscribe-to-your-rds-feed"></a>전자 메일 검색 피드 RDS를 구독할 수 설정

적이 문제가 발생 하는 바람이 인해 피드의 단일 누락 된 문자 중 하나는 게시 된 RDS 피드에 연결할 URL 또는 URL 사용 하 여 전자 메일 사라지므로? 거의 모든 원격 데스크톱 클라이언트 응용 프로그램이 훨씬 더 Remoteapp 및 데스크톱에 연결 된 사용자가 보다 쉽게 사용자의 전자 메일 주소를 입력 하 여 구독을 찾는 것을 지원 합니다.

>[!IMPORTANT]
>Microsoft Store Microsoft 원격 데스크톱 앱에서이 이번에 전자 메일 주소 구독을 지원 하지 않습니다.

전자 메일 검색을 설정 하기 전에 다음을 수행 합니다.

- 전자 메일을 사용 하 여 연결 된 도메인 TXT 레코드를 추가할 수 있는 권한이 있는지 확인 (사용자에 게 제공 하는 경우에 예를 들어 @contoso.com 전자 메일 주소를 contoso.com 도메인에 대 한 권한이 필요)
- 피드 URL RD 웹 만들 (https://\<rdweb dns 이름\>.domain/RDWeb/Feed/webfeed.aspx와 같은 https://rdweb.contoso.com/RDWeb/Feed/webfeed.aspx)

이제 전자 메일 검색을 설정 하려면 다음이 단계를 사용 합니다.

1. 브라우저에서 도메인 등록 되어 있는 도메인 이름 등록자의 웹 사이트에 연결 합니다.
2. 등록 된 도메인이 있습니다 확인에 추가 하 고 있는 DNS 레코드 편집에 대 한 적절 한 페이지로 이동 합니다.
3. 다음 속성을 사용 하 여 새 DNS 레코드를 입력 합니다.
   - **호스트:** _msradc
   - **텍스트:** \<RD 웹 피드 URL\>
   - **TTL:** 300

   도메인 이름 등록자에서 DNS 레코드 필드의 이름이 다를 있지만이 프로세스 _msradc 라는 TXT 레코드에 됩니다. \<domain_name\> 전체 RD 웹 피드의 값이 있는 (예: _msradc.contoso.com).

이것이 전부입니다! 이제 장치에서 원격 데스크톱 응용 프로그램을 시작 하 고 직접 구독!