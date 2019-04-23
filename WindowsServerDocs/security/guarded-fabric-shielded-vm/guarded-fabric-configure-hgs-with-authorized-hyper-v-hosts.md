---
title: 보호된 호스트 배포
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 2379ca26-b32d-4055-8b4b-99d1f2df37e1
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 3b20a7eb2b5097d8ddb7381fd0304581ca4e6722
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845354"
---
# <a name="deploy-guarded-hosts"></a>보호된 호스트 배포

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

이 섹션의에서 항목에서는 패브릭 관리자를 사용 하 여의 보호 서비스 (HGS (호스트)를 작동 하려면 Hyper-v 호스트를 구성 하는 단계를 설명 합니다. 이 단계에서 하나 이상의 노드를 시작 하기 전에 합니다 [HGS 클러스터를 설정 해야](guarded-fabric-setting-up-the-host-guardian-service-hgs.md)합니다.

**신뢰할 수 있는 TPM 증명에 대 한**:
1. [패브릭을 DNS 구성](guarded-fabric-configuring-fabric-dns.md): HGS 도메인에 fabric 도메인에서 DNS 전달자를 설정 하는 방법을 알려줍니다.
2. [HGS에 필요한 정보를 캡처할](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md): TPM 식별자 (플랫폼 식별자 라고도 함)를 캡처, 코드 무결성 정책을 만들고, TPM 기준을 만듭니다를 하는 방법을 설명 합니다. 그런 다음 증명을 구성 하도록 HGS 관리자에 게이 정보를 제공 합니다.
3. [보호 된 호스트 증명할 수 확인](guarded-fabric-confirm-hosts-can-attest-successfully.md)

**호스트 키 증명에 대 한**:
1. [호스트 키를 만들](guarded-fabric-create-host-key.md#create-a-host-key): HGS 도메인에 fabric 도메인에서 DNS 전달자를 설정 하는 방법을 알려줍니다.
2. [호스트 키 증명 서비스를 추가](guarded-fabric-create-host-key.md#add-the-host-key-to-the-attestation-service): HGS 관리자에 게는 그룹 식별자를 제공 하 고 해당 그룹의 구성원으로 보호 된 호스트를 추가 패브릭 도메인의 Active Directory 보안 그룹을 설정 하는 방법을 알려줍니다. 
3. [보호 된 호스트 증명할 수 확인](guarded-fabric-confirm-hosts-can-attest-successfully.md)


**관리자-신뢰할 수 있는 증명에 대 한**:
1. [패브릭을 DNS 구성](guarded-fabric-configuring-fabric-dns.md): HGS 도메인에 fabric 도메인에서 DNS 전달자를 설정 하는 방법을 알려줍니다.
2. [보안 그룹 만들기](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md): HGS 관리자에 게는 그룹 식별자를 제공 하 고 해당 그룹의 구성원으로 보호 된 호스트를 추가 패브릭 도메인의 Active Directory 보안 그룹을 설정 하는 방법을 알려줍니다. 
3. [보호 된 호스트 증명할 수 확인](guarded-fabric-confirm-hosts-can-attest-successfully.md)


## <a name="see-also"></a>참조

- [배포 작업에 대 한 보호 패브릭 및 차폐 Vm](guarded-fabric-deploying-hgs-overview.md#deployment-tasks-for-guarded-fabrics-and-shielded-vms)
