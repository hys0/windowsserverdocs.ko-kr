---
title: Hyper-v에 대 한 1 세대 가상 컴퓨터의 보안 설정
description: 1 세대 가상 컴퓨터에 대 한 Hyper-v 관리자에서 사용할 수 있는 보안 설정을 설명합니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f8f8c569-8b74-4c19-876e-1c7d00cce308
author: larsiwer
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 923216142a45071bc3623e3f37b37cc6a2361f26
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812144"
---
# <a name="generation-1-virtual-machine-security-settings"></a>1 세대 가상 컴퓨터의 보안 설정

>적용 대상: Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

Hyper-v 관리자 1 세대 가상 컴퓨터의 보안 설정의 사용 하 여 데이터 및 가상 컴퓨터의 상태를 보호 합니다.

## <a name="encryption-support-settings-in-hyper-v-manager"></a>Hyper-v 관리자의 암호화 지원 설정

다음과 같은 암호화 지원 옵션을 선택 하 여 데이터와 가상 컴퓨터의 상태를 보호할 수 있습니다.

- **상태 및 가상 컴퓨터 마이그레이션 트래픽을 암호화** -실시간 마이그레이션 트래픽을 디스크에 기록 될 때 저장 된 가상 컴퓨터 상태를 암호화 합니다.

이 옵션을 설정 하려면 가상 컴퓨터에 대 한 키 저장소 드라이브를 추가 해야 합니다.

## <a name="key-storage-drive-in-hyper-v-manager"></a>Hyper-v 관리자에서 키 저장소 드라이브

키 저장소 드라이브는 BitLocker 키를 저장할 수에 대 한 가상 컴퓨터에 작은 드라이브를 제공 합니다. 따라서 가상 컴퓨터의 운영 체제 디스크는 가상화 된 신뢰할 수 있는 TPM (플랫폼 모듈) 칩을 요구 하지 않고 암호화를 수 있습니다. 키 저장소 드라이브의 내용이 키 보호기를 사용 하 여 암호화 됩니다. 가상 컴퓨터를 실행 하는 키 보호기 authories Hyper-v 호스트입니다. 키 저장소 드라이브와 키 보호기의 내용은 가상 컴퓨터의 런타임 상태의 일부로 저장 됩니다.

키 저장소 드라이브의 내용을 해독 하 고 가상 컴퓨터를 시작 하려면 Hyper-v 호스트 여야 필요 합니다.

- 이 가상 컴퓨터에는 권한 있는 가드 된 패브릭의 일부 또는
- 가상 머신의 보호자 중 하나에서 프라이빗 키를 있습니다.

보호 된 패브릭에 대 한 자세한 내용은의 차폐 Vm 소개 섹션을 참조 하십시오 [보안 및 보증](../../../security/Security-and-Assurance.md)합니다.

가상 컴퓨터의 IDE 컨트롤러 중 하나를 빈 슬롯 키 저장소 드라이브를 추가할 수 있습니다. 이 작업을 수행 하려면 **키 저장소 드라이브 추가** 이 가상 컴퓨터의 첫 번째 무료 IDE 컨트롤러 슬롯에 키 저장소 드라이브를 추가 합니다.

##<a name="see-also"></a>참조

- [Hyper-v 관리자에서 2 세대 가상 머신의 보안 설정](Generation-2-virtual-machine-security-settings-for-hyper-v.md)
- [보안 및 보증](../../../security/Security-and-Assurance.md)