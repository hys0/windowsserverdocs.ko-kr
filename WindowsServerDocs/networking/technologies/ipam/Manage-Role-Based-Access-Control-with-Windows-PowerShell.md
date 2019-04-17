---
title: 역할 기반 관리 액세스를 Windows PowerShell 제어
description: 이 항목은 Windows Server 2016에는 IP 주소 관리 (IPAM) 관리 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4f13f78e-0114-4e41-9a28-82a4feccecfc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: df6fa423a4ec891f1ad3faefad6c6054519542c4
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="manage-role-based-access-control-with-windows-powershell"></a>역할 기반 관리 액세스를 Windows PowerShell 제어

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 IPAM 역할 기반 액세스 제어를 Windows PowerShell로 관리 하기 위해 사용 하는 방법을 알아보려면 사용할 수 있습니다.  
  
>[!NOTE]
>Windows PowerShell IPAM 명령 참조 참조 [Windows PowerShell의 IP 주소 관리 (IPAM) 서버 Cmdlet](https://technet.microsoft.com/library/jj553807.aspx)합니다.  
  
새로운 Windows PowerShell IPAM 명령 검색 하 고 액세스 범위 DNS 및 DHCP 개체를 변경할 수 있는 제공 합니다. 다음 표에서 각 IPAM 개체를 사용 하는 올바른 명령을 보여 줍니다.  
  
|IPAM 개체|명령|설명|  
|---------------|-----------|---------------|  
|DNS 서버|Get IpamDnsServer|이 cmdlet DNS 서버 개체 IPAM에서 반환|  
|DNS 영역|Get IpamDnsZone|이 cmdlet IPAM DNS 영역 개체를 반환|  
|DNS 리소스 기록|Get IpamResourceRecord|이 cmdlet IPAM DNS 리소스 기록 개체를 반환|  
|DNS 조건부 전달자|Get IpamDnsConditionalForwarder|이 cmdlet IPAM DNS 조건부 전달자 개체를 반환|  
|DHCP 서버|Get IpamDhcpServer|이 cmdlet DHCP 서버 개체 IPAM에서 반환|  
|DHCP 범위|Get IpamDhcpSuperscope|이 cmdlet IPAM DHCP 범위 개체를 반환|  
|DHCP 범위|Get IpamDhcpScope|이 cmdlet IPAM DHCP 범위 개체를 반환|  
  
다음 명령 출력 예제에서는 `Get-IpamDnsZone` cmdlet 검색는 **dublin.contoso.com** DNS 영역 합니다.  
  
```  
PS C:\Users\Administrator.CONTOSO> Get-IpamDnsZone -ZoneType Forward -ZoneName dublin.contoso.com  
  
ZoneName             : dublin.contoso.com  
ZoneType             : Forward  
AccessScopePath      : \Global\Dublin  
IsSigned             : False  
DynamicUpdateStatus  : None  
ScavengeStaleRecords : False  
```  
  
## <a name="setting-access-scopes-on-ipam-objects"></a>액세스 범위 IPAM 물체에서 설정  
사용 하 여 IPAM 개체에 액세스 범위를 설정할 수 있는 `Set-IpamAccessScope` 명령을 합니다. 이 명령을 액세스 범위 개체 특정 값으로 설정 하거나 액세스 범위 부모 물체에서 상속 개체 하 게 사용할 수 있습니다. 다음은 개체를이 명령으로 구성할 수 있습니다.  
  
-   DHCP 범위  
  
-   DHCP 서버  
  
-   DHCP 범위  
  
-   DNS 조건부 전달자  
  
-   DNS 레코드 리소스  
  
-   DNS 서버  
  
-   DNS 영역  
  
-   IP 주소 차단  
  
-   IP 주소 범위  
  
-   IP 주소 공간  
  
-   IP 주소 서브넷  
  
다음은 구문을 `Set-IpamAccessScope` 명령을 합니다.  
  
```  
NAME  
    Set-IpamAccessScope  
  
SYNTAX  
    Set-IpamAccessScope [-IpamRange] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamDnsServer] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamDhcpServer] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamDhcpSuperscope] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamDhcpScope] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamDnsConditionalForwarder] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamDnsResourceRecord] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamDnsZone] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamAddressSpace] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamSubnet] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamBlock] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  [<CommonParameters>]  
```  
  
다음 예제 DNS 영역의 액세스 범위 **dublin.contoso.com** 에서 변경 **더블린** 에 **유럽**합니다.  
  
```  
PS C:\Users\Administrator.CONTOSO> Get-IpamDnsZone -ZoneType Forward -ZoneName dublin.contoso.com  
  
ZoneName             : dublin.contoso.com  
ZoneType             : Forward  
AccessScopePath      : \Global\Dublin  
IsSigned             : False  
DynamicUpdateStatus  : None  
ScavengeStaleRecords : False  
  
PS C:\Users\Administrator.CONTOSO> $a = Get-IpamDnsZone -ZoneType Forward -ZoneName dublin.contoso.com  
PS C:\Users\Administrator.CONTOSO> Set-IpamAccessScope -IpamDnsZone -InputObject $a -AccessScopePath \Global\Europe -PassThru  
  
ZoneName             : dublin.contoso.com  
ZoneType             : Forward  
AccessScopePath      : \Global\Europe  
IsSigned             : False  
DynamicUpdateStatus  : None  
ScavengeStaleRecords : False  
```  
  


