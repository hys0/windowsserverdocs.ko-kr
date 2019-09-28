---
title: RDS 피드를 구독하도록 이메일 검색 설정
description: RDS 배포에 Azure AD Domain Services를 통합하는 방법을 알아봅니다.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 3/27/2018
ms.localizationpriority: medium
ms.topic: article
author: christianmontoya
ms.openlocfilehash: c56a233adf28270aac809dc960e32b5363e4b8ab
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71387512"
---
# <a name="set-up-email-discovery-to-subscribe-to-your-rds-feed"></a>RDS 피드를 구독하도록 이메일 검색 설정

피드 URL에서 누락된 단일 문자로 인해 또는 URL이 포함된 이메일을 잃어버려서 최종 사용자를 게시된 RDS 피드에 연결하는 데 문제가 있었던 적이 있나요? 거의 모든 원격 데스크톱 클라이언트 애플리케이션은 이메일 주소를 입력하여 구독 찾기를 지원하므로 사용자가 해당 RemoteApps 및 데스크톱에 쉽게 연결할 수 있습니다.

>[!IMPORTANT]
>Microsoft Store에서 Microsoft 원격 데스크톱 앱은 이 때 이메일 주소 구독을 지원하지 않습니다.

이메일 검색을 설정하기 전에 다음을 수행합니다.

- 이메일에 연결된 도메인에 TXT 레코드를 추가할 수 있는 권한이 있는지 확인합니다(예를 들어 사용자가 @contoso.com 이메일 주소를 가진 경우 contoso.com 도메인에 대한 권한이 필요).
- RD 웹 피드 URL을 만듭니다(https://\<rdweb-dns-name\>.domain/RDWeb/Feed/webfeed.aspx, 예: https://rdweb.contoso.com/RDWeb/Feed/webfeed.aspx).

이제 다음 단계를 사용하여 이메일 검색을 설정합니다.

1. 브라우저에서 도메인이 등록되어 있는 도메인 이름 등록자의 웹 사이트에 연결합니다.
2. DNS 레코드를 보고, 추가하고 편집할 수 있는 등록된 도메인에 대한 적절한 페이지로 이동합니다.
3. 다음 속성을 사용하여 새 DNS 레코드를 입력합니다.
   - **호스트:** _msradc
   - **텍스트:** \<RD 웹 피드 URL\>
   - **TTL:** 300

   DNS 레코드 필드의 이름은 도메인 이름 등록자에 따라 다르지만 이 프로세스를 통해 전체 RD 웹 피드 값이 있는 _msradc.\<domain_name\>(예: _msradc.contoso.com)이라는 TXT 레코드가 생성됩니다.

간단하죠. 이제 디바이스에서 원격 데스크톱 애플리케이션을 시작하고 직접 구독하세요!