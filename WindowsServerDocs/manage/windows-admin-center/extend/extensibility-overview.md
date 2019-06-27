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
ms.openlocfilehash: beb2b3d1eefc5d70e39baa461708938ac9c17be5
ms.sourcegitcommit: 3be280c8638214857dc355b201eb56a04499a5e5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2019
ms.locfileid: "67396701"
---
# <a name="extensions-for-windows-admin-center"></a>Windows Admin Center에 대한 확장

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center는 파트너와 개발자가 Windows Admin Center 내의 기존 기능을 활용하고 원활하게 다른 IT 관리 제품 및 솔루션과 통합되어 고객에게 추가 가치를 제공할 수 있도록 하는 확장 가능한 플랫폼으로 만들어집니다. Windows Admin Center의 각 솔루션 및 도구는 현재 Windows Admin Center에서 사용할 수 있는 것과 마찬가지로 강력한 도구를 빌드할 수 있도록 파트너 및 개발자에게 제공되는 동일한 확장성 기능을 사용하는 확장으로 만들어집니다.

Windows Admin Center 확장은 HTML5, CSS, Angular, TypeScript, jQuery를 비롯한 최신 웹 기술을 사용하여 개발되며 PowerShell 또는 WMI를 통해 대상 서버를 관리할 수 있습니다. Windows Admin Center 게이트웨이 플러그 인을 작성하여 REST와 같은 다른 프로토콜을 통해 대상 서버, 서비스 또는 장치도 관리할 수 있습니다.

## <a name="why-you-should-consider-developing-an-extension-for-windows-admin-center"></a>Windows Admin Center에 대한 확장 개발을 고려해야 하는 이유

다음은 Windows Admin Center에 대한 확장을 개발하여 제품 및 고객에게 가져올 수 있는 가치입니다.

- **Windows Admin Center 도구와 통합:** Windows Admin Center 서버 및 클러스터 관리 도구를 사용 하 여 제품 및 서비스를 통합 하 고 통합 하 고 원활한,--종단 간 모니터링, 관리, 문제 해결 경험 고객에 게 제공 합니다.
- **플랫폼 보안, id 및 관리 기능을 활용 합니다.** Azure Active Directory (AAD) 지원 사용, 다단계 인증, 역할 기반 Access Control (RBAC)를 로깅, 오늘날의 복잡 한 요구 사항에 맞게 Windows Admin Center 플랫폼 기능을 활용 하 여 사용 중인 제품과 서비스에 대 한 감사 IT 조직에서는 있습니다.
- **최신 웹 기술을 사용 하 여 개발 합니다.** HTML5, CSS, Angular, TypeScript, jQuery, 포함 하 여 최신 웹 기술을 사용 하 여 멋진 사용자 환경 및 Windows Admin Center SDK에 포함 하는 다양 하 고 강력한 UI 컨트롤을 빠르게 빌드 하세요.
- **제품 홍보를 확장 합니다.** 올해 하반기 기본 신속 하 게 증가 하는 고객 및 활용 하 여 Windows Server 2019 시작 모멘텀 홍보를 사용 하 여 새 Windows Admin Center 에코 시스템의 일부를 됩니다.

## <a name="start-developing-with-the-windows-admin-center-sdk"></a>Windows Admin Center SDK를 사용 하 여 개발 시작

Windows Admin Center 개발을 시작 하는 것은 쉽습니다.  에 대 한 샘플 코드를 찾을 수 있습니다 [도구](develop-tool.md)를 [솔루션](develop-solution.md), 및 [게이트웨이 플러그 인](develop-gateway-plugin.md) SDK 설명서의 확장 형식입니다. 있는 새 확장 프로젝트를 빌드한 다음 지침에 따라 개별를 요구 사항에 맞게 프로젝트를 사용자 지정 Windows Admin Center CLI를 활용 합니다.

