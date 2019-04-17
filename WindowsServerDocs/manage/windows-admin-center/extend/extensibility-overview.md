---
title: Windows Admin Center에 대한 확장
description: Windows Admin Center SDK(Project Honolulu)에 대한 확장
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 09/17/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: fa3d7e75b32f0195346e58db54b7932c8d2fd3b9
ms.sourcegitcommit: 659544db1e19d6eecc52c7de07116ae735280544
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/11/2019
ms.locfileid: "9001845"
---
# Windows Admin Center에 대한 확장

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center는 파트너와 개발자가 Windows Admin Center 내의 기존 기능을 활용하고 원활하게 다른 IT 관리 제품 및 솔루션과 통합되어 고객에게 추가 가치를 제공할 수 있도록 하는 확장 가능한 플랫폼으로 만들어집니다. Windows Admin Center의 각 솔루션 및 도구는 현재 Windows Admin Center에서 사용할 수 있는 것과 마찬가지로 강력한 도구를 빌드할 수 있도록 파트너 및 개발자에게 제공되는 동일한 확장성 기능을 사용하는 확장으로 만들어집니다.

Windows Admin Center 확장은 HTML5, CSS, Angular, TypeScript, jQuery를 비롯한 최신 웹 기술을 사용하여 개발되며 PowerShell 또는 WMI를 통해 대상 서버를 관리할 수 있습니다. Windows Admin Center 게이트웨이 플러그 인을 작성하여 REST와 같은 다른 프로토콜을 통해 대상 서버, 서비스 또는 장치도 관리할 수 있습니다.

## Windows Admin Center에 대한 확장 개발을 고려해야 하는 이유

다음은 Windows Admin Center에 대한 확장을 개발하여 제품 및 고객에게 가져올 수 있는 가치입니다.

- **Windows Admin Center 도구와 통합:** 제품 및 서비스를 Windows Admin Center의 서버 및 클러스터 관리 도구와 통합하고 고객에게 원활하게 통합된 포괄적인 모니터링, 관리, 및 문제 해결 경험을 제공합니다.
- **플랫폼 보안, ID 및 관리 기능 활용:** 오늘날 IT 조직의 복잡한 요구를 충족하기 위해 Windows Admin Center 플랫폼 기능을 활용하여 제품 및 서비스에 대한 Azure Active Directory(AAD) 지원, 다단계 인증, 역할 기반 액세스 제어(RBAC), 로깅, 감사를 구현합니다.
- **최신 웹 기술을 사용하여 개발:** HTML5, CSS, Angular, TypeScript, jQuery를 비롯한 최신 웹 기술을 사용하여 놀라운 사용자 환경과 Windows Admin Center SDK에 포함된 강력하고 풍부한 UI 컨트롤을 신속하게 빌드합니다.
- **제품 지원 확장:** 새 Windows Admin Center 에코시스템에 가입하여 빠르게 고객 기반을 늘리고 올해 추후 출시될 Windows Server 2019 출시 모멘텀을 활용하세요.

## Windows Admin Center SDK를 사용 하 여 개발 시작

Windows Admin Center 개발을 시작 하기 쉽습니다.  SDK 설명서에서 [도구](develop-tool.md), [솔루션](develop-solution.md)및 [게이트웨이 플러그 인](develop-gateway-plugin.md) 확장 형식에 대 한 샘플 코드를 찾을 수 있습니다. 여기 새 확장 프로젝트를 빌드한 다음 요구 사항을 충족 하도록 프로젝트를 사용자 지정 하려면 개별 지침에 따라 Windows Admin Center CLI를 활용 하 게 있습니다.

