---
title: 웹 서버 성능 튜닝
description: Windows Server 16의 웹 서버에 대한 성능 튜닝 권장 사항
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: landing-page
ms.author: davso; ericam; yashi
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: ec36d87957e5bbe897597e330e766c3193cd30d0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851696"
---
# <a name="performance-tuning-web-servers"></a>웹 서버 성능 튜닝


이 토픽에서는 Windows Server 2016 웹 서버의 성능 튜닝 방법 및 권장 사항을 설명합니다.


## <a name="selecting-the-proper-hardware-for-performance"></a>성능에 맞는 적절한 하드웨어 선택


평균 부하, 최대 부하, 용량, 확장 계획 및 응답 시간을 고려하여 예상 웹 부하를 충족하는 적절한 하드웨어를 선택하는 것이 중요합니다. 하드웨어 병목 현상은 소프트웨어 튜닝의 효과를 제한합니다.

[서버 하드웨어의 성능 튜닝](../../hardware/index.md)에는 다음과 같은 성능 제약 조건을 피할 수 있는 하드웨어 권장 사항이 설명되어 있습니다.

-   CPU 속도가 느리면 ASP, ASP.NET 및 TLS 시나리오처럼 CPU 사용량이 많은 워크로드의 처리 능력이 제한됩니다.

-   작은 L2 또는 L3/LLC 프로세서 캐시는 성능에 악영향을 줄 수 있습니다.

-   메모리 양이 제한되면 호스팅할 수 있는 사이트 수, 저장할 수 있는 동적 콘텐츠 스크립트(예: ASP.NET) 수, 애플리케이션 풀 또는 작업자 프로세스 수에도 영향이 있습니다.

-   비효율적인 네트워크 어댑터 때문에 네트워킹 병목 상태가 발생합니다.

-   비효율적인 디스크 하위 시스템 또는 스토리지 어댑터 때문에 파일 시스템에 병목 상태가 발생합니다.

## <a name="operating-system-best-practices"></a>운영 체제 모범 사례


될 수 있으면 운영 체제를 새로 설치합니다. 소프트웨어를 업그레이드하면 오래된, 원치 않는 또는 최적이 아닌 레지스트리 설정과 이전에 설치한 자동으로 시작되는 서비스 및 애플리케이션이 남아 있으면서 리소스를 소비할 수 있습니다. 또 다른 운영 체제가 설치되어 있고 해당 운영 체제를 유지해야 하는 경우 다른 파티션에 새 운영 체제를 설치해야 합니다. 그렇지 않으면 새로 설치되는 운영 체제가 %Program Files%\\Common Files 아래의 설정을 덮어씁니다.

될 수 있으면 디스크 액세스 간섭을 줄이기 위해 시스템 페이지 파일, 운영 체제, 웹 데이터, ASP 템플릿 캐시 및 IIS(인터넷 정보 서비스) 로그를 별도의 물리적 디스크에 배치합니다.

될 수 있으면 시스템 리소스 경합을 줄이기 위해 Microsoft SQL Server와 IIS를 서로 다른 서버에 설치합니다.

필수 서비스와 애플리케이션 외에는 설치하지 마세요. 경우에 따라 시스템에서 필요 없는 서비스를 비활성화할 수도 있습니다.

## <a name="ntfs-file-system-settings"></a>NTFS 파일 시스템 설정

시스템 글로벌 스위치 **NtfsDisableLastAccessUpdate**(REG\_DWORD) 1은 **HKLM\\System\\CurrentControlSet\\Control\\FileSystem** 아래에 있으며 기본적으로 1로 설정됩니다. 이 스위치는 최신 파일 또는 디렉터리 액세스에 대한 날짜 및 시간 스탬프 업데이트를 해제하여 디스크 I/O 부하 및 대기 시간을 줄입니다. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008 버전을 새로 설치하면 이 설정이 기본적으로 사용되며, 이 설정을 조정할 필요가 없습니다. Windows 초기 버전은 이 키를 설정하지 않습니다. 서버에서 Windows 초기 버전을 실행 중이거나 Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008로 업그레이드한 경우 이 설정을 활성화해야 합니다.

디렉터리 수천 개가 포함된 대형 데이터 세트(또는 여러 호스트)를 사용하는 경우 업데이트를 해제하는 것이 효과적입니다. 웹 관리 용도로만 이 정보를 유지하는 경우 IIS 로깅을 사용하는 것이 좋습니다.

>[!Warning]
> 증분 백업 유틸리티 같은 일부 애플리케이션은 이 업데이트 정보에 의존하며, 이 정보가 없으면 올바르게 작동하지 않습니다.

## <a name="see-also"></a>참고 항목
- [IIS 10.0 성능 튜닝](tuning-iis-10.md)
- [HTTP 1.1/2 튜닝](http-performance.md)


