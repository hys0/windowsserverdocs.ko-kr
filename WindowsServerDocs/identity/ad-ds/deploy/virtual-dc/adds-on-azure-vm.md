---
title: Azure 가상 컴퓨터에 Active Directory Domain Services 설치
description: Azure 가상 컴퓨터에서 VM (가상 컴퓨터)에 새 Active Directory 포리스트를 만드는 방법
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 04/11/2019
ms.technology: identity-adds
ms.topic: article
ms.prod: windows-server
ms.openlocfilehash: e0a10e27e044fd1df7cbdb943964440983ce494c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390653"
---
# <a name="install-a-new-active-directory-forest-using-azure-cli"></a>Azure CLI를 사용 하 여 새 Active Directory 포리스트 설치

AD DS는 여러 온-프레미스 인스턴스에서 실행 되는 것과 동일한 방식으로 Azure VM (가상 머신)에서 실행할 수 있습니다. 이 문서에서는 Azure Portal 및 Azure CLI를 사용 하 여 Azure 가용성 집합에서 두 개의 새 도메인 컨트롤러에 새 AD DS 포리스트를 배포 하는 과정을 안내 합니다. 많은 고객이 Azure에서 도메인 컨트롤러 배포를 준비 하거나 랩을 만들 때이 지침을 유용 하 게 사용할 수 있습니다.

## <a name="components"></a>구성 요소

