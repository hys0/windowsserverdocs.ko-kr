---
title: 가상 네트워크의 송신 계량
description: 클라우드 네트워킹 수익의 근본적인 측면은 네트워크 대역폭 송신 합니다. 예를 들어 아웃 바운드 데이터는 Microsoft Azure의 비즈니스 모델을 전송합니다. 아웃 바운드 데이터에 지정된 된 청구 주기 동안 인터넷을 통해 Azure 데이터 센터 밖으로 이동 하는 데이터의 총 금액에 따라 요금이 청구 됩니다.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.date: 10/02/2018
ms.openlocfilehash: 50aee16b0b5797f28ebcdf61494b09669699873f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446324"
---
# <a name="egress-metering-in-a-virtual-network"></a>가상 네트워크의 송신 계량

>적용 대상: Windows Server 2019


클라우드 네트워킹 수익의 근본적인 측면 네트워크 대역폭 사용량의 비용을 청구할 수 있다는 것입니다. 아웃 바운드 데이터에 지정된 된 청구 주기 동안 인터넷을 통해 데이터 센터 외부로 이동 하는 데이터의 총 금액에 따라 요금이 청구 됩니다.

Windows Server 2019에서 SDN 네트워크 트래픽에 대 한 송신 계량 아웃 바운드 데이터 전송 사용량 미터를 제공할 수가 있습니다. 데이터 센터 내에 유지 하지만 각 가상 네트워크를 해제 하는 네트워크 트래픽을 수에서 개별적으로 추적 하므로 청구 요금 계산에서 제외할 수 있습니다. 아웃 바운드 데이터 전송 요금이 청구 명세서가 표시 됩니다 주소 범위 중 하나에 포함 되지 않은 대상 IP 주소에 대 한 바운드 패킷은 추적 됩니다.

## <a name="virtual-network-unbilled-address-ranges-whitelist-of-ip-ranges"></a>미 청구 되는 가상 네트워크 주소 범위 (화이트 리스트 IP 범위)

미 청구 주소 범위에서 찾을 수 있습니다 합니다 **UnbilledAddressRanges** 기존 가상 네트워크의 속성입니다. 기본적으로 추가 주소 범위 없음 있습니다.

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


## <a name="example-manage-the-unbilled-address-ranges-of-a-virtual-network"></a>예: 미 청구 주소 범위는 가상 네트워크 관리

설정 하 여 계량 청구 송신에서 제외할 IP 서브넷 접두사의 집합을 관리할 수 있습니다 합니다 **UnbilledAddressRange** 가상 네트워크의 속성입니다.  접두사 중 하 나와 일치 하는 대상 IP 주소를 사용 하 여 가상 네트워크에서 네트워크 인터페이스에서 보낸 트래픽은 모두 BilledEgressBytes 속성에 포함 되지 않습니다.

1.  업데이트를 **UnbilledAddressRanges** 액세스에 대 한 요금이 청구 되지 것입니다는 서브넷을 포함 하는 속성입니다.

    ```PowerShell
    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceID "VNet1"
    $vnet.Properties.UnbilledAddressRanges = "10.10.2.0/24,10.10.3.0/24"
    ```

    >[!TIP]
    >여러 IP 서브넷을 추가 하는 경우 각 IP 서브넷 사이 쉼표를 사용 합니다.  전이나 쉼표 뒤에 공백을 포함 하지 않습니다.

2.  수정 된 가상 네트워크 리소스를 업데이트할 **UnbilledAddressRanges** 속성입니다.

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


~~~
Tags             :
ResourceRef      : /virtualNetworks/VNet1
InstanceId       : 29654b0b-9091-4bed-ab01-e172225dc02d
Etag             : W/"6970d0a3-3444-41d7-bbe4-36327968d853"
ResourceMetadata :
ResourceId       : VNet1
Properties       : Microsoft.Windows.NetworkController.VirtualNetworkProperties
```
~~~


3. Check the Virtual Network to see the configured **UnbilledAddressRanges**.

   ```PowerShell
   (Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceID "VNet1").properties
   ```

   Your output will now look similar to this:
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

## Check the billed the unbilled egress usage of a virtual network

After you configure the **UnbilledAddressRanges** property, you can check the billed and unbilled egress usage of each subnet within a virtual network. Egress traffic updates every four minutes with the total bytes of the billed and unbilled ranges.

The following properties are available for each virtual subnet:

-   **UnbilledEgressBytes** shows the number of unbilled bytes sent by network interfaces connected to this virtual subnet. Unbilled bytes are bytes sent to address ranges that are part of the **UnbilledAddressRanges** property of the parent virtual network.

-   **BilledEgressBytes** shows Number of billed bytes sent by network interfaces connected to this virtual subnet. Billed bytes are bytes sent to address ranges that are not part of the **UnbilledAddressRanges** property of the parent virtual network.

Use the following example to query egress usage:

```PowerShell
(Get-NetworkControllerVirtualNetwork -ConnectionURI $URI -ResourceId "VNet1").properties.subnets.properties | ft AddressPrefix,BilledEgressBytes,UnbilledEgressBytes
```

Your output will look similar to this:
```
AddressPrefix BilledEgressBytes UnbilledEgressBytes
------------- ----------------- -------------------
10.0.255.8/29          16827067                   0
10.0.2.0/24           781733019                   0
10.0.4.0/24                   0                   0
```


---