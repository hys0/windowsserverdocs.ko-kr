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
ms.openlocfilehash: c318f3dba1d1264c91a7134aafecdd177882f5f8
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70869731"
---
# <a name="extensions-for-windows-admin-center"></a>Windows Admin Center에 대한 확장

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center는 파트너와 개발자가 Windows Admin Center 내의 기존 기능을 활용하고 원활하게 다른 IT 관리 제품 및 솔루션과 통합되어 고객에게 추가 가치를 제공할 수 있도록 하는 확장 가능한 플랫폼으로 만들어집니다. Windows Admin Center의 각 솔루션 및 도구는 현재 Windows Admin Center에서 사용할 수 있는 것과 마찬가지로 강력한 도구를 빌드할 수 있도록 파트너 및 개발자에게 제공되는 동일한 확장성 기능을 사용하는 확장으로 만들어집니다.

Windows Admin Center 확장은 HTML5, CSS, Angular, TypeScript, jQuery를 비롯한 최신 웹 기술을 사용하여 개발되며 PowerShell 또는 WMI를 통해 대상 서버를 관리할 수 있습니다. Windows Admin Center 게이트웨이 플러그 인을 작성하여 REST와 같은 다른 프로토콜을 통해 대상 서버, 서비스 또는 장치도 관리할 수 있습니다.

## <a name="why-you-should-consider-developing-an-extension-for-windows-admin-center"></a>Windows Admin Center에 대한 확장 개발을 고려해야 하는 이유

Windows 관리 센터에 대 한 확장을 개발 하 여 제품 및 고객에 게 제공할 수 있는 값은 다음과 같습니다.

- **Windows 관리 센터 도구와 통합:** 제품 및 서비스를 Windows 관리 센터의 서버 및 클러스터 관리 도구와 통합 하 고 고객에 게 통일 하 고 원활한 종단 간 모니터링, 관리, 문제 해결 환경을 제공할 수 있습니다.
- **플랫폼 보안, id 및 관리 기능 활용:** 오늘날의 복잡 한 요구 사항을 충족 하기 위해 Windows 관리 센터 플랫폼 기능을 활용 하 여 사용자의 제품 및 서비스에 대 한 AAD (Azure Active Directory) 지원, Multi-Factor Authentication, RBAC (역할 기반 Access Control), 로깅, 감사를 사용 하도록 설정 합니다. IT 조직.
- **최신 웹 기술을 사용 하 여 개발:** HTML5, CSS, 각도, TypeScript 및 jQuery를 비롯 한 최신 웹 기술 및 Windows 관리 센터 SDK에 포함 된 풍부한 강력한 UI 컨트롤을 사용 하 여 뛰어난 사용자 환경을 빠르게 구축 합니다.
- **제품 전파를 확장 합니다.** 신속 하 게 성장 하는 고객 기반에 지속적으로 전파 되는 새로운 Windows 관리 센터 에코 시스템의 일부가 되어 올해 후반에 Windows Server 2019 출시 모멘텀을 활용 하세요.

## <a name="start-developing-with-the-windows-admin-center-sdk"></a>Windows 관리 센터 SDK를 사용 하 여 개발 시작

Windows 관리 센터 개발을 쉽게 시작할 수 있습니다.  SDK 설명서에서 [도구](develop-tool.md), [솔루션](develop-solution.md)및 [게이트웨이 플러그 인](develop-gateway-plugin.md) 확장 형식에 대 한 샘플 코드를 찾을 수 있습니다. 여기에서 Windows 관리 센터 CLI를 활용 하 여 새 확장 프로젝트를 빌드한 다음, 개별 가이드에 따라 사용자의 요구에 맞게 프로젝트를 사용자 지정 합니다.

