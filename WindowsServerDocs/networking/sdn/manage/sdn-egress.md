---
title: 가상 네트워크의 송신 계량
description: 클라우드 네트워킹 수익 화의 기본 측면은 네트워크 대역폭 송신입니다. 예를 들어 Microsoft Azure 비즈니스 모델의 아웃 바운드 데이터 전송입니다. 아웃 바운드 데이터는 지정 된 청구 주기 동안 인터넷을 통해 Azure 데이터 센터에서 나가는 총 데이터 양을 기준으로 요금이 부과 됩니다.
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.author: anpaul
author: AnirbanPaul
ms.date: 10/02/2018
ms.openlocfilehash: a5d530d5cd1b42206bd6881ee902496713573793
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854436"
---
# <a name="egress-metering-in-a-virtual-network"></a>가상 네트워크의 송신 계량

>적용 대상: Windows Server 2019


클라우드 네트워킹 수익 화의 기본 측면은 네트워크 대역폭 사용률을 기준으로 청구 될 수 있습니다. 아웃 바운드 데이터는 지정 된 청구 주기 동안 인터넷을 통해 데이터 센터에서 나가는 총 데이터 양을 기준으로 요금이 부과 됩니다.

Windows Server 2019에서 SDN 네트워크 트래픽에 대 한 송신 계량을 통해 아웃 바운드 데이터 전송에 대 한 사용 요금을 제공할 수 있습니다. 각 가상 네트워크는 그대로 유지 되지만 데이터 센터 내에 유지 되는 네트워크 트래픽은 별도로 추적할 수 있으므로 청구 계산에서 제외할 수 있습니다. 청구 되지 않은 주소 범위 중 하나에 포함 되지 않은 대상 IP 주소에 바인딩된 패킷은 청구 되는 아웃 바운드 데이터 전송으로 추적 됩니다.

## <a name="virtual-network-unbilled-address-ranges-whitelist-of-ip-ranges"></a>가상 네트워크 청구 되지 않은 주소 범위 (IP 범위의 허용 목록)

기존 가상 네트워크의 **UnbilledAddressRanges** 속성에서 청구 되지 않은 주소 범위를 찾을 수 있습니다. 기본적으로 주소 범위는 추가 되지 않습니다.

   ```PowerShell
   import-module NetworkController
   $uri = "https://sdn.contoso.com"

   (Get-NetworkControllerVirtualNetwork -ConnectionURI $URI -ResourceId "VNet1").properties
   ```

출력은 다음과 유사 하 게 표시 됩니다.
   ```
    AddressSpace           : Microsoft.Windows.NetworkController.AddressSpace
    DhcpOptions            :
    UnbilledAddressRanges  :
    ConfigurationState     :
    ProvisioningState      : Succeeded
    Subnets                : {21e71701-9f59-4ee5-b798-2a9d8c2762f0, 5f4758ef-9f96-40ca-a389-35c414e996cc,
                         29fe67b8-6f7b-486c-973b-8b9b987ec8b3}
    VirtualNetworkPeerings :
    EncryptionCredential   :
    LogicalNetwork         : Microsoft.Windows.NetworkController.LogicalNetwork
   ```


## <a name="example-manage-the-unbilled-address-ranges-of-a-virtual-network"></a>예: 가상 네트워크의 청구 되지 않은 주소 범위 관리

가상 네트워크의 **UnbilledAddressRange** 속성을 설정 하 여 청구 된 송신 계량에서 제외할 IP 서브넷 접두사 집합을 관리할 수 있습니다.  접두사 중 하 나와 일치 하는 대상 IP 주소를 사용 하 여 가상 네트워크의 네트워크 인터페이스에서 보낸 트래픽은 BilledEgressBytes 속성에 포함 되지 않습니다.

1.  액세스 요금이 청구 되지 않는 서브넷을 포함 하도록 **UnbilledAddressRanges** 속성을 업데이트 합니다.

    ```PowerShell
    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceID "VNet1"
    $vnet.Properties.UnbilledAddressRanges = "10.10.2.0/24,10.10.3.0/24"
    ```

    >[!TIP]
    >여러 IP 서브넷을 추가 하는 경우 각 IP 서브넷 사이에 쉼표를 사용 합니다.  쉼표 앞 이나 뒤에 공백을 넣지 마십시오.

