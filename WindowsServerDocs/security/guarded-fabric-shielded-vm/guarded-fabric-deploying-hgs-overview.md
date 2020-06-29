---
title: 호스트 보호자 서비스 배포
ms.prod: windows-server
ms.topic: article
ms.assetid: 310b63d9-5ac7-4961-98ef-103af45d706a
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 01/14/2020
ms.openlocfilehash: 9244dd8c9a567813c5732571de5dddc42d23be2a
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475590"
---
# <a name="deploying-the-host-guardian-service"></a>호스트 보호자 서비스 배포

>적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016

호스트 된 환경을 제공 하는 가장 중요 한 목표 중 하나는 환경에서 실행 되는 가상 컴퓨터의 보안을 보장 하는 것입니다. 클라우드 서비스 공급 기업 또는 엔터프라이즈 프라이빗 클라우드 관리자로서 보호된 패브릭을 사용하여 VM에 대한 더욱 안전한 환경을 제공할 수 있습니다. 보호된 패브릭은 하나의 HGS(호스트 보호 서비스) (일반적으로 3노드의 클러스터)에 하나 이상의 보호된 호스트 및 보호된 VM(가상 머신) 세트로 구성됩니다.

## <a name="video-deploying-a-guarded-fabric"></a>비디오: 보호 된 패브릭 배포

> [!VIDEO https://www.microsoft.com/videoplayer/embed/dcd8e99f-36f1-4bc8-b3d2-9576da38d9f1?autoplay=false]

## <a name="deployment-tasks-for-guarded-fabrics-and-shielded-vms"></a>보호 된 패브릭 및 보호 된 Vm에 대 한 배포 작업

다음 표에서는 보호 된 패브릭을 배포 하 고 다른 관리자 역할에 따라 보호 된 Vm을 만드는 작업을 분류 합니다. HGS 관리자가 권한 있는 Hyper-v 호스트를 사용 하 여 HGS를 구성 하는 경우 패브릭 관리자는 동시에 호스트에 대 한 식별 정보를 수집 하 여 제공 합니다.

|<img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-hgs-administrator-tasks.png" alt="Host Guardian Service administrator tasks" width="238" height="62" align="left" /> | <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-fabric-administrator-tasks.png" alt="Fabric administrator tasks" width="300" height="62" align="left" /> | <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-tenant-administrator-tasks.png" alt="Tenant administrator tasks" width="184" height="66" align="left" /> |
|-------------------------------------|--------------------------------|-----------------------------------------|
|(1) [HGS 필수 구성 요소 확인](guarded-fabric-prepare-for-hgs.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-verify.png" alt="Step 1" hspace="8" align="right" />| | |
|(2) [첫 번째 HGS &nbsp; 노드 구성](guarded-fabric-choose-where-to-install-hgs.md)&nbsp;<img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-first-hgs-node.png" alt="Step 2" hspace="8" align="right" />| | |
|(3) [추가 HGS &nbsp; 노드 구성](guarded-fabric-configure-additional-hgs-nodes.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-secondary-hgs-nodes.png" alt="Step 3" hspace="8" align="right" />| | |
| &nbsp; |(4) [패브릭 DNS 구성](guarded-fabric-configuring-fabric-dns.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-fabric-dns.png" alt="Step 4" hspace="8" align="right" />| |
| &nbsp; |(5) [호스트 &nbsp; 필수 구성 요소 확인 (키)](guarded-fabric-guarded-host-prerequisites.md#host-key-attestation)<br>[호스트 &nbsp; 필수 구성 요소 확인 (TPM)](guarded-fabric-guarded-host-prerequisites.md#tpm-trusted-attestation)<img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-verify.png" alt="Step 5" hspace="8" align="right" />| |
|(7) [호스트 정보를 사용 하 여 HGS 구성](guarded-fabric-add-host-information-to-hgs.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-hgs-with-host-info.png" alt="Step 7" hspace="8" align="right" />|(6) [호스트 키 만들기 (키)](guarded-fabric-create-host-key.md)<br>[호스트 정보 수집 (TPM)](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-collect-info-from-hosts.png" alt="Step 6" hspace="8" align="right" />| |
| &nbsp; |(8) [호스트에서 증명할 수 있는지 확인](guarded-fabric-confirm-hosts-can-attest-successfully.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-confirm-hosts-attest.png" alt="Step 8" hspace="8" align="right" />| |
| &nbsp; |(9) [VMM 구성 (선택 사항)](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-overview) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-vmm.png" alt="Step 9" hspace="8" align="right" />| |
| &nbsp; |(10) [템플릿 디스크 만들기](guarded-fabric-create-a-shielded-vm-template.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-create-template-disk.png" alt="Step 10" hspace="8" align="right" />| |
| &nbsp; |(11) [VMM에 대 한 VM 실딩 도우미 디스크 만들기 (선택 사항)](guarded-fabric-vm-shielding-helper-vhd.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-create-helper-disk.png" alt="Step 11" hspace="8" align="right" />| |
| &nbsp; |(12) [Windows Azure 팩 설정 (선택 사항)](guarded-fabric-shielded-vm-windows-azure-pack.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-windows-azure-pack.png" alt="Step 12" hspace="8" align="right" />| |
| &nbsp; | &nbsp; |(13) [보호 데이터 파일 만들기](guarded-fabric-tenant-creates-shielding-data.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-shielding-data-file.png" alt="Step 13" hspace="8" align="right" />|
| &nbsp; | &nbsp; |(14) [Windows Azure 팩를 사용 하 여 보호 된 Vm 만들기](guarded-fabric-shielded-vm-windows-azure-pack.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-shielded-vms.png" alt="Step 14" hspace="8" align="right" /><br>[VMM을 사용 하 여 보호 된 Vm 만들기](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-vms) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-shielded-vms.png" alt="Step 15" hspace="8" align="right" />|


## <a name="additional-references"></a>추가 참조

- [보호된 패브릭 및 보호된 VM](guarded-fabric-and-shielded-vms-top-node.md)
