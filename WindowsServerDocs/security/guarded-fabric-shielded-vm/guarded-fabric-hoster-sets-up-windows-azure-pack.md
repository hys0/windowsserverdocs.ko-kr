---
title: 보호 된 Vm-호스팅 서비스 공급자 Windows Azure 팩 설정
ms.prod: windows-server
ms.topic: article
ms.assetid: d528c689-58b0-425c-9740-25e2553ed689
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 4632c218f0638885e3094446704a91c442859d4c
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473970"
---
# <a name="shielded-vms---hosting-service-provider-sets-up-windows-azure-pack"></a>보호 된 Vm-호스팅 서비스 공급자 Windows Azure 팩 설정

이 항목에서는 테 넌 트가 보호 된 Vm을 배포 하는 데 사용할 수 있도록 호스팅 서비스 공급자가 Windows Azure 팩를 구성 하는 방법을 설명 합니다. Windows Azure 팩은 테 넌 트가 간단한 웹 인터페이스를 통해 자체 Vm을 배포 하 고 관리할 수 있도록 System Center Virtual Machine Manager의 기능을 확장 하는 웹 포털입니다. Windows Azure 팩는 보호 된 Vm을 완벽 하 게 지원 하 고 테 넌 트가 해당 보호 데이터 파일을 훨씬 더 쉽게 만들고 관리할 수 있게 해줍니다.

이 항목이 보호 된 Vm을 배포 하는 전체 프로세스에 어떻게 부합 하는지 이해 하려면 [보호 된 호스트 및 보호 된 vm에 대 한 서비스 공급자 구성 단계 호스팅](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)을 참조 하세요.

## <a name="setting-up-windows-azure-pack"></a>Windows Azure 팩 설정

사용자 환경에 Windows Azure 팩을 설정 하려면 다음 작업을 완료 합니다.

1. 호스팅 패브릭에 대 한 System Center 2016-Virtual Machine Manager (VMM)의 구성을 완료 합니다. 여기에는 VM 템플릿 및 VM 클라우드 설정이 포함 되며 Windows Azure 팩를 통해 노출 됩니다.

    [시나리오 - VMM에서 보호된 호스트 및 보호된 가상 컴퓨터 배포](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-overview)

