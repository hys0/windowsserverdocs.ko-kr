---
title: 사용자에게 적합한 설치 유형
description: 이 항목에서는 Windows 10 PC에 설치하거나 여러 관리자가 사용할 Windows 서버를 포함하여 Windows Admin Center에 대한 다양한 설치 옵션을 설명합니다.
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 12/02/2019
ms.openlocfilehash: 503cd64cac0673829fe21bc15e8ad9d6a83bbb15
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950512"
---
# <a name="what-type-of-installation-is-right-for-you"></a>나에게 적합한 설치 유형은 무엇인가요?

이 항목에서는 Windows 10 PC에 설치하거나 여러 관리자가 사용할 Windows 서버를 포함하여 Windows Admin Center에 대한 다양한 설치 옵션을 설명합니다. Azure의 VM에 Windows Admin Center를 설치하려면 [Azure에서 Windows Admin Center 배포](../azure/deploy-wac-in-azure.md)를 참조하세요.

## <a name="installation-types"></a>설치: 형식

![img](../media/deployment-options/install-options.PNG)

| 로컬 클라이언트                                | 게이트웨이 서버                                  | 관리되는 서버                               | 장애 조치 클러스터                           |
|---------------------------------------------|-------------------------------------------------|----------------------------------------------|--------------------------------------------|
| 관리되는 서버에 연결된 로컬 Windows 10 클라이언트에 [설치합니다](../deploy/install.md).  빠른 시작, 테스트, 임시 또는 작은 규모의 시나리오에 적합합니다. |지정된 게이트웨이 서버에 [설치](../deploy/install.md)하고 게이트웨이 서버에 대한 연결을 사용하여 모든 클라이언트 브라우저에서 액세스합니다.  대규모 시나리오 | 자체 또는 구성원 노드인 클러스터를 관리하기 위해 관리되는 서버에 직접 [설치합니다](../deploy/install.md).  분산 시나리오에 적합합니다. | 장애 조치(failover) 클러스터에 [배포](#high-availability)하여 게이트웨이 서비스의 고가용성을 가능하게 합니다. 관리 서비스의 복원력을 보장하기 위해 프로덕션 환경에 적합합니다. |

## <a name="installation-supported-operating-systems"></a>설치: 지원되는 운영 체제

다음 Windows 운영 체제에서 Windows Admin Center를 **설치**할 수 있습니다.

| **플랫폼**                       | **설치 모드** |
| -----------------------------------| --------------------- |
| Windows 10                         | 로컬 클라이언트 |
| Windows Server 반기 채널 | 게이트웨이 서버, 관리되는 서버, 장애 조치(failover) 클러스터 |
| Windows Server 2016                | 게이트웨이 서버, 관리되는 서버, 장애 조치(failover) 클러스터 |
| 시작                | 게이트웨이 서버, 관리되는 서버, 장애 조치(failover) 클러스터 |

Windows Admin Center를 운영하려면:

- **로컬 클라이언트 시나리오에서:** 시작 메뉴에서 Windows Admin Center 게이트웨이를 시작하고 `https://localhost:6516`에 액세스하여 클라이언트 웹 브라우저에서 연결합니다.
- **다른 시나리오에서:** 클라이언트 브라우저에서 해당 URL(예제: `https://servername.contoso.com`)을 통해 다른 머신의 Windows Admin Center 게이트웨이에 연결합니다.

> [!WARNING]
> 도메인 컨트롤러에 Windows Admin Center를 설치하는 것은 지원되지 않습니다. [도메인 컨트롤러 보안 모범 사례에 대한 자세한 내용을 참조하세요](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/security-best-practices/securing-domain-controllers-against-attack).

## <a name="installation-supported-web-browsers"></a>설치: 지원되는 웹 브라우저

Microsoft Edge([Microsoft Edge insider](https://microsoftedgeinsider.com) 포함) 및 Google Chrome은 Windows 10에서 테스트되고 지원됩니다. Internet Explorer 및 Firefox를 비롯한 다른 웹 브라우저는 현재 Microsoft의 테스트 매트릭스에 포함되지 않으므로 *공식적으로* 지원되지 않습니다. 이러한 브라우저는 Windows Admin Center를 실행하는 데 문제가 있을 수 있습니다. 예를 들어 Firefox에는 자체 인증서 저장소가 있으므로 Windows 10에서 Windows Admin Center를 사용하려면 Firefox에 `Windows Admin Center Client` 인증서를 가져와야 합니다. 자세한 내용은 [브라우저 관련 알려진 문제](../support/known-issues.md#browser-specific-issues)를 참조하세요.

## <a name="management-target-supported-operating-systems"></a>관리 대상: 지원되는 운영 체제

Windows Admin Center를 사용하여 다음 Windows 운영 체제를 **관리**할 수 있습니다.

| Version | *서버 관리자*를 통해 *노드* 관리 | *클러스터 관리자*를 통해 관리 |
| ------------------------- |--------------- | ----- |
| Windows 10 | 예(컴퓨터 관리를 통해) | 해당 없음 |
| Windows Server 반기 채널 | 예 | 예 |
| 시작 | 예 | 예 |
| Windows Server 2016 | 예 | 예, [최신 누적 업데이트](../use/manage-hyper-converged.md#prepare-your-windows-server-2016-cluster-for-windows-admin-center) 사용 |
| Microsoft Hyper-V Server 2016 | 예 | 예 |
| Windows Server 2012 R2 | 예 | 예 |
| Microsoft Hyper-V Server 2012 R2 | 예 | 예 |
| Windows Server 2012 | 예 | 예 |
| Windows Server 2008 R2 | 예, 기능이 제한적임 | 해당 없음 |

> [!NOTE]
> Windows Admin Center에는 Windows Server 2008 R2, 2012 및 2012 R2에 포함되지 않은 PowerShell 기능이 필요합니다. Windows Admin Center를 사용하여 이를 관리하려면 이들 서버에 Windows Management Framework(WMF) 버전 5.1 이상을 설치해야 합니다.
> 
> WMF가 설치되어 있는지, 그리고 버전이 5.1 이상인지 확인하려면 PowerShell에 `$PSVersiontable`을 입력합니다. 
> 
> WMF를 설치하지 않은 경우 [WMF 5.1을 다운로드](https://www.microsoft.com/download/details.aspx?id=54616)할 수 있습니다.

## <a name="high-availability"></a>고가용성

장애 조치(failover) 클러스터의 활성-수동 모델에 Windows Admin Center를 배포하여 게이트웨이 서비스의 고가용성을 사용할 수 있습니다. 클러스터의 노드 중 하나가 실패하면 Windows Admin Center는 다른 노드로 정상적으로 장애 조치하여 환경에서 서버를 원활하게 관리할 수 있도록 합니다.

[고가용성을 사용하여 Windows Admin Center를 배포하는 방법을 알아봅니다.](../deploy/high-availability.md)

> [!Tip]
> Windows Admin Center를 설치할 준비가 되셨습니까? [지금 다운로드](https://aka.ms/windowsadmincenter)