* 모든 항목을 저장할 리소스 그룹입니다.
* Vm에 대 한 RDP 액세스를 허용 하는 [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview.md), 서브넷, 네트워크 보안 그룹 및 규칙
* 에 두 개의 Active Directory Domain Services (AD DS) 도메인 컨트롤러를 배치 하도록 설정 된 Azure 가상 컴퓨터 [가용성](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability#availability-sets) .
* AD DS 및 DNS를 실행 하는 두 개의 Azure 가상 머신

### <a name="items-that-are-not-covered"></a>검사 되지 않은 항목

* 온-프레미스 위치에서 [사이트 간 VPN 연결 만들기](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [Azure에서 네트워크 트래픽 보안](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices.md)
* [사이트 토폴로지 디자인](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/designing-the-site-topology)
* [작업 마스터 역할 배치 계획](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/planning-operations-master-role-placement)
* [Azure AD에 id를 동기화 하는 Azure AD Connect 배포](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-express)

## <a name="build-the-test-environment"></a>테스트 환경 빌드

[Azure Portal](https://portal.azure.com) 및 [Azure CLI](https://docs.microsoft.com/cli/azure/overview?view=azure-cli-latest) 를 사용 하 여 환경을 만듭니다.

Azure CLI는 명령줄 또는 스크립트에서 Azure 리소스를 만들고 관리 하는 데 사용 됩니다. 이 자습서에서는 Azure CLI 사용 하 여 Windows Server 2019를 실행 하는 가상 머신을 배포 하는 방법을 자세히 설명 합니다. 배포가 완료 되 면 서버에 연결 하 고 AD DS를 설치 합니다.

Azure 구독이 없는 경우 시작 하기 전에 [무료 계정을 만듭니다](https://azure.microsoft.com/free) .

### <a name="using-azure-cli"></a>Azure CLI 사용

다음 스크립트는 Azure에서 새로운 Active Directory 포리스트에 대해 도메인 컨트롤러를 빌드하기 위해 두 개의 Windows Server 2019 Vm을 빌드하는 프로세스를 자동화 합니다. 관리자는 필요에 따라 아래 변수를 수정 하 여 한 번의 작업으로 완료할 수 있습니다. 이 스크립트는 원격 데스크톱, 가상 네트워크 및 서브넷 및 가용성 그룹에 대 한 트래픽 규칙을 사용 하 여 필요한 리소스 그룹, 네트워크 보안 그룹을 만듭니다. Vm은 각각에 대해 캐싱을 사용 하지 않도록 설정 된 20gb의 데이터 디스크를 사용 하 여 작성 된 후 AD DS에 설치 됩니다.

아래 스크립트는 Azure Portal에서 직접 실행할 수 있습니다. CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 빠른 시작에서 Azure CLI 버전 2.0.4 이상을 실행해야 합니다. `az --version`을 실행하여 버전을 찾습니다. 설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)를 참조하세요.

| 변수 이름 | 용도 |
| :---: | :--- |
| adminUsername | 각 VM에서 로컬 관리자로 구성할 사용자 이름입니다. |
| adminPassword | 각 VM에서 로컬 관리자 암호로 구성할 일반 텍스트 암호입니다. |
| resourceGroupName | 리소스 그룹에 사용할 이름입니다. 기존 이름을 복제 하면 안 됩니다. |
| 위치 | 배포 하려는 Azure location name입니다. @No__t-0을 사용 하 여 현재 구독에 대해 지원 되는 영역을 나열 합니다. |
| VNetName | Azure 가상 네트워크를 할당 하는 이름은 기존 이름을 중복 하면 안 됩니다. |
| VNetAddress | Azure 네트워킹에 사용할 IP 범위입니다. 기존 범위를 복제 하면 안 됩니다. |
| subnetName | IP 서브넷을 할당 하는 이름입니다. 기존 이름을 복제 하면 안 됩니다. |
| SubnetAddress | 도메인 컨트롤러의 서브넷 주소입니다. 는 VNet 내부의 서브넷 이어야 합니다. |
| 가용성 집합 | 도메인 컨트롤러 Vm이 가입할 가용성 집합의 이름입니다. |
| VMSize | 배포 위치에서 사용할 수 있는 표준 Azure VM 크기입니다. |
| DataDiskSize | AD DS 설치 되는 데이터 디스크의 크기 (GB)입니다. |
| DomainController1 | 첫 번째 도메인 컨트롤러의 이름입니다. |
| DC1IP | 첫 번째 도메인 컨트롤러의 IP 주소입니다. |
| DomainController2 | 두 번째 도메인 컨트롤러의 이름입니다. |
| DC2IP | 두 번째 도메인 컨트롤러의 IP 주소입니다. |

```azurecli
#Update based on your organizational requirements
Location=westus2
ResourceGroupName=ADonAzureVMs
NetworkSecurityGroup=NSG-DomainControllers
VNetName=VNet-AzureVMsWestUS2
VNetAddress=10.10.0.0/16
SubnetName=Subnet-AzureDCsWestUS2
SubnetAddress=10.10.10.0/24
AvailabilitySet=DomainControllers
VMSize=Standard_DS1_v2
DataDiskSize=20
AdminUsername=azureuser
AdminPassword=ChangeMe123456
DomainController1=AZDC01
DC1IP=10.10.10.11
DomainController2=AZDC02
DC2IP=10.10.10.12

# Create a resource group.
az group create --name $ResourceGroupName \
                --location $Location

# Create a network security group
az network nsg create --name $NetworkSecurityGroup \
                      --resource-group $ResourceGroupName \
                      --location $Location

# Create a network security group rule for port 3389.
az network nsg rule create --name PermitRDP \
                           --nsg-name $NetworkSecurityGroup \
                           --priority 1000 \
                           --resource-group $ResourceGroupName \
                           --access Allow \
                           --source-address-prefixes "*" \
                           --source-port-ranges "*" \
                           --direction Inbound \
                           --destination-port-ranges 3389

# Create a virtual network.
az network vnet create --name $VNetName \
                       --resource-group $ResourceGroupName \
                       --address-prefixes $VNetAddress \
                       --location $Location \

# Create a subnet
az network vnet subnet create --address-prefix $SubnetAddress \
                              --name $SubnetName \
                              --resource-group $ResourceGroupName \
                              --vnet-name $VNetName \
                              --network-security-group $NetworkSecurityGroup

# Create an availability set.
az vm availability-set create --name $AvailabilitySet \
                              --resource-group $ResourceGroupName \
                              --location $Location

# Create two virtual machines.
az vm create \
    --resource-group $ResourceGroupName \
    --availability-set $AvailabilitySet \
    --name $DomainController1 \
    --size $VMSize \
    --image Win2019Datacenter \
    --admin-username $AdminUsername \
    --admin-password $AdminPassword \
    --data-disk-sizes-gb $DataDiskSize \
    --data-disk-caching None \
    --nsg $NetworkSecurityGroup \
    --private-ip-address $DC1IP \
    --no-wait

az vm create \
    --resource-group $ResourceGroupName \
    --availability-set $AvailabilitySet \
    --name $DomainController2 \
    --size $VMSize \
    --image Win2019Datacenter \
    --admin-username $AdminUsername \
    --admin-password $AdminPassword \
    --data-disk-sizes-gb $DataDiskSize \
    --data-disk-caching None \
    --nsg $NetworkSecurityGroup \
    --private-ip-address $DC2IP

```

## <a name="dns-and-active-directory"></a>DNS 및 Active Directory

이 프로세스의 일부로 만든 Azure 가상 머신이 기존 온-프레미스 Active Directory 인프라의 확장이 되는 경우 배포 전에 온-프레미스 DNS 서버를 포함 하도록 가상 네트워크의 DNS 설정을 변경 해야 합니다. 이 단계는 Azure에서 새로 만든 도메인 컨트롤러가 온-프레미스 리소스를 확인 하 고 복제가 수행 될 수 있도록 허용 하는 데 중요 합니다. DNS, Azure 및 설정을 구성 하는 방법에 대 한 자세한 내용은 [자체 dns 서버를 사용 하는 이름 확인](https://docs.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances#name-resolution-that-uses-your-own-dns-server)섹션에서 찾을 수 있습니다.

Azure에서 새 도메인 컨트롤러의 수준을 올린 후에는 가상 네트워크에 대 한 기본 및 보조 DNS 서버로 설정 해야 하며, 모든 온-프레미스 DNS 서버는 3 차 이상으로 강등 됩니다. DNS 서버를 변경 하는 방법에 대 한 자세한 내용은 [가상 네트워크 만들기, 변경 또는 삭제](https://docs.microsoft.com/azure/virtual-network/manage-virtual-network#change-dns-servers)문서에서 찾을 수 있습니다.

온-프레미스 네트워크를 Azure로 확장 하는 방법에 대 한 정보는 사이트 간 VPN 연결 만들기 @ no__t-1 @no__t 문서에서 찾을 수 있습니다.

## <a name="configure-the-vms-and-install-active-directory-domain-services"></a>Vm을 구성 하 고 Active Directory Domain Services를 설치 합니다.

스크립트가 완료 되 면 [Azure Portal](https://portal.azure.com)찾은 다음 **Virtual machines**로 이동 합니다.

### <a name="configure-the-first-domain-controller"></a>첫 번째 도메인 컨트롤러 구성

스크립트에서 제공한 자격 증명을 사용 하 여 AZDC01에 연결 합니다.

* 데이터 디스크를 초기화 하 여 F로 포맷 합니다.
   * 시작 메뉴를 열고 **컴퓨터 관리** 로 이동 합니다.
   * **저장소** > **디스크 관리** 로 이동 합니다.
   * 디스크를 MBR로 초기화
   * 새 단순 볼륨을 만들고 드라이브 문자 F를 할당 합니다. 원하는 경우 볼륨 레이블을 제공할 수 있습니다.
* 서버 관리자를 사용 하 여 Active Directory Domain Services 설치
* 새 포리스트의 첫 번째 도메인 컨트롤러로 도메인 컨트롤러 수준 올리기
   * 도메인 컨트롤러 옵션 페이지에서 DNS (Domain Name System) 서버 및 GC (글로벌 카탈로그)를 선택 된 상태로 둡니다.
   * 조직의 요구 사항에 따라 디렉터리 서비스 복원 모드 암호를 지정 합니다.
   * C:에서 위치를 묻는 메시지가 표시 될 때 만든 F: 드라이브를 가리키도록 경로를 변경 합니다.
   * 마법사에서 선택한 내용을 검토 하 고 **다음** 을 선택 합니다.

> [!NOTE]
> 필수 구성 요소 확인은 실제 네트워크 어댑터에 고정 IP 주소가 할당 되지 않았다는 경고를 표시 합니다. 고정 IP가 Azure 가상 네트워크에 할당 되 면이를 안전 하 게 무시할 수 있습니다.

* **설치** 선택

마법사가 설치 프로세스를 완료 하면 VM이 다시 부팅 됩니다.

VM이 다시 부팅 되 면 사용 된 자격 증명을 사용 하 여 다시 부팅 되 고 이번에는 만든 도메인의 구성원이 됩니다.

   > [!NOTE]
   > 도메인 컨트롤러를 승격 한 후 첫 번째 로그온은 평소 보다 오래 걸릴 수 있으며이는 정상입니다. Tea, 커피, 물 또는 기타 음료를 선택 합니다.

[Azure virtual network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-faq#do-vnets-support-ipv6) 는 i p v 6을 지원 하지 않으므로 i p v 6을 통해 IPv4를 사용 하도록 vm을 설정 하는 것이 좋습니다. 이 작업을 완료 하는 방법에 대 한 자세한 내용은 기술 자료 문서 [Windows에서 고급 사용자를 위한](https://support.microsoft.com/help/929852/guidance-for-configuring-ipv6-in-windows-for-advanced-users)i p v 6을 구성 하기 위한 지침을 참조 하세요.

### <a name="configure-the-second-domain-controller"></a>두 번째 도메인 컨트롤러 구성

스크립트에서 제공한 자격 증명을 사용 하 여 AZDC02에 연결 합니다.

* 데이터 디스크를 초기화 하 여 F로 포맷 합니다.
   * 시작 메뉴를 열고 **컴퓨터 관리** 로 이동 합니다.
   * **저장소** > **디스크 관리** 로 이동 합니다.
   * 디스크를 MBR로 초기화
   * 새 단순 볼륨을 만들고 드라이브 문자 F를 할당 합니다. 원하는 경우 볼륨 레이블을 제공할 수 있습니다.
* 서버 관리자를 사용 하 여 Active Directory Domain Services 설치
* 도메인 컨트롤러 수준 올리기
   * 기존 도메인에 도메인 컨트롤러 추가-CONTOSO.com
   * 작업을 수행 하는 자격 증명을 제공 합니다.
   * C:에서 위치를 묻는 메시지가 표시 될 때 만든 F: 드라이브를 가리키도록 경로를 변경 합니다.
   * 도메인 컨트롤러 옵션 페이지에서 DNS (Domain Name System) 서버 및 GC (글로벌 카탈로그)가 선택 되어 있는지 확인 합니다.
   * 조직의 요구 사항에 따라 디렉터리 서비스 복원 모드 암호를 지정 합니다.
   * 마법사에서 선택한 내용을 검토 하 고 **다음** 을 선택 합니다.

> [!NOTE]
> 필수 구성 요소 확인은 실제 네트워크 어댑터에 고정 IP 주소가 할당 되지 않았다는 경고를 표시 합니다. 고정 IP가 Azure 가상 네트워크에 할당 되 면이를 안전 하 게 무시할 수 있습니다.

* **설치** 선택

마법사가 설치 프로세스를 완료 하면 VM이 다시 부팅 됩니다.

VM에서 사용 되는 자격 증명을 사용 하 여 로그 뒤로 다시 부팅 하는 경우이 시간은 CONTOSO.com 도메인의 구성원으로 다시 부팅 됩니다.

[Azure virtual network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-faq#do-vnets-support-ipv6) 는 i p v 6을 지원 하지 않으므로 i p v 6을 통해 IPv4를 사용 하도록 vm을 설정 하는 것이 좋습니다. 이 작업을 완료 하는 방법에 대 한 자세한 내용은 기술 자료 문서 [Windows에서 고급 사용자를 위한](https://support.microsoft.com/help/929852/guidance-for-configuring-ipv6-in-windows-for-advanced-users)i p v 6을 구성 하기 위한 지침을 참조 하세요.

### <a name="configure-dns"></a>DNS 구성

Azure에서 새 도메인 컨트롤러의 수준을 올린 후에는 가상 네트워크에 대 한 기본 및 보조 DNS 서버를 설정 해야 하 고, 온-프레미스 DNS 서버는 3 차 이상으로 수준이 내려갑니다. DNS 서버를 변경 하는 방법에 대 한 자세한 내용은 [가상 네트워크 만들기, 변경 또는 삭제](https://docs.microsoft.com/azure/virtual-network/manage-virtual-network#change-dns-servers)문서에서 찾을 수 있습니다.

### <a name="wrap-up"></a>위로 래핑

이 시점에서 환경에는 하나의 도메인 컨트롤러와 추가 서버가 환경에 추가 될 수 있도록 Azure virtual network를 구성 했습니다. 사이트 및 서비스 구성과 같은 Active Directory Domain Services에 대 한 사후 설치 작업, 감사, 백업 및 기본 제공 관리자 계정의 보안을 지금 완료 해야 합니다.

## <a name="removing-the-environment"></a>환경 제거

테스트를 완료 했을 때 환경을 제거 하려면 위에서 만든 리소스 그룹을 삭제할 수 있습니다 .이 단계에서는 해당 리소스 그룹에 속하는 모든 구성 요소를 제거 합니다.

### <a name="remove-using-the-azure-portal"></a>Azure Portal 사용 하 여 제거

Azure Portal에서 **리소스 그룹** 으로 이동 하 고,이 예제 ADonAzureVMs에서 만든 리소스 그룹을 선택한 다음, **리소스 그룹 삭제**를 선택 합니다. 이 프로세스는 리소스 그룹 내에 포함 된 모든 리소스를 삭제 하기 전에 확인 메시지를 표시 합니다.

### <a name="remove-using-the-azure-cli"></a>Azure CLI 사용 하 여 제거

Azure CLI에서 다음 명령을 실행 합니다.

```azurecli
az group delete --name ADonAzureVMs
```

## <a name="next-steps"></a>다음 단계

* [안전 하 게 가상화 Active Directory Domain Services (AD DS)](../../Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md)
* [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-express)
* [백업 및 복구](https://docs.microsoft.com/azure/virtual-machines/windows/backup-recovery)
* [사이트 간 VPN 연결](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)
* [감시](https://docs.microsoft.com/azure/virtual-machines/windows/monitor)
* [보안 및 정책](https://docs.microsoft.com/azure/virtual-machines/windows/security-policy)
* [유지 관리 및 업데이트](https://docs.microsoft.com/azure/virtual-machines/windows/maintenance-and-updates)
