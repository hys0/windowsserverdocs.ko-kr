---
title: Hyper-v에 대한 1 세대 가상 머신의 보안 설정
description: 1세대 가상 머신의 Hyper-V 관리자에서 사용할 수 있는 보안 설정에 대해 설명합니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: f8f8c569-8b74-4c19-876e-1c7d00cce308
author: larsiwer
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 01a4882ec766673af5ff8f57debb829ace743d77
ms.sourcegitcommit: 457e88e5aa6be13a2bffdb8e434a8efc3698678f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548706"
---
# <a name="generation-1-virtual-machine-security-settings"></a>1 세대 가상 머신의 보안 설정

>적용 대상: Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

Hyper-v 관리자 1 세대 가상 머신의 보안 설정에 사용하여 데이터 및 가상 머신의 상태를 보호합니다.

## <a name="encryption-support-settings-in-hyper-v-manager"></a>Hyper-v 관리자의 암호화 지원 설정

다음과 같은 암호화 지원 옵션을 선택하여 데이터와 가상 머신의 상태를 보호할 수 있습니다.

- **상태 및 가상 머신 마이그레이션 트래픽을 암호화** - 실시간 마이그레이션 트래픽을 디스크에 기록할 때 저장된 가상 머신 상태를 암호화합니다.

이 옵션을 설정하려면 가상 머신에 대한 키 스토리지 드라이브를 추가해야 합니다.

## <a name="key-storage-drive-in-hyper-v-manager"></a>Hyper-V 관리자에서 키 스토리지 드라이브

키 스토리지 드라이브는 저장될 BitLocker에 대한 가상 머신에 작은 드라이브를 제공합니다. 따라서 가상 머신의 운영 체제 디스크는 가상화된 신뢰할 수 있는 TPM (플랫폼 모듈) 칩을 요구하지 않고 암호화를 수 있습니다. 키 스토리지 드라이브의 내용이 키 보호기를 사용하여 암호화됩니다. 가상 머신을 실행하는 키 보호기 authories Hyper-v 호스트입니다. 키 스토리지 드라이브와 키 보호기의 내용은 가상 머신의 런타임 상태의 일부로 저장됩니다.

키 스토리지 드라이브의 내용을 해독하고 가상 머신을 시작하려면 Hyper-V 호스트는 다음이 필요합니다.

- 이 가상 머신에는 권한 있는 가드 된 패브릭의 일부 또는
- 가상 머신의 보호자 중 하나에서 프라이빗 키를 있습니다.

보호 된 패브릭에 대 한 자세한 내용은의 차폐 Vm 소개 섹션을 참조 하십시오 [보안 및 보증](../../../security/Security-and-Assurance.yml)합니다.

가상 머신의 IDE 컨트롤러 중 하나를 빈 슬롯 키 스토리지 드라이브를 추가할 수 있습니다. 이 작업을 수행하려면 **키 스토리지 드라이브 추가**를 클릭하여 이 가상 머신의 첫 번째 무료 IDE 컨트롤러 슬롯에 키 스토리지 드라이브를 추가하세요.

## <a name="additional-references"></a>추가 참조

- [Hyper-V 관리자에서 2세대 가상 머신 보안 설정](Generation-2-virtual-machine-security-settings-for-hyper-v.md)
- [보안 및 보증](../../../security/Security-and-Assurance.yml)