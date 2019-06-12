---
title: 보호된 VM - 호스팅 서비스 공급자가 Microsoft Azure 팩 설정
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: d528c689-58b0-425c-9740-25e2553ed689
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 156832087bc7af0c95a92cab9a0c1501264d47a5
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447500"
---
# <a name="shielded-vms---hosting-service-provider-sets-up-windows-azure-pack"></a>보호된 VM - 호스팅 서비스 공급자가 Microsoft Azure 팩 설정

이 설명 하는 방법을 통해 호스팅 서비스 공급자를 테 넌 트가 보호 된 Vm을 배포 하는 데 사용할 수 있도록 Windows Azure 팩을 구성할 수 있습니다. Windows Azure 팩 웹 포털의 System Center Virtual Machine Manager 테 넌 트 간단한 웹 인터페이스를 통해 자신의 Vm을 배포 및 관리할 수 있도록 기능을 확장 하는 경우 Windows Azure Pack 완벽 하 게 보호 된 Vm을 지원 및 테 넌 트가 보호 데이터 파일을 만들고도 쉬워졌습니다.

이 항목에서는 보호 된 Vm을 배포 하는 전체 과정에 얼마나 적합 한지 이해 하려면 [호스팅 서비스 공급자 구성 단계에 대 한 보호 된 호스트 및 차폐 Vm](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)합니다.

## <a name="setting-up-windows-azure-pack"></a>Windows Azure 팩 설정

환경에서 Windows Azure 팩을 설정 하려면 다음 작업을 완료 됩니다.

1. System Center 2016-Virtual Machine Manager (VMM) 호스팅 패브릭에 대 한 구성을 완료 합니다. 여기에 VM 템플릿 및 Windows Azure Pack을 통해 공개 되는 VM 클라우드를 설정 합니다.

    [시나리오-보호 된 호스트 및 VMM에서 보호 된 가상 컴퓨터 배포](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-overview)