Windows Admin Center 스타일, 컨트롤 및 페이지 템플릿을 사용 하 여 powerpoint에서 확장 [SDK 디자인 도구 키트](https://github.com/Microsoft/windows-admin-center-sdk/blob/master/WindowsAdminCenterDesignToolkit.zip) 를 신속 하 게 쉽게 사용할 수 있는 머킹 Windows Admin Center 개선. 확장 수 모양을 확인 Windows 관리 센터에서 코딩을 시작 하기 전에!

GitHub에서 호스트 되는 샘플 코드는: [개발자 도구](https://aka.ms/wacsdk) 는 찾아 자체 확장에서 사용할 수 있는 컨트롤의 풍부한 컬렉션을 포함 하는 샘플 솔루션 확장 합니다. 개발자 도구는 개발자 모드에서 Windows Admin Center에 사이드로드할 수 있는 완벽하게 기능하는 확장입니다.

SDK와 시작 방법에 대한 자세한 내용은 아래 항목을 참조하십시오.

- [확장 작동 방법 이해](understand-extensions.md)
- [확장 개발](developing-extensions.md)
- [가이드](guides.md)
- [확장 게시](publish-extensions.md)

## 파트너 추천

고객이 Windows Admin Center 에코시스템에 가져오기 시작한 놀라운 가치를 확인하고 지금 이러한 확장을 사용해 보십시오. Windows Admin Center에서 [확장을 설치하는 방법](../configure/using-extensions.md)에 대해 더 자세히 알아봅니다.

### DataON

DataON의 MUST 확장 모니터링, 관리 및 종단 간 DataON의 하이퍼 컨 버 지 드 인프라 및 저장소 시스템 Windows 서버를 기반으로 통찰을 제공 합니다. 기록 데이터 보고, 디스크 매핑, 시스템 알림 및 Windows Admin Center 서버 및 하이퍼 컨 버 지 드 인프라 관리 기능을 통해 원활 하 게 보완 SAN 같은 통화 홈 서비스와 같은 고유한 값을 추가 하는 MUST 확장 통합 된 환경입니다. [DataON의 MUST 확장 및 개발 환경에 대해 자세히 알아보세요](case-studies/dataon.md).

![DataON MUST 확장](../media/extensibility-overview/dataon-must-extension.png)

### Fujitsu

Windows Admin Center에 대한 Fujitsu의 ServerView 상태 및 RAID 상태 확장는 Fujitsu PRIMERGY 서버에 대한 프로세서, 메모리, 전원 및 저장소 하위 시스템 등의 중요한 하드웨어 구성 요소에 대한 상세 모니터링 및 관리를 제공합니다. Windows Admin Center UX 디자인 패턴 및 UI 컨트롤을 이용하여 Fujitsu는 서버 역할 및 서비스, 운영 체제, Windows Admin Center 플랫폼을 통한 하드웨어 관리에 대한 포괄적인 통찰력에 큰 발전을 가져왔습니다. [Fujitsu의 확장 및 개발 환경에 대해 자세히 알아보세요](case-studies/fujitsu.md).

![Fujitsu ServerView 확장](../media/extensibility-overview/fujitsu-serverview-extension.png)

### Lenovo

Lenovo의 XClarity 통합자 확장 Windows Admin Center 내에서 다양 한 환경에 원활 하 게 통합 하 여 다음 단계로 하드웨어 관리를 사용 합니다. XClarity 통합자 솔루션은 모든 Lenovo 서버에 대 한 상위 수준 보기를 제공 하 고 단일 서버, 장애 조치 클러스터 또는 하이퍼 수렴 형 클러스터에 연결 되어 있는지 여부를 다른 도구 확장 하드웨어 세부 정보를 제공 합니다. [Lenovo XClarity 통합자 확장에 자세히 알아봅니다](case-studies/lenovo.md).

![Lenovo 확장](../media/extensibility-overview/lenovo-extension.png)

### 순수 저장소

순수 저장소 엔터프라이즈, 데이터 중심 아키텍처 경쟁 우위에 대 한 비즈니스 가속화를 제공 하는 모든 플래시 데이터 저장소 솔루션을 제공 합니다. Windows Admin Center에 대 한 순수 저장소 확장 순수 FlashArray 제품에는 단일 창 보기를 제공 하 고 사용자의 모니터링 작업을 수행, 실시간 성능 메트릭 보기 및 저장소 볼륨 및 초기자 단일 UI 통해 관리 환경입니다. [Pure의 확장 및 개발 환경에 자세히 알아봅니다](case-studies/purestorage.md).

![순수 저장소 확장](../media/extensibility-overview/purestorage-extension.png)

### Squared Up

Squared Up은 System Center Operations Manager를 기반으로 동급 최고의 모니터링 환경을 제공하고 Azure 로그 분석, Application Insights 및 기타 모니터링 솔루션과 통합합니다. [Squared Up 확장](https://squaredup.com/product/honolulu/windows-admin-center-extension/?utm_source=microsoft-docs&utm_medium=public-relations&utm_campaign=honolulu)은 역사적인 성능 데이터 및 라이브 응용 프로그램 토폴로지와 Windows Admin Center가 제공하는 서버 및 클러스터 관리의 컨텍스트에 대한 종속성을 가져왔으며 초기 고객은 여러 분산된 소스의 거대한 데이터를 단일 환경에 가져오는 가치의 혜택을 얻었습니다. [Squared Up의 확장 및 개발 환경에 대해 자세히 알아보세요](case-studies/squared-up.md).

![Squared Up 확장](../media/extensibility-overview/squaredup-extension.png)