2. SPF (System Center 2016-Service Provider Foundation)를 설치 하 고 구성 합니다. 이 소프트웨어를 통해 Windows Azure 팩 VMM 서버와 통신할 수 있습니다.

    [Service Provider Foundation 배포-SPF](https://technet.microsoft.com/system-center-docs/spf/deploy/deploy-spf)

3. Windows Azure 팩를 설치 하 고 SPF와 통신 하도록 구성 합니다.

    - [Windows Azure 팩 설치](#install-windows-azure-pack) (이 항목)
    - [Windows Azure 팩 구성](#configure-windows-azure-pack) (이 항목)

4. VM 클라우드에 대 한 테 넌 트 액세스를 허용 하도록 Windows Azure 팩에서 하나 이상의 호스팅 계획을 만듭니다.

    [Windows Azure 팩에서 계획 만들기](#create-a-plan-in-windows-azure-pack) (이 항목)

## <a name="install-windows-azure-pack"></a>Windows Azure 팩 설치

테 넌 트 용 웹 포털을 호스트 하려는 컴퓨터에 WAP (Windows Azure 팩)를 설치 하 고 구성 합니다. 이 컴퓨터는 SPF 서버에 연결할 수 있어야 하 고 테 넌 트가 연결할 수 있어야 합니다.

1.  [WAP 시스템 요구 사항을](https://technet.microsoft.com/library/dn296442.aspx) 검토 하 고 [필수 구성 요소 소프트웨어](https://technet.microsoft.com/library/dn469335.aspx)를 설치 합니다.

2.  [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)를 다운로드 하 여 설치 합니다. 컴퓨터가 인터넷에 연결 되어 있지 않은 경우 [오프 라인 설치 지침](https://www.iis.net/learn/install/web-platform-installer/web-platform-installer-v4-command-line-webpicmdexe-rtw-release)을 따르세요.

3.  웹 플랫폼 설치 관리자를 열고 **제품** 탭 아래에서 **Windows Azure 팩: 포털 및 API Express** 를 찾습니다. **추가**를 클릭 한 다음 창 맨 아래에서 **설치** 를 클릭 합니다.

4.  설치를 계속합니다. 설치가 완료 되 면 구성 사이트 (*https:// &lt; wapserver &gt; : 30101/*)가 웹 브라우저에서 열립니다. 이 웹 사이트에서 SQL server에 대 한 정보를 제공 하 고 WAP 구성을 완료 합니다.

Windows Azure 팩 설정에 대 한 도움말은 [Windows Azure 팩 express 배포 설치](https://technet.microsoft.com/dn296439.aspx)를 참조 하세요.

> [!NOTE]
> 사용자 환경에서 이미 Windows Azure 팩를 실행 하는 경우 기존 설치를 사용할 수 있습니다. 그러나 최신 차폐 VM 기능을 사용 하려면 설치를 업데이트 롤업 10 이상으로 업그레이드 해야 합니다.

### <a name="configure-windows-azure-pack"></a>Windows Azure 팩 구성

Windows Azure 팩를 사용 하기 전에 인프라에 대해를 이미 설치 하 고 구성 해야 합니다.

1.  *Https:// &lt; wapserver &gt; : 30091*에서 Windows Azure 팩 관리 포털로 이동한 후 관리자 자격 증명을 사용 하 여 로그인 합니다.

2.  왼쪽 창에서 **VM 클라우드**를 클릭 합니다.

3.  **System Center Service Provider Foundation 등록**을 클릭 하 여 Service Provider Foundation 인스턴스에 Windows Azure 팩 연결 합니다. Service Provider Foundation에 대 한 URL과 사용자 이름 및 암호를 지정 해야 합니다.

    ![System Center Service Provider Foundation 등록](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-01-register-spf.png)

4.  완료 되 면 VMM 환경에서 설정 된 VM 클라우드를 볼 수 있습니다. 계속 하기 전에 WAP에서 사용할 수 있는 보호 된 Vm을 지 원하는 VM 클라우드가 하나 이상 있는지 확인 하세요.

### <a name="create-a-plan-in-windows-azure-pack"></a>Windows Azure 팩에서 계획 만들기

테 넌 트가 WAP에서 Vm을 만들 수 있도록 하려면 먼저 테 넌 트가 구독할 수 있는 호스팅 계획을 만들어야 합니다. 계획은 테 넌 트에 대해 허용 되는 VM 클라우드, 템플릿, 네트워크 및 청구 엔터티를 정의 합니다.

1. 포털의 아래쪽 창에서 **+ 새로** &gt; **PLAN** &gt; **만들기 계획 만들기 계획**을 클릭 합니다.

2. 마법사의 첫 번째 단계에서 계획의 이름을 선택 합니다. 구독할 때 테 넌 트에 표시 되는 이름입니다.

3. 두 번째 단계에서는 계획에 제공할 서비스 중 하나로 **가상 머신 클라우드** 를 선택 합니다.

4. 계획에 대 한 추가 기능을 선택 하는 단계를 건너뜁니다.

5. **확인** (확인 표시)을 클릭 하 여 계획을 만듭니다. 이는 계획을 만들지만 아직 구성 된 상태가 아닙니다.

   ![Windows Azure 팩의 계획](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-02-create-plan.png)

6. 계획 구성을 시작 하려면 해당 이름을 클릭 합니다.

7. 다음 페이지의 **계획 서비스**에서 **가상 컴퓨터 클라우드**를 클릭 합니다. 그러면이 계획에 대 한 할당량을 구성할 수 있는 페이지가 열립니다.

8. **기본**에서 테 넌 트에 제공 하려는 VMM 관리 서버 및 가상 컴퓨터 클라우드를 선택 합니다. 보호 된 Vm을 제공할 수 있는 클라우드는 이름 옆에 **(차폐 지원)** 와 함께 표시 됩니다.

9. 이 계획에서 적용 하려는 할당량을 선택 합니다. (예: CPU 코어 및 RAM 사용에 대 한 제한). **Virtual Machines 보호** 가능 확인란을 선택 된 상태로 두어야 합니다.

   ![Windows Azure 팩의 가상 컴퓨터 클라우드에 대 한 설정](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-03-virtual-machine-clouds.png)

10. **템플릿**섹션까지 아래로 스크롤한 다음 테 넌 트에 제공할 하나 이상의 템플릿을 선택 합니다. 테 넌 트에 차폐 템플릿 및 보호 되지 않는 템플릿을 둘 다 제공할 수 있지만 테 넌 트의 무결성과 VM의 비밀에 대 한 종단 간 보증을 제공 하기 위해 차폐 템플릿을 제공 해야 합니다.

11. **네트워크** 섹션에서 테 넌 트에 대해 하나 이상의 네트워크를 추가 합니다.

12. 계획에 대 한 다른 설정 또는 할당량을 설정한 후 아래쪽의 **저장** 을 클릭 합니다.

13. 화면 왼쪽 위에서 화살표를 클릭 하 여 **계획** 페이지로 돌아갑니다.

14. 화면 맨 아래에서 테 넌 트가 계획을 구독할 수 있도록 계획을 **비공개** 에서 **Public** 으로 변경 합니다.

    ![Windows Azure 팩의 계획에 대 한 액세스 변경](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-04-change-access.png)

    이 시점에서 Windows Azure 팩 구성 되 고 테 넌 트가 방금 만든 계획을 구독 하 고 보호 된 Vm을 배포할 수 있습니다. 테 넌 트가 완료 해야 하는 추가 단계는 [테 넌 트에 대 한 보호 된 vm-Windows Azure 팩를 사용 하 여 보호 된 Vm 배포](guarded-fabric-shielded-vm-windows-azure-pack.md)를 참조 하세요.

## <a name="additional-references"></a>추가 참조

- [보호 된 호스트 및 보호 된 Vm에 대 한 호스팅 서비스 공급자 구성 단계](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [보호된 패브릭 및 보호된 VM](guarded-fabric-and-shielded-vms-top-node.md)
