---
title: Windows PowerShell 을 사용하여 역할 기반 액세스 제어 관리
description: 이 항목은 Windows Server 2016에서 관리 IPAM (IP 주소) 관리 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4f13f78e-0114-4e41-9a28-82a4feccecfc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 11dd417be4720b09851fc03f111edaaf06b55e59
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282129"
---
# <a name="manage-role-based-access-control-with-windows-powershell"></a>Windows PowerShell 을 사용하여 역할 기반 액세스 제어 관리

>적용 대상: Windows Server (반기 채널), Windows Server 2016

Windows PowerShell을 사용 하 여 역할 기반 액세스 제어를 관리 하려면 IPAM을 사용 하는 방법을 알아보려면이 항목에서는 사용할 수 있습니다.  
  
>[!NOTE]
>IPAM Windows PowerShell 명령 참조에 대 한 참조를 [Windows PowerShell의 cmdlet IpamServer](https://docs.microsoft.com/powershell/module/ipamserver/?view=win10-ps)합니다.  
  
새 Windows PowerShell IPAM 명령을 검색 하 고 DNS 및 DHCP 개체의 액세스 범위를 변경 하는 기능을 제공 합니다. 다음 표에서 올바른 명령에서 각 IPAM 개체에 대 한 사용을 보여 줍니다.  
  
|IPAM 개체|명령|설명|  
|---------------|-----------|---------------|  
|DNS 서버|Get-IpamDnsServer|이 cmdlet은 IPAM에서 DNS 서버 개체를 반환합니다.|  
|DNS 영역|Get-IpamDnsZone|이 cmdlet은 IPAM에서 DNS 영역 개체를 반환합니다.|  
|DNS 리소스 레코드|Get-IpamResourceRecord|이 cmdlet은 IPAM에서 DNS 리소스 레코드 개체를 반환합니다.|  
|DNS 조건부 전달자|Get-IpamDnsConditionalForwarder|이 cmdlet은 IPAM의 DNS 조건부 전달자 개체를 반환합니다.|  
|DHCP 서버|Get-IpamDhcpServer|이 cmdlet은 IPAM에서 DHCP 서버 개체를 반환합니다.|  
|DHCP 대범위|Get-IpamDhcpSuperscope|이 cmdlet은 IPAM에서 DHCP 대 범위 개체를 반환합니다.|  
|DHCP 범위|Get-IpamDhcpScope|이 cmdlet은 IPAM에서 DHCP 범위 개체를 반환합니다.|  
  
명령 출력의 다음 예제에서는 `Get-IpamDnsZone` cmdlet을 검색 합니다 **dublin.contoso.com** DNS 영역입니다.  
  
```  
PS C:\Users\Administrator.CONTOSO> Get-IpamDnsZone -ZoneType Forward -ZoneName dublin.contoso.com  
  
ZoneName             : dublin.contoso.com  
ZoneType             : Forward  
AccessScopePath      : \Global\Dublin  
IsSigned             : False  
DynamicUpdateStatus  : None  
ScavengeStaleRecords : False  
```  
  
## <a name="setting-access-scopes-on-ipam-objects"></a>IPAM 개체에 대 한 액세스 범위 설정  
사용 하 여 IPAM 개체에 대 한 액세스 범위를 설정할 수는 `Set-IpamAccessScope` 명령입니다. 부모 개체에 액세스 범위 상속에 개체 또는 개체에 대 한 특정 값에 대 한 액세스 범위를 설정 하려면이 명령을 사용할 수 있습니다. 다음은이 명령을 사용 하 여 구성할 수 있는 개체입니다.  
  
-   DHCP 범위  
  
-   DHCP 서버  
  
-   DHCP 대범위  
  
-   DNS 조건부 전달자  
  
-   DNS 리소스 레코드  
  
-   DNS 서버  
  
-   DNS 영역  
  
-   IP 주소 블록  
  
-   IP 주소 범위  
  
-   IP 주소 공간  
  
-   IP 주소 서브넷  
  
다음 구문은 `Set-IpamAccessScope` 명령입니다.  
  
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
  
다음 예제에서는 DNS 영역 액세스 범위의 **dublin.contoso.com** 에서 변경 되었습니다 **더블린** 에 **유럽**합니다.  
  
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
  


