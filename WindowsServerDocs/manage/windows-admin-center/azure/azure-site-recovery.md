---
title: Azure Site Recovery 및 Windows Admin Center 사용 하 여 Hyper-v 가상 머신 보호
description: Windows Admin Center(Project Honolulu)를 사용하여 Azure Site Recovery로 Hyper-V VM을 보호합니다.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 07/17/2018
ms.localizationpriority: low
ms.prod: windows-server-threshold
ms.openlocfilehash: 66e9b2e23a60d1e4725321e88fc1ac262b9c31fa
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445917"
---
# <a name="protect-your-hyper-v-virtual-machines-with-azure-site-recovery-and-windows-admin-center"></a>Azure Site Recovery 및 Windows Admin Center 사용 하 여 Hyper-v 가상 머신 보호

>적용 대상: Windows Admin Center Windows Admin Center 미리 보기

[Azure Windows Admin Center 통합에 대해 알아봅니다.](../plan/azure-integration-options.md)

Windows Admin Center는 Hyper-V 서버 또는 클러스터에 가상 컴퓨터를 복제하는 프로세스를 간소화하여 자체 데이터 센터에서 Azure의 기능을 보다 쉽게 활용할 수 있도록 만듭니다. 설치를 자동화하기 위해 Windows Admin Center 게이트웨이를 Azure에 연결할 수 있습니다.

복제 설정을 구성하고 Azure Portal 내에서 복구 계획을 만들어 Windows Admin Center가 VM 복제를 시작하여 VM을 보호하도록 하려면 다음 정보를 사용합니다.

## <a name="what-is-azure-site-recovery-and-how-does-it-work-with-windows-admin-center"></a>Azure Site Recovery란 무엇이며 Windows Admin Center와 함께 어떻게 작동합니까? 

**Azure Site Recovery**는 재해가 발생하는 경우 업무에 중요한 인프라를 보호할 수 있도록 VM에서 실행되는 워크로드를 복제하는 Azure 서비스입니다.  [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)에 대해 자세히 알아보세요.

Azure Site Recovery는 **복제** 및 **장애 조치**의 두 구성 요소로 이루어져 있습니다. 복제 부분은 재해가 발생하는 경우 Azure 저장소 계정에 대상 VM의 VHD를 복제하여 VM을 보호합니다. 그러면 사용자는 이러한 VM 장애 조치를 수행하고 재해 발생 시 Azure에서 실행합니다. Azure의 복구 프로세스를 테스트하려면 기본 VM에 영향을 주지 않고 테스트 장애 조치를 수행할 수도 있습니다.

복제 구성 요소에 대한 설정을 완료하는 것만으로 재해의 경우에 VM을 보호하기에 충분합니다. 그러나 장애 조치 부분을 구성할 때까지 Azure에서 VM을 시작할 수 없습니다. Azure VM에 대해 장애 조치 수행하고자 할 때 장애 조치 부분을 설정할 수 있습니다. 초기 설정 부분에서 필수가 아닙니다. 호스트 서버가 다운되고 아직 장애 조치 구성 요소를 구성하지 않은 경우 해당 시간에 구성할 수 있으며 보호된 VM의 워크로드에 액세스할 수 있습니다. 그러나 재해가 발생하기 전에 장애 조치를 구성하는 것은 좋은 방법입니다.
 

## <a name="prerequisites-and-planning"></a>필수 구성 요소 및 계획