2.  수정 된 **UnbilledAddressRanges** 속성을 사용 하 여 Virtual Network 리소스를 업데이트 합니다.

    ```PowerShell
    New-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "VNet1" -Properties $unbilled.Properties -PassInnerException
    ```

    출력은 다음과 유사 하 게 표시 됩니다.
      ```
         Confirm
         Performing the operation 'New-NetworkControllerVirtualNetwork' on entities of type
         'Microsoft.Windows.NetworkController.VirtualNetwork' via
         'https://sdn.contoso.com/networking/v3/virtualNetworks/VNet1'. Are you sure you want to continue?
         [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y


         Tags             :
         ResourceRef      : /virtualNetworks/VNet1
         InstanceId       : 29654b0b-9091-4bed-ab01-e172225dc02d
         Etag             : W/"6970d0a3-3444-41d7-bbe4-36327968d853"
         ResourceMetadata :
         ResourceId       : VNet1
         Properties       : Microsoft.Windows.NetworkController.VirtualNetworkProperties
      ```


3. Virtual Network를 확인 하 여 구성 된 **UnbilledAddressRanges**를 확인 합니다.

   ```PowerShell
   (Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceID "VNet1").properties
   ```

   이제 출력이 다음과 같이 표시 됩니다.
   ```
   AddressSpace           : Microsoft.Windows.NetworkController.AddressSpace
   DhcpOptions            :
   UnbilledAddressRanges  : 10.10.2.0/24,192.168.2.0/24
   ConfigurationState     :
   ProvisioningState      : Succeeded
   Subnets                : {21e71701-9f59-4ee5-b798-2a9d8c2762f0, 5f4758ef-9f96-40ca-a389-35c414e996cc,
                        29fe67b8-6f7b-486c-973b-8b9b987ec8b3}
   VirtualNetworkPeerings :
   EncryptionCredential   :
   LogicalNetwork         : Microsoft.Windows.NetworkController.LogicalNetwork
   ```

## <a name="check-the-billed-the-unbilled-egress-usage-of-a-virtual-network"></a>가상 네트워크의 청구 되지 않은 송신 사용량을 확인 합니다.

**UnbilledAddressRanges** 속성을 구성한 후에는 가상 네트워크 내에서 각 서브넷의 청구 및 청구 되지 않은 송신 사용을 확인할 수 있습니다. 송신 트래픽은 4 분 마다 청구 되 고 청구 되지 않은 범위의 총 바이트 수로 업데이트 됩니다.

각 가상 서브넷에 사용할 수 있는 속성은 다음과 같습니다.

-   **UnbilledEgressBytes** 에는이 가상 서브넷에 연결 된 네트워크 인터페이스에서 보낸 청구 되지 않은 바이트 수가 표시 됩니다. 청구 되지 않은 바이트는 부모 가상 네트워크의 **UnbilledAddressRanges** 속성에 포함 된 주소 범위에 전송 된 바이트입니다.

-   **BilledEgressBytes** 에는이 가상 서브넷에 연결 된 네트워크 인터페이스에서 보낸 청구 된 바이트 수가 표시 됩니다. 청구 된 바이트는 부모 가상 네트워크의 **UnbilledAddressRanges** 속성에 포함 되지 않은 주소 범위로 전송 된 바이트입니다.

다음 예제를 사용 하 여 송신 사용을 쿼리할 수 있습니다.

```PowerShell
(Get-NetworkControllerVirtualNetwork -ConnectionURI $URI -ResourceId "VNet1").properties.subnets.properties | ft AddressPrefix,BilledEgressBytes,UnbilledEgressBytes
```

출력은 다음과 유사 하 게 표시 됩니다.
```
AddressPrefix BilledEgressBytes UnbilledEgressBytes
------------- ----------------- -------------------
10.0.255.8/29          16827067                   0
10.0.2.0/24           781733019                   0
10.0.4.0/24                   0                   0
```


---
