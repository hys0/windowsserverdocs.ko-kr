---
title: Windows Server 2016에 Hyper-v의 새로운 기능
description: Hyper-v에서의 새로운 기능 요약을 제공합니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1a65a98e-54b6-4c41-9732-1e3d32fe3a5f
author: KBDAzure
ms.author: kathydav
ms.date: 09/21/2017
ms.openlocfilehash: 1384a15d3b8ecee32d36c6265d478edace0bdb09
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848104"
---
# <a name="whats-new-in-hyper-v-on-windows-server-2016"></a>Windows Server 2016에 Hyper-v의 새로운 기능

>적용 대상: Microsoft Hyper-V Server 2016, Windows Server 2016
  
이 문서에서는 Windows Server 2016 및 Microsoft Hyper-v Server 2016에 Hyper-v의 새로운 기능과 변경 된 기능을 설명 합니다. Windows Server 2012 r 2를 사용 하 여 만든 이동 하거나 Windows Server 2016에서 Hyper-v를 실행 하는 서버에 가져온 가상 컴퓨터에서 새 기능을 사용 하려면 가상 컴퓨터 구성 버전을 수동으로 업그레이드 해야 합니다. 자세한 내용은 [가상 컴퓨터를 업그레이드 버전](deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md)합니다.  
  
다음은이 문서에 포함 된 항목 및 기능은 새로운 또는 업데이트 된 여부입니다.  

## <a name="BKMK_standby"></a>연결 된 대기 상태와 호환 \(새\)
항상 On/Always 연결 (AOAC) 전원 모델을 사용 하는 컴퓨터에 Hyper-v 역할을 설치할 때의 **연결 된 대기** 전원 상태를 출시 되었습니다.  
  
## <a name="BKMK_device"></a>불연속 장치 할당 \(새\) 
이 기능은 일부 PCIe 하드웨어 장치에 가상 컴퓨터 직접 및 단독 액세스할 수 있도록 수 있습니다. 이러한 방식으로 장치를 사용 하 여 빠른 액세스는 Hyper-v 가상화 스택을 무시 합니다. 에 대 한 자세한 내용은 지원 되는 하드웨어, "불연속 장치 할당"을 참조 [Windows Server 2016에서 Hyper-v에 대 한 시스템 요구 사항](System-requirements-for-Hyper-V-on-Windows.md)합니다. 게시물을 참조 하는이 기능 및 고려 사항을 사용 하는 방법을 비롯 한 세부 정보에 대 한 "[불연속 장치 할당-설명 및 배경](https://blogs.technet.microsoft.com/virtualization/2015/11/19/discrete-device-assignment-description-and-background/)" 가상화 블로그에서입니다.

## <a name="encryption-support-for-the-operating-system-disk-in-generation-1-virtual-machines-new"></a>1 세대 가상 컴퓨터에 운영 체제 디스크에 대 한 암호화 지원을 \(새로 만들기)

이제 BitLocker 드라이브 암호화를 사용 하 여 1 세대 가상 컴퓨터에 운영 체제 디스크를 보호할 수 있습니다. 키 저장소는 새로운 기능을 시스템 드라이브의 BitLocker 키를 저장할 수 있는 작은 전용된 드라이브를 만듭니다. 2 세대 가상 컴퓨터에만 제공 되는 가상 모듈 TPM (Trusted Platform)를 사용 하는 대신 수행 됩니다. 디스크의 암호를 해독 하 고 가상 컴퓨터를 시작하려면 Hyper-v 호스트는 인증된 가드 된 패브릭의 일부 이거나 가상 컴퓨터의 보호자 중 하나에서 프라이빗 키가 있습니다. 키 저장소 버전 8 가상 컴퓨터를 필요합니다. 가상 컴퓨터 버전에 대 한 자세한 내용은 참조 [Windows 10 또는 Windows Server 2016에 Hyper-v에서 가상 컴퓨터를 업그레이드 버전](./deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md)합니다.  
  