- 보호하려는 VM을 호스팅하는 대상 서버에는 Azure에 복제하기 위해 인터넷에 액세스가 필요합니다.
- [해당 Windows Admin Center 게이트웨이를 Azure에 연결](azure-integration.md)합니다.
- [성공적인 복제 및 장애 조치에 대한 요구 사항을 평가하는 용량 계획 도구를 검토](https://docs.microsoft.com/azure/site-recovery/hyper-v-site-walkthrough-capacity)합니다.

## <a name="step-1-set-up-vm-protection-on-your-target-host"></a>1단계: 대상 호스트에서 VM 보호 설정

> [!NOTE] 
> 보호에 대한 대상 VM을 포함하는 호스트 서버 또는 클러스터별로 이 단계를 수행해야 합니다.

1. 보호할 VM을 호스팅하는 서버 또는 클러스터로 이동합니다(서버 관리자 또는 하이퍼 컨버지드 클러스터 관리자로).
2. **가상 컴퓨터** > **인벤토리**로 이동합니다.
3. 임의의 VM을 선택합니다(보호하려는 VM일 필요는 없습니다).
4. **자세히** > **VM 보호 설정**을 선택합니다.
5. Azure 계정에 로그인합니다.
6. 필요한 정보를 입력합니다.

   - **구독:** 이 호스트에서 Vm의 복제에 사용 하려는 Azure 구독입니다.
   - **위치:** Azure 지역 ASR 리소스를 만들어야 합니다.
   - **저장소 계정:** 이 호스트에서 복제 된 VM 워크 로드를 저장할 저장소 계정입니다.
   - **Vault:** 이 호스트에서 보호 된 Vm에 대 한 Azure Site Recovery 자격 증명 모음의 이름을 선택 합니다.

7. **ASR 설정**을 선택합니다.
8. 알림이 표시 될 때까지 기다립니다. **Site Recovery 설정 완료**합니다.
 
최대 10분이 걸릴 수 있습니다. **알림**(오른쪽 맨 위쪽 종 아이콘)으로 이동하여 진행 상황을 볼 수 있습니다.

>[!NOTE]
> (클러스터에서 구성하는 경우)이 단계는 자동으로 대상 서버 또는 노드에 ASR 에이전트를 설치하고, 지정된 **위치**에 **저장소 계정** 및 **서버 클러스터**이 지정된 **리소스 그룹**을 만듭니다. 또한 ASR 서비스로 대상 호스트를 등록하고 기본 복제 정책을 구성합니다.

## <a name="step-2-select-virtual-machines-to-protect"></a>2단계: 보호할 가상 컴퓨터를 선택 합니다.

1. 위의 2단계에서 구성한 서버 또는 클러스터로 다시 돌아가 **가상 컴퓨터 > 인벤토리**로 이동합니다.
2. 보호하려는 VM을 선택합니다.
3. **자세히** > **VM 보호**를 선택합니다.
4. [VM을 보호하기 위한 용량 요구 사항](https://docs.microsoft.com/azure/site-recovery/site-recovery-capacity-planner)을 검토합니다.

    프리미엄 저장소 계정을 사용하려면 [Azure Portal에서 만들어야](https://docs.microsoft.com/azure/storage/common/storage-premium-storage) 합니다. Windows Admin Center 창에 제공된 **새로 만들기** 옵션은 표준 저장소 계정을 만듭니다.

5. 이 VM 복제를 위해 사용할 **저장소 계정** 이름을 입력하고 **VM 보호**를 선택합니다. 이 단계에서 선택한 가상 컴퓨터를 복제할 수 있습니다. 

6. ASR에서 복제를 시작합니다. 복제가 완료되고 **가상 컴퓨터 인벤토리** 표에서 **보호됨** 열의 값을 **예**로 변경하는 경우 VM이 보호됩니다. 이 작업은 몇 분 정도 걸릴 수 있습니다.  

## <a name="step-3-configure-and-run-a-test-failover-in-the-azure-portal"></a>3단계: 구성 및 Azure portal에서 테스트 장애 조치 실행

 VM 복제를 시작할 때 이 단계를 완료하지 않아도 되지만(VM은 이미 방금의 복제로 인해 보호될 것임) Azure Site Recovery를 설정할 때 장애 조치 설정을 구성하는 것이 좋습니다. Azure VM에 대한 장애 조치를 준비하려는 경우 다음 단계를 완료합니다.

1. [Azure 네트워크 설정](https://docs.microsoft.com/azure/site-recovery/hyper-v-site-walkthrough-prepare-azure) 장애 조치 VM이 이 VNET에 연결됩니다. 연결된 페이지에 나열된 다른 단계는 Windows Admin Center에 의해 자동으로 완료됩니다. Azure 네트워크만 설정하면 됩니다.

2. [테스트 장애 조치를 수행](https://docs.microsoft.com/azure/site-recovery/hyper-v-site-walkthrough-test-failover)합니다.

## <a name="step-4-create-recovery-plans"></a>4단계: 복구 계획 만들기

**복구 계획**은 장애 조치를 수행하고 VM의 컬렉션을 구성하는 전체 응용 프로그램을 복구할 수 있는 Azure Site Recovery의 기능입니다. 응용 프로그램을 구성하는 VM을 복구 계획에 추가하여 보호된 VM을 개별적으로 복구할 수 있지만 복구 계획을 통해 전체 응용 프로그램의 장애 조치를 수행할 수 있습니다. 응용 프로그램의 복구를 테스트하려면 복구 계획의 테스트 장애 조치 기능을 사용할 수도 있습니다. 복구 계획을 사용하면 VM을 그룹화하고, 장애 조치 동안 가져와야 하는 순서를 시퀀싱하고, 복구 프로세스의 일부로 수행할 추가 단계를 자동화할 수 있습니다. VM을 보호하고 있는 경우 Azure Portal에서 Azure Site Recovery로 이동하고 이 VM에 대한 복구 계획을 만들 수 있습니다. [복구 계획에 대해 자세히 알아보세요](https://docs.microsoft.com/azure/site-recovery/site-recovery-create-recovery-plans).

## <a name="monitoring-replicated-vms-in-azure"></a>Azure의 복제된 VM 모니터링 ##

서버 등록에서 오류가 없는지 확인하려면 **Azure Portal** > **모든 리소스** > **복구 서비스 자격 증명 모음**(2단계에서 지정) > **작업** > **사이트 복구 작업**으로 이동합니다.

**복구 서비스 자격 증명 모음** > **복제된 항목**으로 이동하여 VM 복제를 모니터링할 수 있습니다.

자격 증명 모음에 등록된 모든 서버를 보려면 **복구 서비스 자격 증명 모음** > **사이트 복구 인프라** > **Hyper-V 호스트**(Hyper-V 사이트 섹션 아래)로 이동합니다.

## <a name="known-issue"></a>알려진 문제 ##

클러스터로 ASR을 등록할 때 노드가 ASR 설치 또는 ASR 서비스 등록에 실패하는 경우 VM은 보호되지 않을 수 있습니다. **복구 서비스 자격 증명 모음** > **작업** > **사이트 복구 작업**으로 이동하여 Azure Portal에 등록된 클러스터의 모든 노드를 확인합니다.