---
title: 설치 유형을 적합 한
description: 어떤 유형의 설치는 Windows Admin Center (프로젝트 브라 티) 사용자에 게 적합 합니다. 높은 가용성과 복원 력을 위해 장애 조치 클러스터에 설치 합니다.
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: fae0305e454cdd10109219c6182ff612f539e9c9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868014"
---
# <a name="what-type-of-installation-is-right-for-you"></a>나에게 적합한 유형의 설치는 무엇입니까?

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

## <a name="supported-operating-systems-installation"></a>지원 되는 운영 체제: 설치

할 수 있습니다 **설치** 다음 Windows 운영 체제에서 Windows Admin Center:

| **버전(Version)** | **설치 모드** |
|-------------|-----------------------|
|Windows 10 버전 1709 이상 | 데스크톱 모드 |
|Windows Server 반기 채널 | 게이트웨이 모드 |
|Windows Server 2016 | 게이트웨이 모드 |
|Windows Server 2019 | 게이트웨이 모드 |

**데스크톱 모드:** 시작 메뉴에서 시작 하 고 설치 하는 동일한 컴퓨터에서 Windows Admin Center 게이트웨이에 연결 (즉, `https://localhost:6516`)

**게이트웨이 모드:** 다른 컴퓨터에서 클라이언트 브라우저에서 Windows Admin Center 게이트웨이에 연결 (즉, `https://servername.contoso.com`) 

> [!WARNING]
> 도메인 컨트롤러에 Windows Admin Center 설치 하는 것은 지원 되지 않습니다. [도메인 컨트롤러 보안에 대해 자세히 알아보기 모범 사례](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/security-best-practices/securing-domain-controllers-against-attack)합니다. 

> [!IMPORTANT]
> Internet Explorer를 사용 하면 Windows Admin Center 관리할 수 없습니다-사용 해야 하는 대신 한 [지원 되는 브라우저](../understand/faq.md#which-web-browsers-are-supported-by-windows-admin-center
)합니다.  Windows Server에서 Windows Admin Center 설치 하는 경우에 Windows 10 및 Edge를 사용 하 여 원격으로 연결 하 여 관리 하는 것이 좋습니다.  또는 관리할 수 있습니다 로컬 Windows Server에서 지원 되는 브라우저를 설치한 경우.

## <a name="supported-operating-systems-management"></a>지원 되는 운영 체제: 관리

할 수 있습니다 **관리할** Windows Admin Center 사용 하 여 다음 Windows 운영 체제:

| 버전 | 관리할 *노드에* 를 통해 *서버 관리자* | 관리할 *클러스터* 를 통해 *장애 조치 클러스터 관리자* | 관리할 *HCI* 를 통해 *HCI 클러스터 관리자*|
|-------------------------|---------------|-----|------------------------|
| Windows 10 버전 1709 이상 | 예 (관리를 통해 컴퓨터) | 해당 사항 없음 | 해당 사항 없음 |
| Windows Server 반기 채널 | 예 | 예 | 해당 사항 없음 |
| Windows Server 2019 | 예 | 예 | 예 |
| Windows Server 2016 | 예 | 예 | 예, [최신 누적 업데이트](../use/manage-hyper-converged.md#prepare-your-windows-server-2016-cluster-for-windows-admin-center) |
| Microsoft Hyper-V Server 2016 | 예 | 예 | 해당 사항 없음 |
| Windows Server 2012 R2 | 예 | 예 | 해당 사항 없음 |
| Microsoft Hyper-V Server 2012 R2 | 예 | 예 | 해당 사항 없음 |
| Windows Server 2012 | 예 | 예 | 해당 사항 없음 |
| Windows Server 2008 R2 | 예, 제한 된 기능 | 해당 사항 없음 | 해당 사항 없음 |

> [!NOTE]
> Windows Admin Center는 Windows Server 2008 R2, 2012 및 2012 R2에에서 포함 되지 않은 PowerShell 기능이 필요 합니다. Windows Admin Center 사용 하 여 이러한 관리는 해당 서버의 Windows WMF (Management Framework) 5.1 이상 버전을 설치 해야 합니다.

>WMF가 설치되어 있는지, 그리고 버전이 5.1 이상인지 확인하려면 PowerShell에 `$PSVersiontable`을 입력합니다. 

>WMF를 설치 하지 않은 경우 [WMF 5.1 다운로드](https://www.microsoft.com/en-us/download/details.aspx?id=54616)합니다.

## <a name="deployment-options"></a>배포 옵션

| ![img](../media/deployment-options/W10.png) | ![img](../media/deployment-options/gateway.png) | ![img](../media/deployment-options/node.png) | ![img](../media/deployment-options/HA.png) |
|---|---|---|---|

| 로컬 클라이언트 | 게이트웨이 서버 | 관리되는 서버 | 장애 조치(failover) 클러스터 |
| --- | --- | --- | --- |
| 관리 되는 서버에 연결 된 로컬 Windows 10 클라이언트를 설치 합니다.  빠른 시작에서는 테스트, 특별 또는 소규모 시나리오에 적합 합니다. |지정 된 게이트웨이 서버에 설치 하 고 게이트웨이 서버에 연결 된 모든 클라이언트 브라우저에서 액세스 키를 누릅니다.  대규모 시나리오에 적합 합니다. | 자체 또는 멤버 노드는 클러스터를 관리할 목적으로 관리 되는 서버에 직접 설치 합니다.  배포 시나리오에 적합 합니다. | 게이트웨이 서비스의 고가용성을 사용 하도록 설정 하려면 장애 조치 클러스터에 배포 합니다. 관리 서비스의 복원 력을 보장 하려면 프로덕션 환경에 적합 합니다. |

## <a name="high-availability"></a>고가용성

장애 조치 클러스터의 활성-수동 모델에서 Windows Admin Center 배포 하 여 게이트웨이 서비스의 고가용성을 사용할 수 있습니다. 클러스터의 노드 중 하나가 실패 하면 Windows Admin Center 정상적으로 장애 조치를 다른 노드로 환경의 서버를 원활 하 게 관리를 계속할 수 있도록 합니다.

[고가용성을 사용 하 여 Windows Admin Center 배포 하는 방법에 알아봅니다.](../deploy/high-availability.md)

> [!Tip]
> Windows Admin Center를 설치할 준비가 되셨습니까? [지금 다운로드](https://aka.ms/windowsadmincenter)
