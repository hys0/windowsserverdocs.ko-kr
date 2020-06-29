---
title: 보호된 호스트 배포
ms.prod: windows-server
ms.topic: article
ms.assetid: 2379ca26-b32d-4055-8b4b-99d1f2df37e1
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 59b6aaa22fa89620df2ce6757b2d9f5ffe91c652
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475350"
---
# <a name="deploy-guarded-hosts"></a>보호된 호스트 배포

>적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016

이 섹션의 항목에서는 패브릭 관리자가 HGS (호스트 보호 서비스)와 함께 작동 하도록 Hyper-v 호스트를 구성 하는 단계에 대해 설명 합니다. 이러한 단계를 시작 하려면 먼저 HGS 클러스터에서 하나 이상의 노드를 [설정 해야](guarded-fabric-setting-up-the-host-guardian-service-hgs.md)합니다.

**TPM에서 신뢰할 수 있는 증명의 경우**:
1. [패브릭 Dns 구성](guarded-fabric-configuring-fabric-dns.md): 패브릭 도메인에서 HGS 도메인으로 DNS 전달자를 설정 하는 방법을 설명 합니다.
2. [HGS에 필요한 정보 캡처](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md): tpm 식별자 (플랫폼 식별자 라고도 함)를 캡처하고, 코드 무결성 정책을 만들고, tpm 기준을 만드는 방법을 알려줍니다. 그런 다음이 정보를 HGS 관리자에 게 제공 하 여 증명을 구성 합니다.
3. [보호 된 호스트가 증명할 수 있는지 확인](guarded-fabric-confirm-hosts-can-attest-successfully.md)

**호스트 키 증명의 경우**:
1. [호스트 키 만들기](guarded-fabric-create-host-key.md#create-a-host-key): 패브릭 도메인에서 HGS 도메인으로 DNS 전달자를 설정 하는 방법을 알려줍니다.
2. [증명 서비스에 호스트 키 추가](guarded-fabric-create-host-key.md#add-the-host-key-to-the-attestation-service): 패브릭 도메인에서 Active Directory 보안 그룹을 설정 하 고, 보호 된 호스트를 해당 그룹의 구성원으로 추가 하 고,이 그룹 식별자를 HGS 관리자에 게 제공 하는 방법을 알려줍니다.
3. [보호 된 호스트가 증명할 수 있는지 확인](guarded-fabric-confirm-hosts-can-attest-successfully.md)


**관리자가 신뢰할 수 있는 증명의 경우**:
1. [패브릭 Dns 구성](guarded-fabric-configuring-fabric-dns.md): 패브릭 도메인에서 HGS 도메인으로 DNS 전달자를 설정 하는 방법을 설명 합니다.
2. [보안 그룹 만들기](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md): 패브릭 도메인에서 Active Directory 보안 그룹을 설정 하 고, 보호 된 호스트를 해당 그룹의 구성원으로 추가 하 고,이 그룹 식별자를 HGS 관리자에 게 제공 하는 방법을 알려줍니다.
3. [보호 된 호스트가 증명할 수 있는지 확인](guarded-fabric-confirm-hosts-can-attest-successfully.md)


## <a name="additional-references"></a>추가 참조

- [보호 된 패브릭 및 보호 된 Vm에 대 한 배포 작업](guarded-fabric-deploying-hgs-overview.md#deployment-tasks-for-guarded-fabrics-and-shielded-vms)
