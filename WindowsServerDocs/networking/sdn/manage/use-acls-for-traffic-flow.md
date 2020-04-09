---
title: Acl (액세스 제어 목록)을 사용 하 여 데이터 센터 네트워크 트래픽 흐름 관리
description: 이 항목에서는 Acl (액세스 제어 목록)을 구성 하 여 가상 서브넷의 데이터 센터 방화벽과 Acl을 사용 하는 데이터 트래픽 흐름을 관리 하는 방법에 대해 알아봅니다. 가상 서브넷 또는 네트워크 인터페이스에 적용 되는 Acl을 만들어 데이터 센터 방화벽을 사용 하도록 설정 하 고 구성 합니다.
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 6a7ac5af-85e9-4440-a631-6a3a38e9015d
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/27/2018
ms.openlocfilehash: 2b8a3af119ac11f3bcfd704bb4f43f12c989dbf6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854416"
---
# <a name="use-access-control-lists-acls-to-manage-datacenter-network-traffic-flow"></a>Acl (액세스 제어 목록)을 사용 하 여 데이터 센터 네트워크 트래픽 흐름 관리

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 Acl (액세스 제어 목록)을 구성 하 여 가상 서브넷의 데이터 센터 방화벽과 Acl을 사용 하는 데이터 트래픽 흐름을 관리 하는 방법에 대해 알아봅니다. 가상 서브넷 또는 네트워크 인터페이스에 적용 되는 Acl을 만들어 데이터 센터 방화벽을 사용 하도록 설정 하 고 구성 합니다.   

이 항목의 다음 예제에서는 Windows PowerShell을 사용 하 여 이러한 Acl을 만드는 방법을 보여 줍니다.  

## <a name="configure-datacenter-firewall-to-allow-all-traffic"></a>모든 트래픽을 허용 하도록 데이터 센터 방화벽 구성  

SDN을 배포한 후에는 새 환경에서 기본 네트워크 연결을 테스트 해야 합니다.  이를 위해 제한 없이 모든 네트워크 트래픽을 허용 하는 데이터 센터 방화벽에 대 한 규칙을 만듭니다.   

다음 표의 항목을 사용 하 여 모든 인바운드 및 아웃 바운드 네트워크 트래픽을 허용 하는 규칙 집합을 만듭니다.


| 원본 IP | 대상 IP | 프로토콜 | 원본 포트 | 대상 포트 | Direction | 작업 | Priority |
|:---------:|:--------------:|:--------:|:-----------:|:----------------:|:---------:|:------:|:--------:|
|    \*     |       \*       |   모두    |     \*      |        \*        |  인바운드  | 허용  |   100    |
|    \*     |       \*       |   모두    |     \*      |        \*        | 아웃바운드  | 허용  |   110    |

---       

### <a name="example-create-an-acl"></a>예: ACL 만들기 
이 예제에서는 두 개의 규칙을 사용 하 여 ACL을 만듭니다.

1. **AllowAll_Inbound** -모든 네트워크 트래픽이이 ACL이 구성 된 네트워크 인터페이스로 전달 되도록 허용 합니다.    
2. **AllowAllOutbound** -모든 트래픽이 네트워크 인터페이스에서 통과할 수 있도록 허용 합니다. 이제 리소스 id "AllowAll-1"로 식별 된이 ACL을 가상 서브넷 및 네트워크 인터페이스에서 사용할 수 있습니다.  

다음 예제 스크립트는 **NetworkController** 모듈에서 내보낸 Windows PowerShell 명령을 사용 하 여이 ACL을 만듭니다.  


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
>네트워크 컨트롤러에 대 한 Windows PowerShell 명령 참조는 [네트워크 컨트롤러 cmdlet](https://technet.microsoft.com/library/mt576401.aspx)항목에 있습니다.  

## <a name="use-acls-to-limit-traffic-on-a-subnet"></a>Acl을 사용 하 여 서브넷의 트래픽 제한  
이 예제에서는 192.168.0.0/24 서브넷 내의 Vm이 서로 통신 하는 것을 방지 하는 ACL을 만듭니다. 이 유형의 ACL은 공격자가 서브넷 내에서 수평를 분산 하는 기능을 제한 하는 동시에 다른 서브넷의 다른 서비스와 통신 하는 것 뿐만 아니라 서브넷 외부에서 요청을 받을 수 있도록 하는 데 유용 합니다.   


|   원본 IP    | 대상 IP | 프로토콜 | 원본 포트 | 대상 포트 | Direction | 작업 | Priority |
|:--------------:|:--------------:|:--------:|:-----------:|:----------------:|:---------:|:------:|:--------:|
|  192.168.0.1   |       \*       |   모두    |     \*      |        \*        |  인바운드  | 허용  |   100    |
|       \*       |  192.168.0.1   |   모두    |     \*      |        \*        | 아웃바운드  | 허용  |   101    |
| 192.168.0.0/24 |       \*       |   모두    |     \*      |        \*        |  인바운드  | 블록  |   102    |
|       \*       | 192.168.0.0/24 |   모두    |     \*      |        \*        | 아웃바운드  | 블록  |   103    |
|       \*       |       \*       |   모두    |     \*      |        \*        |  인바운드  | 허용  |   104    |
|       \*       |       \*       |   모두    |     \*      |        \*        | 아웃바운드  | 허용  |   105    |

--- 

리소스 id **서브넷-192-168-0-0**으로 식별 되는 아래 예제 스크립트에서 만든 ACL은 이제 "192.168.0.0/24" 서브넷 주소를 사용 하는 가상 네트워크 서브넷에 적용할 수 있습니다.  해당 가상 네트워크 서브넷에 연결 된 모든 네트워크 인터페이스는 자동으로 위의 ACL 규칙을 적용 합니다.  

다음은 네트워크 컨트롤러 REST API를 사용 하 여이 ACL을 만드는 Windows Powershell 명령을 사용 하는 예제 스크립트입니다.  

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

