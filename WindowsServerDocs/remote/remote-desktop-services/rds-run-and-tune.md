---
title: RDS - 실행 및 조정
description: 원격 데스크톱 서비스에 대한 관리 정보를 제공합니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: spatnaik
ms.date: 02/08/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 79909767-a4c3-4ecf-8d3f-77d37a663153
author: spatnaik
manager: scottman
ms.openlocfilehash: 5a2aa5c166b41ed8bd04ccfb92911368c07a5459
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71387161"
---
# <a name="run-and-tune-your-remote-desktop-services-environment"></a>원격 데스크톱 서비스 환경 실행 및 조정

배포 조정은 시간이 걸리며 계측 및 모니터링이 필요합니다. 아래 프로세스를 사용하여 원격 데스크톱 배포를 구체화하고, 실행을 유지하고 필요에 따라 확장을 활성화합니다. 

메트릭을 지속적으로 평가하고 실행 비용의 균형을 유지하는 것이 좋습니다.

## <a name="management-and-monitoring"></a>관리 및 모니터링

데스크톱 및 원격 리소스에 대한 액세스를 관리하는 방법에 대한 정보는 [RDS 컬렉션의 사용자 관리](rds-user-management.md)를 확인하세요.

**Microsoft Operations Management Suite(OMS)** 를 사용하여 잠재적인 병목 상태에 대한 원격 데스크톱 배포를 모니터링하고 다음 방법 중 하나를 사용하여 관리합니다. 

- **서버 관리자**: Windows Server에 기본 제공된 RD 관리 도구를 사용하여 최대 500개의 동시 원격 최종 사용자로 배포를 관리합니다. 
- **PowerShell**: Windows Server에 기본 제공된 RD PowerShell 모듈을 사용하여 최대 5000개의 동시 원격 최종 사용자로 배포를 관리합니다.

## <a name="scale-bigger-better-faster"></a>배율: 더 크고, 더 뛰어나며, 더 빠름

배포에 대한 가시성으로 보다 정확하게 배율을 제어할 수 있습니다. 배율 요구에 따라 원격 데스크톱 호스트 서버를 쉽게 추가하거나 제거합니다. 

Azure에서 빌드된 원격 데스크톱 배포는 Azure SQL과 같은 Azure 서비스를 사용하여 요청 시 자동으로 비율 크기 조정할 수 있습니다.

## <a name="automation-script-for-success"></a>자동화: 성공을 위한 스크립트

실행 중인 고도로 확장된 애플리케이션을 유지 관리하려면 정기적으로 작업을 반복해야 합니다. 원격 데스크톱 서비스 PowerShell cmdlet 및 WMI 공급 기업을 사용하여 필요한 경우 여러 배포에서 실행될 수 있는 스크립트를 개발합니다. 배포에서 원격 데스크톱 서비스에 대한 모범 사례 분석기(BPA) 규칙을 실행하여 배포를 조정합니다.

## <a name="load-testing-avoid-surprises"></a>로드 테스트: 문제 방지

스트레스 테스트와 실제 사용 시뮬레이션으로 배포를 로드 테스트합니다. 놀라는 부하 크기를 다르게 지정! 응답성 사용자 요구 사항을 충족 하는지 확인 하는 전체 시스템 복원 력이 뛰어난 인지 확인 합니다. LoginVSI와 같이 사용자의 요구를 충족하는 배포의 능력을 검사하는 시뮬레이션 도구를 사용하여 부하 테스트를 만듭니다. 