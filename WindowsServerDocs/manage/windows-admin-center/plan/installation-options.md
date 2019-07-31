---
title: 사용자에 게 적합 한 설치 유형
description: 이 항목에서는 windows 10 PC에 설치 하거나 여러 관리자가 사용할 Windows server를 포함 하 여 Windows 관리 센터에 대 한 다양 한 설치 옵션을 설명 합니다.
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 06/07/2019
ms.openlocfilehash: 36c9dfcb38ef417df56206cdb18633cc877183c4
ms.sourcegitcommit: af80963a1d16c0b836da31efd9c5caaaf6708133
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68658896"
---
# <a name="what-type-of-installation-is-right-for-you"></a>나에게 적합한 유형의 설치는 무엇입니까?

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

이 항목에서는 windows 10 PC에 설치 하거나 여러 관리자가 사용할 Windows server를 포함 하 여 Windows 관리 센터에 대 한 다양 한 설치 옵션을 설명 합니다. Azure의 VM에 Windows 관리 센터를 설치 하려면 [azure에서 Windows 관리 센터 배포](../azure/deploy-wac-in-azure.md)를 참조 하세요.

## <a name="installation-types"></a>설치: 유형

| 로컬 클라이언트                                | 게이트웨이 서버                                  | 관리 서버                               | 장애 조치 클러스터                           |
|---------------------------------------------|-------------------------------------------------|----------------------------------------------|--------------------------------------------|
| ![g](../media/deployment-options/W10.PNG) | ![g](../media/deployment-options/gateway.PNG) | ![g](../media/deployment-options/node.PNG) | ![g](../media/deployment-options/HA.png) |
| 관리 되는 서버에 연결 된 로컬 Windows 10 클라이언트에를 설치 합니다.  빠른 시작, 테스트, 임시 또는 작은 규모의 시나리오에 적합 합니다. |지정 된 게이트웨이 서버에를 설치 하 고 게이트웨이 서버에 대 한 연결을 사용 하 여 모든 클라이언트 브라우저에서 액세스 합니다.  대규모 시나리오에 적합 합니다. | 자체 또는 구성원 노드인 클러스터를 관리 하기 위해 관리 되는 서버에 직접를 설치 합니다.  분산 시나리오에 적합 합니다. | 장애 조치 (failover) 클러스터에를 배포 하 여 게이트웨이 서비스의 고가용성을 가능 하 게 합니다. 관리 서비스의 복원 력을 보장 하기 위해 프로덕션 환경에 적합 합니다. |

## <a name="installation-supported-operating-systems"></a>설치: 지원되는 운영 체제

Windows 관리 센터는 다음 Windows 운영 체제에 **설치할** 수 있습니다.

| **플랫폼**                       | **설치 모드** |
| -----------------------------------| --------------------- |
| Windows 10, 버전 1709 이상  | 로컬 클라이언트 |
| Windows Server 반기 채널 | 게이트웨이 서버, 관리 서버, 장애 조치 (failover) 클러스터 |
| Windows Server 2016                | 게이트웨이 서버, 관리 서버, 장애 조치 (failover) 클러스터 |
| Windows Server 2019                | 게이트웨이 서버, 관리 서버, 장애 조치 (failover) 클러스터 |

Windows 관리 센터를 운영 하려면:

- **로컬 클라이언트 시나리오에서:** 시작 메뉴에서 Windows 관리 센터 게이트웨이를 시작 하 고에 액세스 `https://localhost:6516`하 여 클라이언트 웹 브라우저에서 연결 합니다.
- **다른 시나리오에서는 다음을 수행 합니다.** 클라이언트 브라우저에서 URL을 통해 다른 컴퓨터의 Windows 관리 센터 게이트웨이에 연결 합니다 (예:).`https://servername.contoso.com`

> [!WARNING]
> 도메인 컨트롤러에 Windows 관리 센터를 설치 하는 것은 지원 되지 않습니다. [도메인 컨트롤러 보안 모범 사례에 대해 자세히](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/security-best-practices/securing-domain-controllers-against-attack)알아보세요. 