Windows Admin Center 만들었습니다 [SDK 디자인 도구 키트](https://github.com/Microsoft/windows-admin-center-sdk/blob/master/WindowsAdminCenterDesignToolkit.zip) Windows Admin Center 스타일, 컨트롤 및 페이지 템플릿을 사용 하 여 PowerPoint의 확장의 모형을 신속 하 게 하는 데 사용할 수 있습니다. 새로운 확장 다음과 같을 수 있습니다 Windows Admin Center 코딩을 시작 하기 전에 확인 하세요.

GitHub에서 호스트 되는 샘플 코드를 사용할 수도 있습니다. [개발자 도구](https://aka.ms/wacsdk) 탐색 하 고 고유한 확장에서 사용할 수 있는 컨트롤의 다양 한 컬렉션을 포함 하는 샘플 솔루션 확장 됩니다. 개발자 도구는 개발자 모드에서 Windows Admin Center에 사이드로드할 수 있는 완벽하게 기능하는 확장입니다.

SDK와 시작 방법에 대한 자세한 내용은 아래 항목을 참조하십시오.

- [확장의 작동 방식을 이해합니다](understand-extensions.md)
- [확장 개발](developing-extensions.md)
- [가이드](guides.md)
- [확장 게시](publish-extensions.md)

## <a name="partner-spotlight"></a>파트너 추천

고객이 Windows Admin Center 에코시스템에 가져오기 시작한 놀라운 가치를 확인하고 지금 이러한 확장을 사용해 보십시오. Windows Admin Center에서 [확장을 설치하는 방법](../configure/using-extensions.md)에 대해 더 자세히 알아봅니다.

### <a name="biitops"></a>BiitOps
BiitOps 변경 확장에서 변경 내용 추적 하드웨어, 소프트웨어 및 구성 설정에 대 한 Windows Server 실제/가상 컴퓨터를 제공 합니다. 확장 알아보겠습니다 BiitOps 변경 내용을 정확 하 게 새로운 기능, 변경 된 내용 및 새로운 단일-창-의-유리 문제를 추적 하는 데에서 삭제 되었습니다 관련 규정 준수, 안정성 및 보안. [BiitOps 변경 확장에 자세히 알아보려면](case-studies/biitops.md)합니다.

![BiitOps 확장](../media/extensibility-overview/biitops-1.png)

### <a name="dataon"></a>DataON

DataON 해야 확장은 모니터링, 관리 및 DataON의 하이퍼 수렴 형 인프라 및 Windows Server를 기반으로 하는 저장소 시스템의 종단 간 통찰력을 제공 합니다. 반드시 확장은 기록 데이터를 보고, 디스크 매핑, 시스템 경고 및 Windows Admin Center 서버 및 하이퍼 수렴 형 인프라 관리 기능을 통해 원활 하 게 구현 하 여 SAN 같은 호출 홈 서비스와 같은 고유한 값을 추가 합니다. 통합 된 환경입니다. [DataON의 MUST 확장 및 개발 환경에 대해 자세히 알아보세요](case-studies/dataon.md).

![DataON MUST 확장](../media/extensibility-overview/dataon-must-extension.png)

### <a name="fujitsu"></a>Fujitsu

Fujitsu의 ServerView 상태 및 Windows Admin Center 대 한 RAID 상태 확장 Fujitsu PRIMERGY 서버에 대 한 심층 모니터링 및 프로세서, 메모리, 성능 및 저장소 하위 시스템 등 중요 한 하드웨어 구성 요소의 관리를 제공합니다. Windows Admin Center UX 디자인 패턴 및 UI 컨트롤을 이용하여 Fujitsu는 서버 역할 및 서비스, 운영 체제, Windows Admin Center 플랫폼을 통한 하드웨어 관리에 대한 포괄적인 통찰력에 큰 발전을 가져왔습니다. [Fujitsu의 확장 및 개발 환경에 대해 자세히 알아보세요](case-studies/fujitsu.md).

![Fujitsu ServerView 확장](../media/extensibility-overview/fujitsu-serverview-extension.png)

### <a name="lenovo"></a>Lenovo

Windows Admin Center 내에서 다양 한 환경에 원활 하 게 통합 하 여 다음 단계로 하드웨어 관리를 사용 하는 Lenovo XClarity 통합자 확장 합니다. XClarity 통합자 솔루션은 Lenovo 서버 모든 상위 수준 보기를 제공 하 고 단일 서버, 장애 조치 클러스터 또는 하이퍼 수렴 형 클러스터에 연결 되어 있는지 여부를 다른 도구 확장 하드웨어 세부 정보를 제공 합니다. [Lenovo XClarity 통합자 확장에 자세히 알아보려면](case-studies/lenovo.md)합니다.

![Lenovo 확장](../media/extensibility-overview/lenovo-extension.png)

### <a name="pure-storage"></a>Pure Storage

순수 저장소는 엔터프라이즈, 경쟁 우위에 대 한 비즈니스를 가속화 하는 데이터 중심 아키텍처를 제공 하는 모든 플래시 데이터 저장소 솔루션을 제공 합니다. Windows Admin Center 대 한 순수 저장소 확장 순수 FlashArray 제품에 단일 창 보기를 제공 하 고 모니터링 작업을 수행 하 고 실시간 성능 메트릭을 보려면 저장소 볼륨 및 초기자 단일 UI 통해 관리 환경을 제공 합니다. [순수형의 확장 및 개발 경험에 자세히 알아보려면](case-studies/purestorage.md)합니다.

![순수 저장소 확장](../media/extensibility-overview/purestorage-extension.png)

### <a name="qct"></a>QCT

물리적 서버 모니터링과 QCT Azure Stack HCI 인증 시스템에 대 한 관리를 제공 하 여 Windows Admin Center 보완 하는 QCT 관리 제품군을 확장 합니다. QCT Management Suite 확장 서버 하드웨어 정보를 표시 하 고 직관적인 마법사 UI 물리적 교체 하는 데 디스크 하드웨어 이벤트 로그 도구 및 S.M.A.R.T. 효율적으로 제공 합니다. 예측 디스크 관리를 기반합니다. [QCT Management 확장에 자세히 알아보려면](case-studies/qct.md)합니다.

![QCT 확장](../media/extensibility-overview/qct-extension.png)

### <a name="squared-up"></a>Squared Up

Squared Up은 System Center Operations Manager를 기반으로 동급 최고의 모니터링 환경을 제공하고 Azure 로그 분석, Application Insights 및 기타 모니터링 솔루션과 통합합니다. [Squared Up 확장](https://squaredup.com/product/honolulu/windows-admin-center-extension/?utm_source=microsoft-docs&utm_medium=public-relations&utm_campaign=honolulu)은 역사적인 성능 데이터 및 라이브 응용 프로그램 토폴로지와 Windows Admin Center가 제공하는 서버 및 클러스터 관리의 컨텍스트에 대한 종속성을 가져왔으며 초기 고객은 여러 분산된 소스의 거대한 데이터를 단일 환경에 가져오는 가치의 혜택을 얻었습니다. [Squared Up의 확장 및 개발 환경에 대해 자세히 알아보세요](case-studies/squared-up.md).

![Squared Up 확장](../media/extensibility-overview/squaredup-extension.png)