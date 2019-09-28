---
title: 보호된 패브릭 및 보호된 VM
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 5c7ada81-2d97-41d4-87cf-1a7ccf06cd20
manager: dongill
author: rpsqrd
ms.author: justinha
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: c06432a039341978956066344710920652187b97
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403669"
---
# <a name="guarded-fabric-and-shielded-vms"></a>보호된 패브릭 및 보호된 VM

>적용 대상: Windows server 2019, Windows Server (반기 채널), Windows Server 2016

호스트 된 환경을 제공 하는 가장 중요 한 목표 중 하나는 환경에서 실행 되는 가상 컴퓨터의 보안을 보장 하는 것입니다. 클라우드 서비스 공급자 또는 엔터프라이즈 사설 클라우드 관리자로서 보호된 패브릭을 사용하여 VM에 대한 더욱 안전한 환경을 제공할 수 있습니다. 보호된 패브릭은 하나의 HGS(호스트 보호 서비스)(일반적으로 3노드의 클러스터)에 하나 이상의 보호된 호스트 및 보호된 가상 컴퓨터(VM) 세트로 구성됩니다.

> [!IMPORTANT]
> 프로덕션 환경에서 보호 된 가상 컴퓨터를 배포 하기 전에 최신 누적 업데이트를 설치 했는지 확인 합니다.

## <a name="videos-blog-and-overview-topic-about-guarded-fabrics-and-shielded-vms"></a>보호 된 패브릭 및 차폐 Vm에 대 한 비디오, 블로그 및 개요 항목

- 비디오: [Windows Server 2019를 사용 하 여 insider 위협 으로부터 가상화 패브릭을 보호 하는 방법](https://myignite.techcommunity.microsoft.com/sessions/64690)
- 비디오: [Windows Server 2016의 차폐 Virtual Machines 소개](https://channel9.msdn.com/Shows/Mechanics/Introduction-to-Shielded-Virtual-Machines-in-Windows-Server-2016)
- 비디오: [Windows Server 2016 Hyper-v를 사용 하 여 보호 된 Vm에 대해 알아보기](https://channel9.msdn.com/events/Ignite/2016/BRK3124)
- 비디오: [Windows Server 2016를 사용 하 여 보호 된 Vm 및 보호 된 패브릭 배포](https://mva.microsoft.com/en-US/training-courses/deploying-shielded-vms-and-a-guarded-fabric-with-windows-server-2016-17131?l=WFLef7vUD_4604300474)
- 치거나 [데이터 센터 및 사설 클라우드 보안 블로그](https://blogs.technet.microsoft.com/datacentersecurity/)
- 개요: [보호된 패브릭 및 보호된 VM 개요](Guarded-Fabric-and-Shielded-VMs.md)

## <a name="planning-topics"></a>계획 항목

- [호스팅 서비스 공급자 계획 가이드](guarded-fabric-planning-for-hosters.md)
- [테 넌 트 계획 가이드](guarded-fabric-shielded-vm-planning-for-tenants.md)

## <a name="deployment-topics"></a>배포 항목

- [배포 가이드](guarded-fabric-deploying-hgs-overview.md)
    - [빠른 시작](guarded-fabric-deployment-overview.md)
    - [HGS 배포](guarded-fabric-setting-up-the-host-guardian-service-hgs.md)
    - [보호된 호스트 배포](guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)
        - [보호 되는 호스트가 될 호스트에 대 한 패브릭 DNS 구성](guarded-fabric-configuring-fabric-dns.md)
        - [AD 모드를 사용 하 여 보호 된 호스트 배포](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md)
        - [TPM 모드를 사용 하 여 보호 된 호스트 배포](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md)
        - [보호 된 호스트가 증명할 수 있는지 확인](guarded-fabric-confirm-hosts-can-attest-successfully.md)
        - [보호 된 Vm-호스팅 서비스 공급자가 VMM에서 보호 된 호스트를 배포 합니다.](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-hosts)
    - [보호된 VM 배포](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
        - [보호 된 VM 템플릿 만들기](guarded-fabric-create-a-shielded-vm-template.md)
        - [VM 실딩 도우미 VHD 준비](guarded-fabric-vm-shielding-helper-vhd.md)
        - [Windows Azure 팩 설치](guarded-fabric-hoster-sets-up-windows-azure-pack.md)
        - [보호 데이터 파일 만들기](guarded-fabric-tenant-creates-shielding-data.md)
        - [Windows Azure 팩를 사용 하 여 보호 된 VM 배포](guarded-fabric-shielded-vm-windows-azure-pack.md)
        - [Virtual Machine Manager를 사용 하 여 보호 된 VM 배포](guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)

## <a name="operations-and-management-topic"></a>작업 및 관리 항목

- [호스트 보호자 서비스 관리](guarded-fabric-manage-hgs.md)
