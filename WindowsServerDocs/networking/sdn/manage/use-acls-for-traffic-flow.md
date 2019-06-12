---
title: 관리 데이터 센터 네트워크 트래픽 흐름을 사용 하 여 액세스 제어 목록 (Acl)
description: 이 항목에서는 액세스 제어 목록 (Acl) 데이터 트래픽 흐름 데이터 센터 방화벽 및 Acl을 사용 하 여 가상 서브넷 관리를 구성 하는 방법을 알아봅니다. 사용 하도록 설정 하 고이 정보를 가상 서브넷 또는 네트워크 인터페이스에 적용 하는 Acl을 만들어 데이터 센터 방화벽을 구성 합니다.
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a7ac5af-85e9-4440-a631-6a3a38e9015d
ms.author: pashort
author: shortpatti
ms.date: 08/27/2018
ms.openlocfilehash: 7bfb74e0964735d357226ab1e5af826796c48d81
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446306"
---
# <a name="use-access-control-lists-acls-to-manage-datacenter-network-traffic-flow"></a>관리 데이터 센터 네트워크 트래픽 흐름을 사용 하 여 액세스 제어 목록 (Acl)

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 액세스 제어 목록 (Acl) 데이터 트래픽 흐름 데이터 센터 방화벽 및 Acl을 사용 하 여 가상 서브넷 관리를 구성 하는 방법을 알아봅니다. 사용 하도록 설정 하 고이 정보를 가상 서브넷 또는 네트워크 인터페이스에 적용 하는 Acl을 만들어 데이터 센터 방화벽을 구성 합니다.   

이 항목의 다음 예제에서는 이러한 Acl을 만들려면 Windows PowerShell을 사용 하는 방법을 보여 줍니다.  

## <a name="configure-datacenter-firewall-to-allow-all-traffic"></a>모든 트래픽을 허용 하도록 데이터 센터 방화벽 구성  

SDN을 배포 하면 기본 네트워크 연결을 위한 새로운 환경에서 테스트 해야 합니다.  이를 위해 제한 없이 모든 네트워크 트래픽을 허용 하는 데이터 센터 방화벽에 대 한 규칙을 만듭니다.   

다음 표에서 항목을 사용 하 여 모든 인바운드 및 아웃 바운드 네트워크 트래픽을 허용 하는 규칙 집합을 만듭니다.


| 원본 IP | 대상 IP | Protocol | 원본 포트 | 대상 포트 | Direction | 작업 | Priority |
|:---------:|:--------------:|:--------:|:-----------:|:----------------:|:---------:|:------:|:--------:|
|    \*     |       \*       |   All    |     \*      |        \*        |  인바운드  | 허용  |   100    |
|    \*     |       \*       |   All    |     \*      |        \*        | 아웃바운드  | 허용  |   110    |

---       

### <a name="example-create-an-acl"></a>예: ACL을 만들어 
이 예제에서는 두 개의 규칙을 사용 하 여 ACL을 만듭니다.

1. **AllowAll_Inbound** -모든 네트워크 트래픽이이 ACL 구성 되어 있는 네트워크 인터페이스에 전달 되도록 허용 합니다.    
2. **AllowAllOutbound** -모든 트래픽이 네트워크 인터페이스에서 전달 되도록 허용 합니다. 리소스 id "AllowAll-1"로 식별 되는이 ACL을 가상 서브넷 및 네트워크 인터페이스에서 사용할 준비가 되었습니다.  

다음 예제 스크립트에서 내보낸 Windows PowerShell 명령을 사용 하 여 **NetworkController** 모듈을이 ACL을 만들 합니다.  


```PowerShell
$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Allow"  
$ruleproperties.SourceAddressPrefix = "*"  
$ruleproperties.DestinationAddressPrefix = "*"  
$ruleproperties.Priority = "100"  
$ruleproperties.Type = "Inbound"  
$ruleproperties.Logging = "Enabled"  
$aclrule1 = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule1.Properties = $ruleproperties  
$aclrule1.ResourceId = "AllowAll_Inbound"  
$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Allow"  
$ruleproperties.SourceAddressPrefix = "*"  
$ruleproperties.DestinationAddressPrefix = "*"  
$ruleproperties.Priority = "110"  
$ruleproperties.Type = "Outbound"  
$ruleproperties.Logging = "Enabled"  
$aclrule2 = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule2.Properties = $ruleproperties  
$aclrule2.ResourceId = "AllowAll_Outbound"  
$acllistproperties = new-object Microsoft.Windows.NetworkController.AccessControlListProperties  
$acllistproperties.AclRules = @($aclrule1, $aclrule2)  
New-NetworkControllerAccessControlList -ResourceId "AllowAll" -Properties $acllistproperties -ConnectionUri <NC REST FQDN>  
```  