Windows 관리 센터 스타일, 컨트롤 및 페이지 템플릿을 사용 하 여 PowerPoint에서 확장을 신속 하 게 만들 수 있도록 Windows 관리 센터 [SDK 디자인 도구 키트](https://github.com/Microsoft/windows-admin-center-sdk/blob/master/WindowsAdminCenterDesignToolkit.zip) 를 만들었습니다. 코딩을 시작 하기 전에 Windows 관리 센터에서 확장의 모양을 확인 하세요.

GitHub에서 호스트 되는 샘플 코드도 있습니다. [개발자 도구](https://aka.ms/wacsdk) 는 사용자 고유의 확장에서 찾아보고 사용할 수 있는 풍부한 컨트롤 컬렉션이 포함 된 샘플 솔루션 확장입니다. 개발자 도구는 개발자 모드에서 Windows Admin Center에 사이드로드할 수 있는 완벽하게 기능하는 확장입니다.

SDK와 시작 방법에 대한 자세한 내용은 아래 항목을 참조하십시오.

- [확장 작동 방법 이해](understand-extensions.md)
- [확장 개발](developing-extensions.md)
- [가이드](guides.md)
- [확장 게시](publish-extensions.md)

## <a name="partner-spotlight"></a>파트너 추천

고객이 Windows Admin Center 에코시스템에 가져오기 시작한 놀라운 가치를 확인하고 지금 이러한 확장을 사용해 보십시오. Windows Admin Center에서 [확장을 설치하는 방법](../configure/using-extensions.md)에 대해 더 자세히 알아봅니다.

### <a name="biitops"></a>BiitOps
BiitOps 변경 확장은 Windows Server 물리적/가상 컴퓨터의 하드웨어, 소프트웨어 및 구성 설정에 대 한 변경 내용 추적 기능을 제공 합니다. BiitOps 변경 확장은 새로운 기능, 변경 된 내용 및 단일 창에서 삭제 된 항목을 정확 하 게 보여 줍니다 .이를 통해 규정 준수, 안정성 및 보안과 관련 된 문제를 추적할 수 있습니다. [BiitOps 변경 확장에 대해 자세히 알아보세요](case-studies/biitops.md).

![BiitOps 확장](../media/extensibility-overview/biitops-1.png)

### <a name="dataon"></a>DataON

DataON은 확장을 통해 모니터링, 관리 및 종단 간 정보를 Windows Server를 기반으로 하는 하이퍼 수렴 형 인프라 및 저장소 시스템의 데이터에 대 한 모니터링, 관리 및 종단 간 통찰력을 제공 합니다. 확장 해야 하는 경우에는 기록 데이터 보고, 디스크 매핑, 시스템 경고 및 SAN과 같은 SAN 호출 홈 서비스와 같은 고유한 값을 추가 하 고, Windows 관리 센터 서버와 하이퍼 수렴 형 인프라 관리 기능을 보완 하 고, 원활 하 게 통합 환경. [DataON의 MUST 확장 및 개발 환경에 대해 자세히 알아보세요](case-studies/dataon.md).

![DataON MUST 확장](../media/extensibility-overview/dataon-must-extension.png)

### <a name="fujitsu"></a>Fujitsu

Windows 관리 센터에 대 한 Fujitsu의 ServerView 상태 및 RAID 상태 확장은 Fujitsu PRIMERGY 서버용 프로세서, 메모리, 전원 및 저장소 하위 시스템 같은 중요 한 하드웨어 구성 요소에 대 한 심층 모니터링 및 관리를 제공 합니다. Windows Admin Center UX 디자인 패턴 및 UI 컨트롤을 이용하여 Fujitsu는 서버 역할 및 서비스, 운영 체제, Windows Admin Center 플랫폼을 통한 하드웨어 관리에 대한 포괄적인 통찰력에 큰 발전을 가져왔습니다. [Fujitsu의 확장 및 개발 환경에 대해 자세히 알아보세요](case-studies/fujitsu.md).

![Fujitsu ServerView 확장](../media/extensibility-overview/fujitsu-serverview-extension.png)

### <a name="lenovo"></a>Lenovo

Lenovo XClarity 통합자 확장은 Windows 관리 센터 내에서 다양 한 환경에 원활 하 게 통합 하 여 하드웨어 관리를 다음 수준으로 사용 합니다. XClarity 통합자 솔루션은 모든 Lenovo 서버에 대 한 개략적인 정보를 제공 하 고, 다른 도구 확장은 단일 서버, 장애 조치 (failover) 클러스터 또는 하이퍼 수렴 형 클러스터에 연결 되어 있는지 여부에 상관 없이 하드웨어 세부 정보를 제공 합니다. [Lenovo XClarity 통합자 확장에 대해 자세히 알아보세요](case-studies/lenovo.md).

![Lenovo 확장](../media/extensibility-overview/lenovo-extension.png)

### <a name="pure-storage"></a>Pure Storage

순수 저장소는 데이터 중심 아키텍처를 제공 하 여 경쟁 우위의 비즈니스를 가속화 하는 엔터프라이즈급 데이터 저장소 솔루션을 제공 합니다. Windows 관리 센터의 순수 저장소 확장은 순수 FlashArray 제품에 대 한 단일 창 보기를 제공 하 고 사용자에 게 모니터링 작업을 수행 하 고, 실시간 성능 메트릭을 확인 하 고, 단일 UI를 통해 저장소 볼륨과 초기자를 관리할 수 있는 기능을 제공 합니다. 지. [순수한 확장 및 개발 환경에 대해 자세히 알아보세요](case-studies/purestorage.md).

![순수 저장소 확장](../media/extensibility-overview/purestorage-extension.png)

### <a name="qct"></a>QCT

QCT Management Suite 확장은 QCT Azure Stack HCI 인증 시스템에 대 한 물리적 서버 모니터링과 관리를 제공 하 여 Windows 관리 센터를 보완 합니다. QCT 관리 도구 모음 확장은 서버 하드웨어 정보를 표시 하 고 실제 디스크를 효율적으로 대체 하는 데 유용한 직관적인 마법사 UI를 제공 합니다 (하드웨어 이벤트 로그 도구 및 S.M.A.R.T.). 기반 예측 디스크 관리. [QCT 관리 도구 모음 확장에 대해 자세히 알아보세요](case-studies/qct.md).

![QCT 확장](../media/extensibility-overview/qct-extension.png)

### <a name="squared-up"></a>Squared Up

Squared Up은 System Center Operations Manager를 기반으로 동급 최고의 모니터링 환경을 제공하고 Azure 로그 분석, Application Insights 및 기타 모니터링 솔루션과 통합합니다. [Squared Up 확장](https://squaredup.com/product/honolulu/windows-admin-center-extension/?utm_source=microsoft-docs&utm_medium=public-relations&utm_campaign=honolulu)은 역사적인 성능 데이터 및 라이브 응용 프로그램 토폴로지와 Windows Admin Center가 제공하는 서버 및 클러스터 관리의 컨텍스트에 대한 종속성을 가져왔으며 초기 고객은 여러 분산된 소스의 거대한 데이터를 단일 환경에 가져오는 가치의 혜택을 얻었습니다. [Squared Up의 확장 및 개발 환경에 대해 자세히 알아보세요](case-studies/squared-up.md).

![Squared Up 확장](../media/extensibility-overview/squaredup-extension.png)