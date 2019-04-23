---
title: 보호된 패브릭 및 보호된 VM
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 5c7ada81-2d97-41d4-87cf-1a7ccf06cd20
manager: dongill
author: rpsqrd
ms.author: justinha
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: c2c16574439569eeb1181977f23bae238f43865c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857434"
---
# <a name="guarded-fabric-and-shielded-vms"></a>보호된 패브릭 및 보호된 VM

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

호스팅된 환경을 제공 하는 가장 중요 한 목표 중 하나 환경에서 실행 중인 가상 컴퓨터의 보안을 보장 하는 것입니다. 클라우드 서비스 공급자 또는 엔터프라이즈 사설 클라우드 관리자로서 보호된 패브릭을 사용하여 VM에 대한 더욱 안전한 환경을 제공할 수 있습니다. 보호된 패브릭은 하나의 HGS(호스트 보호 서비스)(일반적으로 3노드의 클러스터)에 하나 이상의 보호된 호스트 및 보호된 가상 컴퓨터(VM) 세트로 구성됩니다.

> [!IMPORTANT]
> 프로덕션 환경에서 보호 된 가상 컴퓨터를 배포 하기 전에 최신 누적 업데이트를 설치 했는지 확인 합니다.

## <a name="videos-blog-and-overview-topic-about-guarded-fabrics-and-shielded-vms"></a>비디오, 블로그 및 개요 항목에 대 한 보호 패브릭 및 차폐 Vm

- 비디오: [가상화 패브릭 Windows Server 2019를 사용 하 여 내부자 위협 으로부터 보호 하는 방법](https://myignite.techcommunity.microsoft.com/sessions/64690)
- 비디오: [Windows Server 2016의에서 보호 된 Virtual Machines 소개](https://channel9.msdn.com/Shows/Mechanics/Introduction-to-Shielded-Virtual-Machines-in-Windows-Server-2016)
- 비디오: [Windows 사용 하 여 보호 된 Vm에 자세히 알아보기 Server 2016 Hyper-v](https://channel9.msdn.com/events/Ignite/2016/BRK3124)
- 비디오: [보호 된 Vm 및 Windows Server 2016으로 보호 된 패브릭 배포](https://mva.microsoft.com/en-US/training-courses/deploying-shielded-vms-and-a-guarded-fabric-with-windows-server-2016-17131?l=WFLef7vUD_4604300474)
- 블로그: [데이터 센터 및 사설 클라우드 보안 블로그](https://blogs.technet.microsoft.com/datacentersecurity/)
- 개요: [보호 된 패브릭 및 보호 된 Vm 개요](Guarded-Fabric-and-Shielded-VMs.md)

## <a name="planning-topics"></a>계획 항목

- [호스팅 서비스 공급자에 대 한 계획 가이드](guarded-fabric-planning-for-hosters.md)
- [테 넌 트에 대 한 계획 가이드](guarded-fabric-shielded-vm-planning-for-tenants.md)

## <a name="deployment-topics"></a>배포 항목

- [배포 가이드](guarded-fabric-deploying-hgs-overview.md)
    - [빠른 시작](guarded-fabric-deployment-overview.md)
    - [HGS를 배포 합니다.](guarded-fabric-setting-up-the-host-guardian-service-hgs.md)
    - [보호 된 호스트 배포](guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)
        - [보호 된 호스트 될 호스트에 대 한 패브릭 DNS 구성](guarded-fabric-configuring-fabric-dns.md)
        - [AD 모드를 사용 하 여 보호 된 호스트 배포](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md)
        - [TPM 모드를 사용 하 여 보호 된 호스트 배포](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md)
        - [보호 된 호스트 증명할 수 확인](guarded-fabric-confirm-hosts-can-attest-successfully.md)
        - [보호 된 Vm-호스팅 서비스 공급자를 VMM에서 보호 된 호스트 배포](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-hosts)
    - [보호 된 Vm 배포](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
        - [보호 된 VM 템플릿 만들기](guarded-fabric-create-a-shielded-vm-template.md)
        - [VM 실딩 도우미 VHD 준비](guarded-fabric-vm-shielding-helper-vhd.md)
        - [Windows Azure 팩 설정](guarded-fabric-hoster-sets-up-windows-azure-pack.md)
        - [실딩 데이터 파일을 만들려면](guarded-fabric-tenant-creates-shielding-data.md)
        - [Windows Azure Pack을 사용 하 여 보호 된 VM 배포](guarded-fabric-shielded-vm-windows-azure-pack.md)
        - [Virtual Machine Manager 사용 하 여 보호 된 VM 배포](guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)

## <a name="operations-and-management-topic"></a>작업 및 관리 항목

- [호스트 보호 서비스 관리](guarded-fabric-manage-hgs.md)
