---
title: 어떤 유형의 설치는 여러분에 게 적합
description: 이 항목에서는 Windows Admin Center를 포함 하 여 여러 관리자가 Windows 10 PC 또는 사용 하기 위해 Windows server에 설치에 대 한 다른 설치 옵션에 설명 합니다.
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 04/12/2019
ms.openlocfilehash: cc6f9e6c2f2572618c1c5fdae00047d24fbeb3cf
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296665"
---
# 나에게 적합한 유형의 설치는 무엇입니까?

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

이 항목에서는 Windows Admin Center를 포함 하 여 여러 관리자가 Windows 10 PC 또는 사용 하기 위해 Windows server에 설치에 대 한 다른 설치 옵션에 설명 합니다. Azure의 VM에서 Windows Admin Center를 설치 하려면 [Azure에서 Windows Admin Center 배포를](../azure/deploy-wac-in-azure.md)참조 하세요.

## 지원 되는 운영 체제: 설치

**설치** Windows Admin Center는 다음 Windows 운영 체제에서 수행할 수 있습니다.

| **버전** | **설치 모드** |
|-------------|-----------------------|
|Windows 10, 버전 1709 이상 | 데스크톱 모드 |
|Windows Server 반기 채널 | 게이트웨이 모드 |
|WindowsServer 2016 | 게이트웨이 모드 |
|WindowsServer 2019 | 게이트웨이 모드 |

**데스크톱 모드:** 시작 메뉴에서 시작 하 고이 설치 된 동일 컴퓨터에서 Windows Admin Center 게이트웨이에 연결 (예: `https://localhost:6516`)

**게이트웨이 모드:** 다른 컴퓨터의 클라이언트 브라우저에서 Windows Admin Center 게이트웨이에 연결 (예: `https://servername.contoso.com`) 

> [!WARNING]
> 도메인 컨트롤러에서 Windows Admin Center를 설치 하는 것은 지원 되지 않습니다. [도메인 컨트롤러 보안 모범 사례에 대해 자세히 읽어보세요](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/security-best-practices/securing-domain-controllers-against-attack). 

> [!IMPORTANT]
> Windows Admin Center를 관리 하는 Internet Explorer를 사용할 수 없습니다-대신 사용 하 여 [브라우저를 지원](../understand/faq.md#which-web-browsers-are-supported-by-windows-admin-center
)해야 합니다.  Windows Server에서 Windows Admin Center를 설치 하는 경우에 Windows 10 및 Edge를 사용 하 여 원격으로 연결 하 여 관리 하는 것이 좋습니다.  또는 관리할 수 있습니다 로컬로 Windows 서버에서 지원 되는 브라우저를 설치한 경우.

## 지원 되는 운영 체제: 관리

**관리** Windows Admin Center를 사용 하 여 다음 Windows 운영 체제 것 기능은 다음과 같습니다.

| 버전 | *서버 관리자* 를 통해 *노드* 관리 합니다. | *장애 조치 클러스터 관리자* 를 통해 *클러스터* 관리 | *HCI* *HCI 클러스터 관리자* 를 통해 관리|
|-------------------------|---------------|-----|------------------------|
| Windows 10, 버전 1709 이상 | 예 (컴퓨터 관리) | 해당 없음 | 해당 없음 |
| Windows Server 반기 채널 | 예 | 예 | 해당 없음 |
| WindowsServer 2019 | 예 | 예 | 예 |
| WindowsServer 2016 | 예 | 예 | 예, [최신 누적 업데이트](../use/manage-hyper-converged.md#prepare-your-windows-server-2016-cluster-for-windows-admin-center) |
| Microsoft Hyper-V Server 2016 | 예 | 예 | 해당 없음 |
| WindowsServer 2012 R2 | 예 | 예 | 해당 없음 |
| Microsoft Hyper-V Server 2012 R2 | 예 | 예 | 해당 없음 |
| Windows Server 2012 | 예 | 예 | 해당 없음 |
| Windows Server 2008 R2 | 예, 제한 된 기능 | 해당 없음 | 해당 없음 |

> [!NOTE]
> Windows Admin Center는 Windows Server 2008 R2, 2012 및 2012 r 2에에서 포함 되지 않은 PowerShell 기능이 필요 합니다. Windows Admin Center를 사용 하 여이 관리, 해당 서버에 Windows Management Framework (WMF) 버전 5.1 이상을 설치 해야 합니다.

>WMF가 설치되어 있는지, 그리고 버전이 5.1 이상인지 확인하려면 PowerShell에 `$PSVersiontable`을 입력합니다. 

>WMF 설치 되어 있지 않으면 [WMF 5.1을 다운로드](https://www.microsoft.com/en-us/download/details.aspx?id=54616)할 수 있습니다.

## 배포 옵션

| ![img](../media/deployment-options/W10.png) | ![img](../media/deployment-options/gateway.png) | ![img](../media/deployment-options/node.png) | ![img](../media/deployment-options/HA.png) |
|---|---|---|---|

| 로컬 클라이언트 | 게이트웨이 서버 | 관리 되는 서버 | 장애 조치(failover) 클러스터 |
| --- | --- | --- | --- |
| 관리 되는 서버에 연결 되어 있는 로컬 Windows 10 클라이언트에 설치 합니다.  빠른 시작, 테스트, 임시 또는 소규모 시나리오에 적합 합니다. |지정 된 게이트웨이 서버에 설치 하 고 게이트웨이 서버에 연결 된 모든 클라이언트 브라우저에서 액세스 합니다.  대규모 시나리오에 이상적입니다. | 자체 또는 구성원 노드 중인 클러스터를 관리 하기 위한 목적으로 관리 되는 서버에 직접 설치 합니다.  분산 된 시나리오에 이상적입니다. | 게이트웨이 서비스의 고가용성 장애 조치 클러스터를 배포 합니다. 관리 서비스의 복원 력을 위해 프로덕션 환경에 적합 합니다. |

## 고가용성

장애 조치 클러스터에서 활성 수동 모델에서 Windows Admin Center를 배포 하 여 고가용성 게이트웨이 서비스를 사용할 수 있습니다. 클러스터 노드 중 하나에 실패 하는 경우 Windows Admin Center 정상적으로 장애 조치 다른 노드로 환경에서 서버를 원활 하 게 관리 계속 수 있습니다.

[높은 가용성과 함께 Windows Admin Center를 배포 하는 방법을 알아봅니다.](../deploy/high-availability.md)

> [!Tip]
> Windows Admin Center를 설치할 준비가 되셨습니까? [지금 다운로드](https://aka.ms/windowsadmincenter)