>[!NOTE]  
>네트워크 컨트롤러에 대 한 Windows PowerShell 명령 참조 항목에 위치한 [네트워크 컨트롤러 Cmdlet](https://technet.microsoft.com/library/mt576401.aspx)합니다.  

## <a name="use-acls-to-limit-traffic-on-a-subnet"></a>서브넷에서 트래픽을 제한 하기 위해 Acl을 사용 합니다.  
이 예제에서는 서로 통신에서 192.168.0.0/24 서브넷 내에서 Vm을 방지 하는 ACL을 만들 수 있습니다. 이 유형의 ACL 서브넷 내 서브넷 외부에서 요청을 받을 뿐만 아니라 다른 서브넷에 있는 다른 서비스와 통신 하는 Vm을 계속 하면서 가로로 분포에 공격자의 능력을 제한 하기 위해 유용 합니다.   


|   원본 IP    | 대상 IP | Protocol | 원본 포트 | 대상 포트 | Direction | 작업 | Priority |
|:--------------:|:--------------:|:--------:|:-----------:|:----------------:|:---------:|:------:|:--------:|
|  192.168.0.1   |       \*       |   All    |     \*      |        \*        |  인바운드  | 허용  |   100    |
|       \*       |  192.168.0.1   |   All    |     \*      |        \*        | 아웃바운드  | 허용  |   101    |
| 192.168.0.0/24 |       \*       |   All    |     \*      |        \*        |  인바운드  | 차단  |   102    |
|       \*       | 192.168.0.0/24 |   All    |     \*      |        \*        | 아웃바운드  | 차단  |   103    |
|       \*       |       \*       |   All    |     \*      |        \*        |  인바운드  | 허용  |   104    |
|       \*       |       \*       |   All    |     \*      |        \*        | 아웃바운드  | 허용  |   105    |

--- 

리소스 id로 식별 된 ACL 아래의 예제 스크립트로 만든 **서브넷-192-168-0-0**, 이제 "192.168.0.0/24" 서브넷 주소를 사용 하는 가상 네트워크 서브넷에 적용할 수 있습니다.  자동으로 해당 가상 네트워크 서브넷에 연결 된 모든 네트워크 인터페이스는 적용 된 위의 ACL 규칙을 가져옵니다.  

다음은 Windows Powershell 명령을 사용 하 여 네트워크 컨트롤러 REST API를 사용 하 여이 ACL을 만드는 예제 스크립트입니다.  

```PowerShell  
import-module networkcontroller  
$ncURI = "https://mync.contoso.local"  
$aclrules = @()  

$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Allow"  
$ruleproperties.SourceAddressPrefix = "192.168.0.1"  
$ruleproperties.DestinationAddressPrefix = "*"  
$ruleproperties.Priority = "100"  
$ruleproperties.Type = "Inbound"  
$ruleproperties.Logging = "Enabled"  

$aclrule = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule.Properties = $ruleproperties  
$aclrule.ResourceId = "AllowRouter_Inbound"  
$aclrules += $aclrule  

$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Allow"  
$ruleproperties.SourceAddressPrefix = "*"  
$ruleproperties.DestinationAddressPrefix = "192.168.0.1"  
$ruleproperties.Priority = "101"  
$ruleproperties.Type = "Outbound"  
$ruleproperties.Logging = "Enabled"  

$aclrule = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule.Properties = $ruleproperties  
$aclrule.ResourceId = "AllowRouter_Outbound"  
$aclrules += $aclrule  

$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Deny"  
$ruleproperties.SourceAddressPrefix = "192.168.0.0/24"  
$ruleproperties.DestinationAddressPrefix = "*"  
$ruleproperties.Priority = "102"  
$ruleproperties.Type = "Inbound"  
$ruleproperties.Logging = "Enabled"  

$aclrule = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule.Properties = $ruleproperties  
$aclrule.ResourceId = "DenySubnet_Inbound"  
$aclrules += $aclrule  

$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Deny"  
$ruleproperties.SourceAddressPrefix = "*"  
$ruleproperties.DestinationAddressPrefix = "192.168.0.0/24"  
$ruleproperties.Priority = "103"  
$ruleproperties.Type = "Outbound"  
$ruleproperties.Logging = "Enabled"  

$aclrule = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule.Properties = $ruleproperties  
$aclrule.ResourceId = "DenySubnet_Outbound"  

$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Allow"  
$ruleproperties.SourceAddressPrefix = "*"  
$ruleproperties.DestinationAddressPrefix = "*"  
$ruleproperties.Priority = "104"  
$ruleproperties.Type = "Inbound"  
$ruleproperties.Logging = "Enabled"  

$aclrule = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule.Properties = $ruleproperties  
$aclrule.ResourceId = "AllowAll_Inbound"  
$aclrules += $aclrule  

$ruleproperties = new-object Microsoft.Windows.NetworkController.AclRuleProperties  
$ruleproperties.Protocol = "All"  
$ruleproperties.SourcePortRange = "0-65535"  
$ruleproperties.DestinationPortRange = "0-65535"  
$ruleproperties.Action = "Allow"  
$ruleproperties.SourceAddressPrefix = "*"  
$ruleproperties.DestinationAddressPrefix = "*"  
$ruleproperties.Priority = "105"  
$ruleproperties.Type = "Outbound"  
$ruleproperties.Logging = "Enabled"  

$aclrule = new-object Microsoft.Windows.NetworkController.AclRule  
$aclrule.Properties = $ruleproperties  
$aclrule.ResourceId = "AllowAll_Outbound"  
$aclrules += $aclrule  

$acllistproperties = new-object Microsoft.Windows.NetworkController.AccessControlListProperties  
$acllistproperties.AclRules = $aclrules  

New-NetworkControllerAccessControlList -ResourceId "Subnet-192-168-0-0" -Properties $acllistproperties -ConnectionUri $ncURI   
```  

