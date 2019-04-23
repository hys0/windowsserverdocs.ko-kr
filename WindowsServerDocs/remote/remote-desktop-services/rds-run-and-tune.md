---
title: RDS-실행 및 조정
description: 원격 데스크톱 서비스에 대 한 관리 정보를 제공합니다.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 40f8dbd560da359e8764ed715e7776cc2d230a7f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862184"
---
# <a name="run-and-tune-your-remote-desktop-services-environment"></a>실행 및 원격 데스크톱 서비스 환경 조정

배포 튜닝 시간이 걸리며 계측 및 모니터링에 필요 합니다. 원격 데스크톱 배포를 구체화 하 고, 실행, 필요에 따라 확장 (및) 확장을 사용 하도록 설정 하려면 아래 프로세스를 사용 합니다. 

메트릭 및 분산 실행 비용에 대해 지속적으로 평가 하는 것이 좋습니다.

## <a name="management-and-monitoring"></a>관리 및 모니터링

체크 아웃 [RDS 컬렉션에서 사용자 관리](rds-user-management.md) 데스크톱 및 원격 리소스에 대 한 액세스를 관리 하는 방법에 대 한 정보에 대 한 합니다.

사용 하 여 **Microsoft Operations Management Suite (OMS)** 잠재적인 병목 상태에 대 한 원격 데스크톱 배포를 모니터링 하 고 다음 방법 중 하나를 사용 하 여 관리 합니다. 

- **서버 관리자**: 최대 500 개의 동시 원격 최종 사용자를 사용 하 여 배포를 관리 하려면 Windows Server에 기본 제공 RD 관리 도구를 사용 합니다. 
- **PowerShell**: 최대 5000 개의 동시 원격 최종 사용자를 사용 하 여 배포를 관리 하려면 Windows Server에도 기본적으로, RD PowerShell 모듈을 사용 합니다.

## <a name="scale-bigger-better-faster"></a>확장: 더 큰, 더 뛰어나고 더 빠릅니다

배포에 대 한 가시성을 사용 하 여 전체 자릿수를 사용 하 여 확장을 제어할 수 있습니다. 쉽게 추가 하거나 확장 요구에 따라 원격 데스크톱 호스트 서버를 제거 합니다. 

Azure에서 빌드된 원격 데스크톱 배포 가능 사용 하 여 Azure SQL과 유사한 Azure 서비스에 요청 시 자동으로 확장 합니다.

## <a name="automation-script-for-success"></a>Automation: 성공에 대 한 스크립트

고도로 확장 된 응용 프로그램을 실행 중인 유지 관리를 정기적으로 작업을 반복 해야 합니다. 필요한 경우 여러 배포에서 실행 될 수 있는 스크립트를 개발 하려면 원격 데스크톱 서비스 PowerShell cmdlet 및 WMI 공급자를 사용 합니다. 배포를 조정 하 여 배포에서 원격 데스크톱 서비스에 대 한 분석기 BPA (모범 사례) 규칙을 실행 합니다.

## <a name="load-testing-avoid-surprises"></a>부하 테스트: 문제를 방지합니다

부하 스트레스 테스트와 실제 사용 시뮬레이션을 사용 하 여 배포를 테스트 합니다. 놀라는 부하 크기를 다르게 지정! 응답성 사용자 요구 사항을 충족 하는지 확인 하는 전체 시스템 복원 력이 뛰어난 인지 확인 합니다. LoginVSI, 같은 사용자의 요구를 충족 하는 배포의 능력을 검사 하는 시뮬레이션 도구와 부하 테스트를 작성 합니다. 