## <a name="BKMK_host"></a>호스트 리소스 보호 \(새\)
이 기능을 사용 하면 과도 한 수준의 작업에 대 한 조회 하 여 사용 하 여 시스템 리소스를 공유 하는 보다 많은 가상 컴퓨터. 이렇게 하면 작업이 과도 한 가상 컴퓨터의 호스트 또는 다른 가상 컴퓨터의 성능을 저하 하는 것을 방지할 수 있습니다. 모니터링 프로세스 과도 한 활동을 포함 하는 가상 컴퓨터를 감지, 가상 컴퓨터 리소스가 더 적게 부여 됩니다. 이 모니터링 및 적용은 기본적으로 해제 되어 있습니다. Windows PowerShell를 사용 하 여 설정 하거나 해제 합니다. 이 설정 하려면이 명령을 실행 합니다.  
  
```  
Set-VMProcessor TestVM -EnableHostResourceProtection $true 
```       

이 cmdlet에 대 한 자세한 참조 [Set-vmprocessor](https://docs.microsoft.com/powershell/module/hyper-v/set-vmprocessor)합니다.

## <a name="BKMK_hot"></a>핫 추가 및 네트워크 어댑터 및 메모리에 대 한 제거 \(새\) 
이제 추가 하거나 발생 시 키 지 가동 중지 시간 없이 가상 컴퓨터가 실행 되는 동안 네트워크 어댑터를 제거할 수 있습니다. 이 Windows 또는 Linux 운영 체제를 실행 하는 2 세대 가상 컴퓨터에 적합 합니다.  
  
또한 동적 메모리를 설정 하지 않은 경우에 실행 되는 동안 가상 컴퓨터에 할당 된 메모리의 양을 조정할 수 있습니다. 이 1 세대와 2 세대 가상 컴퓨터, Windows Server 2016 또는 Windows 10 실행에 대 한 작동 합니다.  
  
## <a name="BKMK_Mgmt"></a>Hyper-v 관리자 향상 \(업데이트\) 
  
-   **대체 자격 증명 지원** -이제 사용할 수 있습니다 다른 자격 증명 집합 Hyper-v 관리자에서 다른 Windows Server 2016 또는 Windows 10 원격 호스트에 연결 합니다. 다시 로그온을 쉽게 수행할 수 있도록 이러한 자격 증명을 저장할 수도 있습니다.  
  
-   **이전 버전 관리** -Hyper-v 관리자와 Windows Server 2016 및 Windows 10에서 Windows Server 2012, Windows 8, Windows Server 2012 R2 및 Windows 8.1에서 Hyper-v를 실행 하는 컴퓨터를 관리할 수 있습니다.  
  
-   **업데이트 관리 프로토콜** -Hyper-v 관리자는 이제 CredSSP, Kerberos 또는 NTLM 인증 허용 되는 WS-MAN 프로토콜을 사용 하 여 원격 Hyper-v 호스트와 통신 합니다. CredSSP를 사용 하 여 원격 Hyper-v 호스트에 연결할 때 Active Directory에서 제한 된 위임을 사용 하지 않고 실시간 마이그레이션을 수행할 수 있습니다. WS MAN 기반 인프라 또한 쉽게 원격 관리를 위한 호스트를 사용할 수 있도록 합니다. WS-MAN은 기본적으로 열리는 포트 80을 통해 연결합니다.  
  
## <a name="BKMK_IS"></a>Integration services Windows Update를 통해 전달 \(업데이트\) 
Windows 게스트에 대 한 통합 서비스에 대 한 업데이트는 Windows Update를 통해 배포 됩니다. 서비스 공급자 및 프라이빗 클라우드 호스터의 경우 가상 머신을 소유한 테넌트에 의해 업데이트 적용 제어 권한을 부여합니다. 테 넌 트가 이제 업데이트할 수 Windows 가상 컴퓨터, 통합 서비스를 비롯 한 모든 업데이트와 단일 메서드를 사용 하 여. Linux 게스트에 대 한 통합 서비스에 대 한 자세한 참조 [Linux 및 FreeBSD 가상 컴퓨터에 Hyper-v](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)합니다.  
  
> [!IMPORTANT]  
> Vmguest.iso 라 하 고 이미지 파일은 더 이상 필요 Windows Server 2016에 Hyper-v에 포함 되지 않습니다.  
  
## <a name="BKMK_linux"></a>Linux Secure Boot \(new\) 
2 세대 가상 컴퓨터에서 실행 되는 Linux 운영 체제 보안 부팅 옵션을 설정한 상태로 이제 부팅할 수 있습니다. Ubuntu 14.04 이상, SUSE Linux Enterprise Server 12 및 이후, Red Hat Enterprise Linux 7.0 이상 및 CentOS 7.0 이상 Windows Server 2016를 실행 하는 호스트에서 보안 부팅에 대 한 활성화 됩니다. 처음으로 가상 컴퓨터를 부팅 하기 전에 Microsoft UEFI 인증 기관을 사용 하 여 가상 컴퓨터를 구성 해야 합니다. Hyper-v 관리자, 가상 컴퓨터 관리자 또는 관리자 권한 Windows Powershell 세션에서이 수행할 수 있습니다. Windows PowerShell이이 명령을 실행 합니다.  
  
```  
Set-VMFirmware TestVM -SecureBootTemplate MicrosoftUEFICertificateAuthority  
```  
  
Hyper-v의 Linux 가상 컴퓨터에 대 한 자세한 내용은 참조 하십시오. [Linux 및 FreeBSD 가상 컴퓨터에 Hyper-v](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)합니다. Cmdlet에 대 한 자세한 내용은 참조 [Set-vmfirmware](https://docs.microsoft.com/powershell/module/hyper-v/set-vmfirmware)합니다.

## <a name="more-memory-and-processors-for-generation-2-virtual-machines-and-hyper-v-hosts-updated"></a>더 많은 메모리와 프로세서 2 세대 가상 컴퓨터 및 Hyper-v 호스트에 대 한 \(업데이트\)
버전 8 이상에서는 2 세대 가상 컴퓨터 훨씬 더 많은 메모리와 가상 프로세서를 사용할 수 있습니다. 호스트도 구성할 수 있습니다 훨씬 더 많은 메모리와 가상 프로세서 지원 하 던 것 보다. 이러한 변경 내용은 전자 상거래 온라인 트랜잭션 처리 (OLTP) 및 데이터 웨어하우징 (DW)에 대 한 큰 메모리 내 데이터베이스를 실행 하는 등 새로운 시나리오를 지원 합니다. Windows Server 블로그 최근 5.5 테라바이트의 4TB 메모리 내 데이터베이스를 실행 하는 128 가상 프로세서 및 메모리와 가상 컴퓨터의 성능 결과 게시 합니다. 성능 실제 서버의 성능의 95% 보다 큽니다. 자세한 내용은 다음을 참조 하십시오. [메모리 내 트랜잭션 처리를 위해 Windows Server 2016 Hyper-v 대규모 VM 성능](https://blogs.technet.microsoft.com/windowsserver/2016/09/28/windows-server-2016-hyper-v-large-scale-vm-performance-for-in-memory-transaction-processing/)합니다. 가상 컴퓨터 버전에 대 한 자세한 참조 [Windows 10 또는 Windows Server 2016에 Hyper-v에서 가상 컴퓨터를 업그레이드 버전](./deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md)합니다. 지원 되는 최대 구성의 전체 목록을 참조 하십시오. [Windows Server 2016의 Hyper-v 확장성에 대 한 계획](./plan/plan-hyper-v-scalability-in-windows-server.md)합니다. 

## <a name="BKMK_nested"></a>중첩 된 가상화 \(새\) 
이 기능을 사용 하 여 Hyper-v 호스트로 가상 컴퓨터를 사용 하 고 해당 가상화 호스트 내에서 가상 컴퓨터를 만들 수 있습니다. 이 개발 및 테스트 환경에 특히 유용할 수 있습니다. 중첩 된 가상화를 사용 하려면 다음이 필요 합니다.  
  
-   이상으로 실행 하려면 Windows Server 2016 또는 Windows 10 실제 Hyper-v 호스트와 가상화 된 호스트에서.  
  
-   Intel VT x (중첩 된 가상화는 Intel 프로세서에 대해서만 사용할 수 있는 지금은)가 포함 된 프로세서입니다.  
  
세부 정보 및 지침을 참조 하세요 [실행-Hyper-v 중첩 된 가상화를 사용 하 여 가상 머신에서](https://docs.microsoft.com/virtualization/hyper-v-on-windows/user-guide/nested-virtualization)합니다.  
  
## <a name="BKMK_networking"></a>네트워킹 기능 \(새\) 
다음과 같은 새로운 네트워킹 기능  
  
-   **원격 직접 메모리 액세스 (RDMA)와 포함 된 팀 (SET) 전환**합니다. 집합은 또한 사용 여부에 관계 없이 Hyper-v 가상 스위치에 바인딩된 네트워크 어댑터에서 RDMA를 설정할 수 있습니다. NIC 팀으로 동일한 기능 중 일부와 가상 스위치를 제공합니다. 자세한 내용은 다음을 참조 하십시오. [원격 직접 메모리 액세스 (RDMA) 및 스위치 포함 된 팀 (SET)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming)합니다.  
  
-   **가상 컴퓨터 다중 큐 (VMMQ)** 합니다. 여러 하드웨어 큐 당 가상 컴퓨터를 할당 하 여 VMQ 처리량을 개선 합니다.  기본 큐는 가상 컴퓨터에 대 한 큐 집합을 되며 큐 간에 분산 되는 트래픽입니다.  
  
-   **서비스 품질 (QoS 소프트웨어 정의 네트워크에 대 한)** 합니다. 기본 클래스 대역폭 내에서 가상 스위치를 통해 트래픽의 기본 클래스를 관리합니다.  
  
새로운 네트워킹 기능에 대 한 자세한 내용은 [네트워킹의 새로운](../../networking/What-s-New-in-Networking.md)합니다.  
  
## <a name="BKMK_check"></a>프로덕션 검사점 \(새\)
프로덕션 검사점은 가상 컴퓨터의 "-시점" 이미지입니다. 이러한 가상 컴퓨터에서 프로덕션 작업 부하를 실행 하는 경우 지원 정책에 부합 하는 검사점을 적용 하는 방법을 제공 합니다. 프로덕션 검사점 저장된 된 상태는 대신 게스트 내 백업 기술을 기반으로 합니다. Windows 가상 컴퓨터 VSS (볼륨 스냅샷 서비스)를 사용합니다. Linux 가상 컴퓨터에 대 한 파일 시스템 버퍼는 파일 시스템으로 일치 하는 검사점을 만드는 플러시됩니다. 대신 저장 된 상태를 기준으로 검사점을 사용 하는 경우 표준 검사점을 대신 선택 합니다. 자세한 내용은 참조 하세요 [Hyper-v에서 표준 또는 프로덕션 검사점 간의 선택](manage/Choose-between-standard-or-production-checkpoints-in-Hyper-V.md)합니다.  
  
> [!IMPORTANT]  
> 새 가상 컴퓨터는 기본적으로 프로덕션 검사점을 사용 합니다.  
  
## <a name="BKMK_HyperVRollingUpgrades"></a>Hyper-v 클러스터 업그레이드 롤링 \(새\) 
이제 Windows Server 2012 r 2를 실행 하는 노드가 포함 된 Windows Server 2016 Hyper-v 클러스터를 실행 하는 노드를 추가할 수 있습니다. 이 옵션을 사용 하면 가동 중지 시간 없이 클러스터를 업그레이드할 수 있습니다. 클러스터의 모든 노드를 업그레이드 하 고 Windows PowerShell cmdlet으로 클러스터 기능 수준을 업데이트 될 때까지 Windows Server 2012 R2 기능 수준에서 실행 되는 클러스터 [업데이트 ClusterFunctionalLevel](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel)합니다.  
  
> [!IMPORTANT]  
> 클러스터 기능 수준을 업데이트 한 후 Windows Server 2012 r 2로 반환할 수 없습니다.  
  
Hyper-v 클러스터의 노드가 포함 된 Windows Server 2012 r 2의 기능 수준으로 실행 중인 Windows Server 2012 R2 및 Windows Server 2016 다음 사항에 유의 합니다.  
  
-   Windows Server 2016 또는 Windows 10을 실행 하는 노드에서 클러스터, Hyper-v 및 가상 컴퓨터를 관리 합니다.  
  
-   모든 Hyper-v 클러스터의 노드 간에 가상 컴퓨터를 이동할 수 있습니다.  
  
-   모든 노드에서 새 Hyper-v 기능을 사용 하려면 Windows Server 2016를 실행 해야 하며 클러스터 기능 수준을 업데이트 해야 합니다.  
  
-   기존 가상 컴퓨터에 대 한 가상 컴퓨터 구성 버전 업그레이드 되지 않습니다. 클러스터 기능 수준을 업그레이드 한 후에 구성 버전을 업그레이드할 수 있습니다.  
  
-   가상 컴퓨터를 만들면 Windows Server 2012 R2 가상 컴퓨터 구성 수준 5와 호환 됩니다.  
  
한 후 클러스터 기능 수준을 업데이트 합니다.  
  
-   새로운 Hyper-v 기능을 사용할 수 있습니다.  
  
-   새 가상 컴퓨터 기능을 사용할 수 있도록 가상 컴퓨터 구성 수준을 수동으로 업데이트 하려면 업데이트 VmConfigurationVersion cmdlet을 사용 합니다. 자세한 내용은 [가상 컴퓨터를 업그레이드 버전](deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md)합니다.    
-   Windows Server 2012 r 2를 실행 하는 Hyper-v 클러스터에 노드를 추가할 수 없습니다.  
  
> [!NOTE]  
> Windows 10에서 Hyper-v 장애 조치 클러스터링을 지원 하지 않습니다.  
  
세부 정보 및 지침에 대 한 참조는 [클러스터 운영 체제 롤링 업그레이드](https://technet.microsoft.com/library/dn850430.aspx)합니다.  

## <a name="BKMK_shared"></a>공유 가상 하드 디스크가 \(업데이트\)
이제 공유 가상 하드 디스크 (.vhdx 파일) 게스트 가동 중지 시간 없이 클러스터링에 사용 되는 크기를 조정할 수 있습니다. 공유 가상 하드 디스크를 증가 또는 가상 컴퓨터가 온라인 상태 이며 축소할 수 있습니다. 게스트 클러스터 이제 보호할 수도 공유 가상 하드 디스크 재해 복구에 대 한 Hyper-v 복제본을 사용 하 여.

컬렉션에서 복제를 활성화 합니다. 가 컬렉션에 대해 복제를 사용 하도록 설정 **WMI 인터페이스를 통해서만 노출**합니다. 에 대 한 설명서를 참조 하세요 [Msvm_CollectionReplicationService 클래스](https://msdn.microsoft.com/library/mt167787%28v=vs.85%29.aspx) 대 한 자세한 내용은 합니다. **PowerShell cmdlet 또는 UI를 통해 컬렉션의 복제를 관리할 수 없습니다.** Vm은 호스트 컬렉션에 관련 된 기능에 액세스 하는 Hyper-v 클러스터의 일부인에 있어야 합니다. 공유 VHD 여기에-독립 실행형 호스트에는 공유 Vhd는 Hyper-v 복제본에서 지원 되지 않습니다.

공유 Vhd에 대 한 지침을 따르세요 [Virtual Hard Disk Sharing Overview](https://technet.microsoft.com/library/dn281956.aspx), 공유 Vhd는 게스트 클러스터에 속해 있는지 확인 합니다. 

공유 VHD가 있지만 없는 연결된 게스트 클러스터를 사용 하 여 컬렉션 (에 관계 없이 공유 VHD에에서 포함 되는지 여부는 참조 지점 만들지 여부) 컬렉션에 대 한 참조 지점을 만들 수 없습니다. 

## <a name="virtual-machine-backupnew"></a>가상 머신 백업\(새\)

(에 관계 없이 호스트는 클러스터 여부)를 단일 가상 머신을 백업 하는 경우 하지는 VM 그룹을 사용 해야 합니다.  나 스냅숏 컬렉션을 사용 해야 합니다. VM 그룹 및 스냅숏 컬렉션은 전적으로 사용 하는 공유 vhdx 게스트 클러스터를 백업에 사용 되는 것입니다. 사용 하 여 스냅숏을 야 하는 대신 합니다 [Hyper-v WMI v2 공급자](https://msdn.microsoft.com/library/windows/desktop/hh850319(v=vs.85).aspx)합니다. 마찬가지로, 사용 하지 마십시오 합니다 [장애 조치 클러스터 WMI 공급자](https://msdn.microsoft.com/library/windows/desktop/mt167750(v=vs.85).aspx)합니다.

## <a name="BKMK_shielded"></a>보호 된 가상 머신을 \(새\)
가상 컴퓨터 사용을 어렵게 하기 위해 Hyper-v 관리자 및 호스트에서 맬웨어 검사, 변조, 또는 실드 된 가상 컴퓨터의 상태에서 데이터를 도용 하는 몇 가지 기능이 차폐 합니다. 데이터 및 상태도 암호화 되어 하 고 Hyper-v 관리자는 비디오 출력 및 디스크를 볼 수 없는 가상 컴퓨터 호스트 보호자 서버에 의해 결정 된 대로 알려진, 정상 호스트 에서만 실행 되도록 제한 될 수 있습니다. 자세한 내용은 다음을 참조 하십시오. [보호 된 패브릭 및 차폐 Vm](../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms.md)합니다.
  
>[!NOTE]  
> 보호 된 가상 컴퓨터는 Hyper-v 복제본과 호환 됩니다. 실드 된 가상 컴퓨터를 복제 하려면 복제 하려는 호스트 차폐 가상 컴퓨터를 실행 권한이 있어야 합니다.  

## <a name="BKMK_StartOrder"></a>클러스터 된 가상 컴퓨터에 대 한 우선 순위 순서를 시작 \(새\)
이 기능을 사용 하면 더 많은 제어를 통해 클러스터 된 가상 컴퓨터의 시작 또는 먼저 다시 시작 합니다. 이렇게 하면 보다 쉽게 이러한 서비스를 사용 하는 가상 컴퓨터 보다 먼저 서비스를 제공 하는 가상 컴퓨터를 시작할 수 있습니다. 집합을 정의 집합에 가상 컴퓨터를 배치 하 고 종속성을 지정 합니다. Windows PowerShell cmdlet을 사용 하 여 관리와 같은 [새로 만들기-ClusterGroupSet](https://docs.microsoft.com/powershell/module/failoverclusters/new-clustergroupset)를 [만들기-ClusterGroupSet](https://docs.microsoft.com/powershell/module/failoverclusters/get-clustergroupset), 및 [ClusterGroupSetDependency 추가](https://docs.microsoft.com/powershell/module/failoverclusters/add-clustergroupsetdependency)합니다.
.  
## <a name="BKMK_QoS"></a>저장소 서비스 품질 (QoS) \(업데이트\)
이제 스케일 아웃 파일 서버에서 저장소 QoS 정책을 만들고 Hyper-V 가상 컴퓨터에서 하나 이상의 가상 디스크에 할당할 수 있습니다. 저장소 로드 변동에 따라 정책을 준수하도록 저장소 성능이 자동으로 재조정됩니다. 자세한 내용은 다음을 참조 하십시오. [저장소 서비스 품질](../../storage/storage-qos/storage-qos-overview.md)합니다.  
  
## <a name="BKMK_Config"></a>가상 머신 구성 파일 형식을 \(업데이트\)
가상 컴퓨터 구성 파일에는 구성 데이터를 보다 효율적으로 읽기 및 쓰기를 수행 하는 새 형식을 사용 합니다. 형식 뿐만 아니라 데이터가 손상 가능성이 더 낮아집니다 저장소 오류가 발생 하면 됩니다. .Vmcx 파일 이름 확장명을 사용 하는 가상 컴퓨터 구성 데이터 파일 및 런타임 상태 데이터 파일.vmrs 파일 이름 확장명을 사용 합니다.  
  
> [!IMPORTANT]  
> .Vmcx 파일 이름 확장명 이진 파일을 나타냅니다. .Vmcx 또는.vmrs 파일 편집이 지원 되지 않습니다.  
  
## <a name="BKMK_ConfgVersion"></a>가상 머신 구성 버전 \(업데이트\)
버전의 Hyper-v 버전과 상태 및 스냅샷 파일을 저장 하는 가상 컴퓨터의 구성의 호환성을 나타냅니다. 버전 5와 가상 컴퓨터는 Windows Server 2012 r 2와 호환 되는 및 Windows Server 2012 R2 및 Windows Server 2016 모두에서 실행할 수 있습니다. Windows Server 2016에 도입 된 버전으로 가상 컴퓨터는 Windows Server 2012 r 2에서 Hyper-v에서 실행 되지 않습니다.   
  
을 이동 하거나 Windows Server 2016에서 Windows Server 2012 r 2에서 Hyper-v를 실행 하는 서버에 가상 컴퓨터를 가져올 가상 컴퓨터의 구성은 자동으로 업데이트 되지 않습니다. 즉, Windows Server 2012 r 2를 실행 하는 서버에 다시 가상 컴퓨터를 이동할 수 있습니다. 그러나 즉, 가상 컴퓨터 구성의 버전을 수동으로 업데이트 될 때까지 새 가상 컴퓨터 기능을 사용할 수 없습니다.  
  
에 대 한 지침은 검사 및 버전 업그레이드를 참조 하십시오. [가상 컴퓨터를 업그레이드 버전](deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md)합니다. 이 문서는 또한 일부 기능이 도입 된 버전을 나열 합니다.   
  
> [!IMPORTANT]  
> -   버전을 업데이트 한 후에 Windows Server 2012 r 2를 실행 하는 서버에 가상 컴퓨터를 이동할 수 없습니다.  
> -   구성 이전 버전으로 다운 그레이드할 수 없습니다.  
> -   합니다 [업데이트 VMVersion](https://docs.microsoft.com/powershell/module/hyper-v/update-vmversion) cmdlet는 클러스터 기능 수준을 Windows Server 2012 R2 경우 Hyper-v 클러스터에서 차단 됩니다.  

## <a name="virtualization-based-security-for-generation-2-virtual-machines-new"></a>2 세대 가상 컴퓨터에 대 한 Virtualization-based 보안 \(새로 만들기)
가상화 기반 보안 장치 가드 맬웨어로부터 악용 으로부터 운영 체제의 향상 된 보호를 제공 하는 가드를 자격 증명 등의 기능을 제공 합니다. 가상화 기반 보안은 버전 8부터 세대 2 게스트 가상 컴퓨터에서 사용할 수 있습니다. 가상 컴퓨터 버전에 대 한 자세한 내용은 참조 [Windows 10 또는 Windows Server 2016에 Hyper-v에서 가상 컴퓨터를 업그레이드 버전](./deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md)합니다.


## <a name="BKMK_Containers"></a>Windows 컨테이너 \(새\) 
Windows 컨테이너 여러 격리 된 응용 프로그램을 한 컴퓨터 시스템에서 실행을 허용 합니다. 신속 하 게 구축 하 고 뛰어나고 휴대용 됩니다. 두 가지 유형의 런타임 컨테이너를 사용할 수는 각각 서로 다른 수준의 응용 프로그램을 격리 합니다. Windows Server 컨테이너 네임 스페이스 및 프로세스 격리를 사용 합니다. Hyper-v 컨테이너는 각 컨테이너에 대 한 간단한 가상 컴퓨터를 사용합니다.  
  
주요 기능은 다음과 같습니다.  
  
-   웹 사이트 및 HTTPS를 사용 하 여 응용 프로그램에 대 한 지원  
  
-   Windows 서버와 Hyper-v 컨테이너 Nano 서버를 호스팅할 수 있습니다.  
  
-   공유 컨테이너 폴더를 통해 데이터를 관리 하는 기능  
  
-   컨테이너 리소스를 제한 하는 기능  
  
빠른 시작 가이드를 비롯 한 정보를 참조 합니다 [Windows 컨테이너 설명서](https://docs.microsoft.com/virtualization/windowscontainers/index)합니다.  
  
## <a name="BKMK_PowerShellDirect"></a>Windows PowerShell Direct \(새\)  
호스트에서 가상 컴퓨터에서 Windows PowerShell 명령을 실행 하는 방법을 제공 합니다. Windows PowerShell 직접 호스트와 가상 컴퓨터 간에 실행 됩니다. 즉, 원격 관리 구성에 관계 없이 작동 하 고 네트워킹 또는 방화벽 요구 사항은 필요 하지 않습니다.  
  
Windows PowerShell 직접은 Hyper-v 호스트에 가상 컴퓨터에 연결 하려면 Hyper-v 관리자를 사용 하는 기존 도구에 대 한 대안입니다.  
  
-   PowerShell 또는 원격 데스크톱 등의 원격 관리 도구  
  
-   Hyper-v 가상 컴퓨터 연결 (VMConnect)  
  
이러한 도구는 잘 작동 하지만 절충할: VMConnect를 신뢰할 수 있지만 자동화 하기 어려울 수 있습니다. 원격 PowerShell은 강력한 반면 하지만를 설정 하 고 유지 관리 하기 어려울 수 있습니다. 이러한 장단점이 Hyper-v 배포 규모가 커짐에 따라 더 중요 될 수 있습니다. Windows PowerShell 직접이 문제를 해결 한 강력한 스크립팅 및 자동화 경험을 제공 하므로 VMConnect를 사용 하 여 처럼 간단 하 게 합니다.   
  
요구 사항 및 지침을 참조 하십시오. [Windows 관리 가상 컴퓨터에 PowerShell 직접](manage/Manage-Windows-virtual-machines-with-PowerShell-Direct.md)합니다.  
