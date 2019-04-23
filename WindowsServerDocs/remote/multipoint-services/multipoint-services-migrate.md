---
title: Windows Server 2016에서에서 MultiPoint Service로 마이그레이션
description: MultiPoint 서비스의 이전 버전에서 마이그레이션하는 방법을 알아봅니다
ms.custom: na
ms.date: 07/29/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 16c217ad-700a-48a3-8398-4a7f7e9edb52
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: 24c35c31bf920c41bafa16901ee30a023565dad8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861204"
---
# <a name="multipoint-services-migration-in-windows-server-2016"></a>Windows Server 2016에서 multiPoint 서비스 마이그레이션
>적용 대상: Windows Server 2016

MultiPoint 서비스의 RTM 버전의 Windows Server 2016 MultiPoint 서비스 이전 버전에서 마이그레이션할 수 있습니다. 다음 정보는 정보 및 마이그레이션 및 확인 단계 준비를 제공합니다.

마이그레이션 설명서 및 도구는 서버 역할 설정 및 Windows Server 2016를 실행 하는 대상 서버에는 기존 서버에서 데이터의 마이그레이션 과정을 용이 합니다. 이 가이드에서 설명하는 프로세스를 사용하면 마이그레이션 프로세스를 간소화하고 마이그레이션 시간을 단축하는 한편, 마이그레이션 프로세스의 정확성을 높여 마이그레이션 프로세스를 진행하는 동안 그 밖에 발생할 수 있는 충돌을 방지할 수 있습니다. 

## <a name="what-to-know-before-you-begin"></a>시작 하기 전에 알아야 할 사항
마이그레이션 프로세스를 시작 하기 전에 다음 note 하십시오.

- 마이그레이션 프로세스는 자동으로 수집 하거나 MultiPoint 서비스 역할에서 응용 프로그램에 대 한 설정을 기록 합니다. 마이그레이션하려는 모든 응용 프로그램에 대 한 사용자 지정 된 마이그레이션 계획을 세워야 합니다. MultiPoint 서비스의 가상 데스크톱 기능을 사용 하는 경우에 마찬가지입니다.
- 이 가이드는 데이터 이동에 대 한 지침 사용자에 저장 하거나 공유 MultiPoint 서버에서 폴더를 제공 하지 않습니다. 이 일반 스테이션 및 가상 데스크톱에 적용 스테이션 합니다.
- 이 가이드는 원본 서버에서 여러 역할을 실행 하는 경우 마이그레이션하는 방법에 대 한 지침을 포함 하지 않습니다. 서버에서 여러 역할을 실행 하는 경우 역할 마이그레이션 가이드에 제공 된 정보에 따라 서버 환경에 관련 된 사용자 지정 마이그레이션 절차를 디자인 해야 합니다.
- 이 가이드에는 마이그레이션 원격 데스크톱 서비스 CAL에 대 한 정보가 없습니다. 이 정보를 참조 하십시오. [마이그레이션하려면 원격 데스크톱 서비스 클라이언트 액세스 라이선스 (RDS Cal)](https://technet.microsoft.com/library/dd851844.aspx)합니다.

## <a name="supported-migration-scenarios-for-multipoint-services-in-windows-server-2016"></a>Windows Server 2016에서 MultiPoint 서비스에 대 한 지원 되는 마이그레이션 시나리오
MultiPoint 서비스 역할 서비스는 Windows Server 2016 Standard 및 Datacenter 제공 됩니다. 이 마이그레이션 가이드는 Windows Server 2016 동일한 버전을 실행 하는 대상 서버를 실행 하는 원본 서버에서 Multipoint 서비스 역할 서비스를 마이그레이션하는 방법을 설명 합니다.

## <a name="scenarios-that-are-not-supported"></a>지원 되지 않는 시나리오

다음 마이그레이션 시나리오는 지원되지 않습니다.

- 마이그레이션 또는 Windows MultiPoint Server 2012 및 2011에서 업그레이드 합니다.
- 다른 시스템 UI 언어가 설치 된 운영 체제에서 실행 되는 대상 서버에는 원본 서버에서 마이그레이션.
- 가상 컴퓨터에 물리적 서버에서 MultiPoint 서비스 역할 서비스를 마이그레이션.
- MultiPoint 서버에서 모든 응용 프로그램 또는 응용 프로그램 설정 마이그레이션입니다.

## <a name="the-impact-of-migration-on-multipoint-services"></a>MultiPoint 서비스에 대 한 마이그레이션의 영향
MultiPoint 서비스 역할은 사용할 수 없음을 마이그레이션하는 동안 주의 합니다. 가동 중지 시간을 최소화하고 사용자에게 미치는 영향을 줄이려면 사용량이 많은 시간을 피해서 데이터 마이그레이션을 계획해야 합니다. 또한 마이그레이션 중에는 리소스를 사용할 수 없음을 사용자에게 알려야 합니다.

## <a name="migration-information-and-steps"></a>마이그레이션 정보 및 단계
MultiPoint 서비스 마이그레이션을 계획 및 수행 하려면 다음 정보를 사용 합니다.

- [마이그레이션에 대 한 필요한 정보를 수집 합니다.](multipoint-services-migration-preparation.md)
- [MultiPoint 서비스 역할 서비스를 마이그레이션하십시오.](multipoint-services-migration-steps.md)
- [마이그레이션 확인 및 마이그레이션 후 정리 작업 수행](multipoint-services-post-migration-steps.md)