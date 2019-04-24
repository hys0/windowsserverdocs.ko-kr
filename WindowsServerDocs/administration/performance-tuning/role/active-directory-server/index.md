---
title: Active Directory 서버 성능 조정
description: Active Directory 서버 성능 조정
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: landing-page
ms.author: TimWi; ChrisRob; HerbertM; KenBrumf;  MLeary; ShawnRab
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 04c9683c3d14291d5dc2682c6836657313865866
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59891944"
---
# <a name="performance-tuning-active-directory-servers"></a>Active Directory 서버 성능 조정

Active Directory 성능 조정은 두 가지 목표에 초점을 맞추었습니다.
- 가능한 한 가장 효율적인 방식으로 부하를 서비스하도록 최적으로 구성된 Active Directory
- Active Directory에 워크로드를 제출하는 것은 최대한 효율적으로 처리해야 합니다.

이를 위해 세 가지 별도 영역에 적절한 주의가 필요합니다.
- 적절한 용량 계획 – 기존 부하를 지원할 수 있도록 충분한 하드웨어를 배치했는지 확인합니다.
- 서버 쪽 조정 – 가능한 한 효율적으로 부하를 처리하도록 도메인 컨트롤러를 구성합니다.
- Active Directory 클라이언트/애플리케이션 조정 – 클라이언트 및 애플리케이션에서 최적화된 방식으로 Active Directory를 사용하는지 확인합니다.

## <a name="start-with-capacity-planning"></a>용량 계획으로 시작
정확한 시간에 클라이언트 요청을 처리하려면 올바른 도메인과 올바른 로캘에 충분한 수의 도메인 컨트롤러를 적절히 배포해야 하고 중복 배치도 중요합니다. 이 부분은 심도 있는 주제이며 가이드의 범위를 벗어납니다. 읽는 사람. 읽는 사람은 [Active Directory 도메인 서비스에 대한 용량 계획](https://go.microsoft.com/fwlink/?LinkId=324566)에 있는 권장 사항 및 지침을 읽고 이해한 후 Active Directory 성능 조정을 시작하는 것이 좋습니다.

>[!Important]
> 적절한 구성 및 Active Directory 크기 조정은 전체 시스템 및 워크로드 성능에 커다란 영향을 줄 수 있습니다. 읽는 사람은 [Active Directory 도메인 서비스에 대한 용량 계획](https://go.microsoft.com/fwlink/?LinkId=324566)을 읽은 후 작업을 시작하는 것이 좋습니다.

## <a name="updates-and-evolving-recommendations"></a>업데이트 및 권장 사항 개선

Active Directory와 클라이언트 성능 최적화는 지난 몇 세대의 운영 체제에 걸쳐 엄청나게 향상되었으며 이러한 노력은 지금도 계속되고 있습니다. 다음을 포함한 이점을 활용하려면 가장 최신 버전의 플랫폼을 배포하는 것이 좋습니다.

- 향상된 안정성
- 성능 향상
- 더 나은 로깅 및 문제 해결 도구

그러나 여기에는 시간이 많이 걸리고 최신 플랫폼을 100% 채택할 수 없는 많은 환경에서 시나리오가 실행되고 있다는 사실을 알고 있습니다. 이전 버전의 플랫폼에 몇 가지 개선 사항이 추가되었으며 계속 추가될 예정입니다.

팀 블로그 ["디렉터리 서비스 팀에게 요청"](https://blogs.technet.microsoft.com/askds)을 팔로잉하여 ADDS 관리를 위한 최신 뉴스, 지침 및 모범 사례에 대한 정보를 얻으세요.

## <a name="see-also"></a>참고 항목
- [하드웨어 고려 사항](hardware-considerations.md)
- [LDAP 고려 사항](ldap-considerations.md)
- [적절한 도메인 컨트롤러 배치 및 사이트 고려 사항](site-definition-considerations.md)
- [ADDS 성능 문제 해결](troubleshoot.md) 
- [Active Directory 도메인 서비스의 용량 계획](https://go.microsoft.com/fwlink/?LinkId=324566)