2. 설치 하 고 System Center 2016-Service Provider Foundation (SPF)를 구성 합니다. 이 소프트웨어에 Windows Azure 팩에 VMM 서버와 통신할 수 있습니다.

    [Service Provider Foundation-SPF 배포](https://technet.microsoft.com/system-center-docs/spf/deploy/deploy-spf)

3. Windows Azure 팩을 설치 하 고 SPF를 사용 하 여 통신 하도록 구성 합니다.

    - [Windows Azure Pack 설치](#install-windows-azure-pack) (이 항목에서)
    - [Windows Azure pack](#configure-windows-azure-pack) (이 항목에서)

4. 테 넌 트 VM 클라우드를 액세스할 수 있도록 Windows Azure 팩에서 하나 이상의 호스팅 계획을 만듭니다.

    [Windows Azure Pack에서 계획을 만들어](#create-a-plan-in-windows-azure-pack) (이 항목에서)

## <a name="install-windows-azure-pack"></a>설치할 Windows Azure 팩

설치 하 고 테 넌 트의 웹 포털을 호스트 하려는 컴퓨터에서 Windows Azure Pack (WAP)을 구성 합니다. SPF 서버에 연결 되며 테 넌 트에 연결할 수 있으려면이 컴퓨터를 해야 합니다.

1.  검토 [WAP 시스템 요구 사항](https://technet.microsoft.com/library/dn296442.aspx) 하 고 설치 합니다 [필수 구성 요소 소프트웨어](https://technet.microsoft.com/library/dn469335.aspx)합니다.

2.  다운로드 및 설치 합니다 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)합니다. 컴퓨터가 인터넷에 연결 되어 있지 않으면를 수행 합니다 [오프 라인 설치 지침](http://www.iis.net/learn/install/web-platform-installer/web-platform-installer-v4-command-line-webpicmdexe-rtw-release)합니다.

3.  웹 플랫폼 설치 관리자를 열고 찾습니다 **Windows Azure Pack: 포털 및 API Express** 아래의 합니다 **제품** 탭 합니다. 클릭 **추가**, 한 다음 **설치** 창의 맨 아래에 있습니다.

4.  설치를 계속합니다. 설치가 완료 되 면 구성 사이트 (*https://&lt;wapserver&gt;: 30101 /* ) 웹 브라우저에서 열립니다. 이 웹 사이트에서 SQL server에 대 한 정보를 제공 하 고 WAP 구성을 완료 합니다.

Windows Azure pack 도움말 설정을 참조 하세요 [Windows Azure Pack의 express 배포 설치](https://technet.microsoft.com/dn296439.aspx)합니다.

> [!NOTE]
> 이미 Windows Azure 팩 환경에서 실행 하면 기존 설치를 사용할 수 있습니다. 보호 된 VM 기능을 최신 작동 하려면 최소 설치를 업그레이드 해야 하는 반면, 업데이트 롤업 10입니다.

### <a name="configure-windows-azure-pack"></a>구성 Windows Azure 팩

Windows Azure Pack을 사용 하기 전에 이미 있어야 설치 하 고 인프라에 대해 구성 합니다.

1.  Windows Azure Pack 관리 포털에서 이동할 *https://&lt;wapserver&gt;: 30091*, 그런 다음 관리자 자격 증명을 사용 하 여 로그인 합니다.

2.  왼쪽된 창에서 클릭 **VM 클라우드**합니다.

3.  클릭 하 여 Windows Azure Pack의 Service Provider Foundation 인스턴스에 연결할 **System Center Service Provider Foundation 등록**합니다. Service Provider Foundation에 대 한 URL 뿐만 아니라 사용자 이름 및 암호를 지정 해야 합니다.

    ![System Center Service Provider Foundation 등록](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-01-register-spf.png)

4.  완료 되 면 VMM 환경에서 설정 하는 VM 클라우드를 표시 해야 합니다. 하나 이상의 VM 클라우드를 지 원하는 보호 된 Vm WAP를 사용할 수 있는 계속 하기 전에 확인 합니다.

### <a name="create-a-plan-in-windows-azure-pack"></a>Windows Azure Pack에서 계획 만들기

WAP의 Vm을 만들려면 테 넌 트를 허용 하려면 먼저 테 넌 트가 구독할 수 있는 호스팅 계획을 만들어야 합니다. 테 넌 트에 대 한 허용 된 VM 클라우드, 템플릿, 네트워크 및 청구 엔터티를 정의 하는 계획 합니다.

1. 포털의 아래쪽 창에서 클릭 **+ 새로 만들기** &gt; **계획** &gt; **계획 만들기**합니다.

2. 마법사의 첫 번째 단계에서 계획의 이름을 선택 합니다. 구독할 때 테 넌 트 표시 이름입니다.

3. 두 번째 단계에서 선택 **가상 머신 클라우드** 계획에서 제공 하는 서비스 중 하 나와 있습니다.

4. 계획에 대 한 모든 추가 기능을 선택 하는 방법에 대 한 단계를 건너뜁니다.

5. 클릭 **확인** 계획을 만들려면 (확인 표시). 계획을 만들지만이 것 아직 구성 된 상태에서입니다.

   ![계획에서 Windows Azure 팩](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-02-create-plan.png)

6. 계획을 구성 하려면 해당 이름을 클릭 합니다.

7. 다음 페이지에서 아래 **서비스 계획**, 클릭 **가상 머신 클라우드**합니다. 이 계획에 대 한 할당량을 구성할 수 있는 페이지가 열립니다.

8. 아래 **기본**, VMM 관리 서버 및 테 넌 트에 제공 하려는 가상 컴퓨터 클라우드를 선택 합니다. 사용 하 여 보호 된 Vm을 제공할 수 있는 클라우드가 표시 됩니다 **(지원 되는 실딩)** 해당 이름 옆에 있는 합니다.

9. 이 계획에 적용 하려는 할당량을 선택 합니다. (예를 들어 제한 CPU 코어 및 RAM 사용). 유지 해야 합니다 **허용 Virtual Machines를 보호** 확인란을 선택 합니다.

   ![Windows Azure Pack에서 가상 컴퓨터 클라우드에 대 한 설정](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-03-virtual-machine-clouds.png)
    
10. 섹션까지 아래로 스크롤합니다 **템플릿**를 선택한 다음 하나 이상의 템플릿이 테 넌 트에 제공 합니다. 모두 보호 하 고 테 넌 트 VM 및 해당 암호의 무결성에 대 한 종단 간 보증을 제공 하려면 테 넌 트에 차폐 되지 않은 템플릿은 있지만 보호 된 템플릿을 제공 해야 합니다를 제공할 수 있습니다.

11. 에 **네트워크** 섹션, 테 넌 트에 대 한 하나 이상의 네트워크를 추가 합니다.

12. 계획에 대 한 설정 또는 할당량을 설정한 후 클릭 **저장** 맨 아래에 있습니다.

13. 화면 왼쪽 상단을 보면, 다시 이동 하 고 화살표를 클릭 합니다 **계획** 페이지입니다.

14. 화면 아래쪽에서 계획을 변경 **사설** 하 **공용** 테 넌 트가 계획을 구독할 수 있도록 합니다.

    ![Windows Azure Pack의 계획에 대 한 액세스를 변경 합니다.](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-04-change-access.png)

    이 시점에서 Windows Azure Pack 구성 되 고 테 넌 트를 방금 만든 계획을 구독 하 고 보호 된 Vm을 배포할 수 있게 됩니다. 테 넌 트를 완료 해야 하는 추가 단계를 참조 하세요 [테 넌 트-Windows Azure Pack을 사용 하 여 보호 된 VM을 배포에 대 한 보호 된 Vm](guarded-fabric-shielded-vm-windows-azure-pack.md)합니다.

## <a name="see-also"></a>참조

- [보호 된 호스트 및 차폐 Vm 호스팅 서비스 공급자 구성 단계](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [보호된 패브릭 및 보호된 VM](guarded-fabric-and-shielded-vms-top-node.md)