## <a name="installation-supported-web-browsers"></a>설치: 지원 되는 웹 브라우저

Microsoft Edge 및 Google Chrome은 Windows 10에서 테스트 되 고 지원 됩니다. Internet Explorer 및 Firefox를 비롯 한 다른 웹 브라우저는 현재 테스트 매트릭스의 일부가 아니므로 *공식적* 으로 지원 되지 않습니다. 이러한 브라우저는 Windows 관리 센터를 실행 하는 데 문제가 있을 수 있습니다. 예를 들어 firefox에는 자체 인증서 저장소가 있으므로 windows 10에서 windows 관리 센터 `Windows Admin Center Client` 를 사용 하려면 firefox로 인증서를 가져와야 합니다. 자세한 내용은 [브라우저 관련 알려진 문제](../support/known-issues.md#browser-specific-issues)를 참조 하세요.

## <a name="management-target-supported-operating-systems"></a>관리 대상: 지원되는 운영 체제

Windows 관리 센터를 사용 하 여 다음 Windows 운영 체제를 **관리할** 수 있습니다.

| 버전 | *서버 관리자* 를 통해 *노드* 관리 | *장애 조치(Failover) 클러스터 관리자* 를 통해 *클러스터* 관리 | *HCI 클러스터 관리자* 를 통해 *HCI* 관리 |
| ------------------------- |--------------- | ----- | ------------------------ |
| Windows 10, 버전 1709 이상 | 예 (컴퓨터 관리를 통해) | 해당 사항 없음 | 해당 사항 없음 |
| Windows Server 반기 채널 | 예 | 예 | 해당 사항 없음 |
| Windows Server 2019 | 예 | 예 | 예 |
| Windows Server 2016 | 예 | 예 | 예, [최신 누적 업데이트](../use/manage-hyper-converged.md#prepare-your-windows-server-2016-cluster-for-windows-admin-center) 포함 |
| Microsoft Hyper-V Server 2016 | 예 | 예 | 해당 사항 없음 |
| Windows Server 2012 R2 | 예 | 예 | 해당 사항 없음 |
| Microsoft Hyper-V Server 2012 R2 | 예 | 예 | 해당 사항 없음 |
| Windows Server 2012 | 예 | 예 | 해당 사항 없음 |
| Windows Server 2008 R2 | 예, 제한 된 기능 | 해당 사항 없음 | 해당 사항 없음 |

> [!NOTE]
> Windows 관리 센터에는 Windows Server 2008 R2, 2012 및 2012 r 2에 포함 되지 않은 PowerShell 기능이 필요 합니다. Windows 관리 센터를 사용 하 여이를 관리 하려면 해당 서버에 WMF (Windows Management Framework) 버전 5.1 이상을 설치 해야 합니다.
> 
> WMF가 설치되어 있는지, 그리고 버전이 5.1 이상인지 확인하려면 PowerShell에 `$PSVersiontable`을 입력합니다. 
> 
> WMF를 설치 하지 않은 경우 [wmf 5.1를 다운로드할](https://www.microsoft.com/en-us/download/details.aspx?id=54616)수 있습니다.

## <a name="high-availability"></a>고가용성

장애 조치 (failover) 클러스터의 활성-수동 모델에 Windows 관리 센터를 배포 하 여 게이트웨이 서비스의 고가용성을 사용할 수 있습니다. 클러스터의 노드 중 하나가 실패 하면 Windows 관리 센터는 다른 노드로 정상적으로 장애 조치 하 여 환경에서 서버를 원활 하 게 관리할 수 있도록 합니다.

[고가용성을 사용 하 여 Windows 관리 센터를 배포 하는 방법을 알아봅니다.](../deploy/high-availability.md)

> [!Tip]
> Windows Admin Center를 설치할 준비가 되셨습니까? [지금 다운로드](https://aka.ms/windowsadmincenter)
