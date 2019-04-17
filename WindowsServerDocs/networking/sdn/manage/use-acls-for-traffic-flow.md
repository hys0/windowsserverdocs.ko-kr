---
title: 액세스를 제어 (Acl 목록) 교통 흐름 Datacenter 네트워크 관리를 사용 하 여
description: 이 항목은 관리 테 작업 및 Windows Server 2016에 가상 네트워크 방법에 대해 소프트웨어 네트워킹 정의 가이드 일부입니다.
manager: brianlic
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
ms.openlocfilehash: 64b7e1abf1ddb8132a8c6692fe82521c589f32df
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="use-access-control-lists-acls-to-manage-datacenter-network-traffic-flow"></a>액세스를 제어 (Acl 목록) 교통 흐름 Datacenter 네트워크 관리를 사용 하 여

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 구성 액세스 제어 목록을 Datacenter 방화벽 및 Acl 가상 서브넷에 사용 하 여 데이터 교통 흐름을 관리 하는 방법을 알아보려면 사용할 수 있습니다.  
  
사용 하도록 설정 하 고 만들어 Acl 가상 서브넷 또는 네트워크 인터페이스에 적용 되는 데이터 센터 방화벽 구성할 수 있습니다.  
  
다음은 Windows PowerShell 이러한 Acl 만드는 사용 하는 방법을 보여 줍니다.  
  
## <a name="configure-datacenter-firewall-to-allow-all-traffic"></a>모든 교통 수 있도록 데이터 센터 방화벽 구성  
  
SDN를 배포한 후 기본 네트워크 연결이 새로운 환경에 테스트 하는 것이 좋습니다.  
  
이를 위해 규칙 제한 없이 모든 네트워크 교통 허용 하는 데이터 센터 방화벽을 만들 수 있습니다.   
  
다음 표에 있는 일련의 모든 인바인드 및 아웃 바운드 네트워크 교통 수 있도록 규칙 만들 수 항목을 사용할 수 있습니다.  
  
  
  
원본 i P|대상 IP|프로토콜|원본 포트|대상 포트|방향|알림|우선 순위 부여   
---------|---------|---------|---------|---------|---------|---------|---------  
*    |   *      |   모든      |    *     |      *   |     돌아오는    |   허용      |   100        
*    |     *    |     모든    |     *    |     *    |   아웃 바운드      |  허용       |  110         
  
  
이 들어 스크립트 두 규칙 포함 된 ACL 만들어집니다.    
- 첫 번째 규칙 "AllowAll_Inbound" 모든 네트워크 교통 체증이이 ACL 구성 된 네트워크 인터페이스도 전달할 수 있게 합니다.    
- 두 번째 규칙 "AllowAllOutbound" 네트워크 인터페이스를 전달 하는 모든 교통 수 있게 합니다.  
"AllowAll 1" 리소스 id로 식별이 ACL 가상 서브넷 및 한 네트워크 인터페이스 사용할 준비가 되었습니다.  
  
다음 예제 스크립트 내보낸에서 Windows PowerShell 명령을 사용 하는 **NetworkController** 모듈이이 ACL 만들 수 있습니다.  
  
  
```  
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
>네트워크 컨트롤러에 대 한 Windows PowerShell 명령 참조 주제에 있는 [네트워크 컨트롤러 Cmdlet](https://technet.microsoft.com/library/mt576401.aspx)합니다.  
  
## <a name="use-acls-to-limit-traffic-on-a-subnet"></a>Acl를 사용 하 여 서브넷 교통 제한  
  
서로 통신할에서 192.168.0.0/24 서브넷 내 Vm (가상 컴퓨터) 되지 않는 ACL 만드는이 예제를 사용할 수 있습니다.   
  
이 이와 같은 액세스 서브넷, 외부의 요청을 받을 수 뿐만 아니라 다른 서브넷 다른 서비스와 소통 하 고 Vm 여전히 허용 하면서도 서브넷, 내 옆쪽 확산 공격자 기능이 제한에 유용 합니다.  
  
  
원본 i P|대상 IP|프로토콜|원본 포트|대상 포트|방향|알림|우선 순위 부여   
---------|---------|---------|---------|---------|---------|---------|---------  
192.168.0.1    | * | 모든 | * | * | 돌아오는|   허용      |   100        
* |192.168.0.1 | 모든 | * | * | 아웃 바운드|  허용       |  101         
192.168.0.0/24 | * | 모든 | * | * | 돌아오는| 차단 | 102  
* | 192.168.0.0/24 |모든| * | * | 아웃 바운드 | 차단 |103  
* | *  |모든| * | * | 돌아오는 | 허용 |104  
* | *  |모든| * | * | 아웃 바운드 | 허용 |105  
  
아래의 예제 스크립트가 만든 ACL 리소스 id로 식별 **서브넷-192-168-0-0**, "192.168.0.0/24" 서브넷 주소를 사용 하 여 가상 네트워크 서브넷에 적용할 수 있습니다.  해당 가상 네트워크 서브넷에 자동으로 연결 되는 모든 네트워크 인터페이스 위의 ACL 규칙이 적용을 가져옵니다.  
  
다음은 Windows Powershell 명령을 사용 하 여 네트워크 컨트롤러 REST API를 사용 하 여이 ACL 만드는 예제 스크립트입니다.  
  
```  
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
  
