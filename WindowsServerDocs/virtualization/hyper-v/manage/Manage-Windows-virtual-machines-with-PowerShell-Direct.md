---
title: PowerShell Direct를 사용 하 여 Windows virtual machines 관리
description: PowerShell Direct를 사용 하 여 네트워크 또는 원격 연결에 의존 하지 않고 가상 컴퓨터를 관리 하는 지침을 제공 합니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5715c02-a90f-4de9-a71e-0fc09093ba2d
author: KBDAzure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 4081a9737825d2f50f0d3b19b3bada3b9bbc76f1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814704"
---
# <a name="manage-windows-virtual-machines-with-powershell-direct"></a>PowerShell Direct를 사용 하 여 Windows virtual machines 관리

>적용 대상: Windows 10, Windows Server 2016, Windows Server 2019
  
Windows 10, Windows Server 2016 또는 Windows Server 2019 Hyper-v 호스트에서 Windows 10, Windows Server 2016 또는 Windows Server 2019 가상 컴퓨터를 원격으로 관리 하려면 PowerShell Direct를 사용할 수 있습니다. PowerShell Direct는 네트워크 구성 또는 Hyper-v 호스트에서 원격 관리 설정에 관계 없이 또는 가상 컴퓨터 내에서 Windows PowerShell 관리를 허용합니다. 이를 통해 Hyper-V 관리자는 스크립트 가상 컴퓨터 관리 및 구성을 더욱 쉽게 자동화할 수 있습니다.  
  
PowerShell Direct를 실행하는 방법은 두 가지가 있습니다.  
  
- 만들고 PSSession cmdlet을 사용 하 여 PowerShell Direct 세션을 종료 합니다.
  
- 이 명령은 Invoke-command cmdlet으로 스크립트 또는 명령을 실행합니다
  
이전 가상 컴퓨터를 관리하는 경우 가상 컴퓨터 연결(VMConnect)을 사용하거나 [가상 컴퓨터에 대한 가상 네트워크를 구성합니다](https://technet.microsoft.com/library/cc816585.aspx).  
  
## <a name="create-and-exit-a-powershell-direct-session-using-pssession-cmdlets"></a>만들고 PSSession cmdlet을 사용 하 여 PowerShell Direct 세션을 종료 합니다.  
  
1. Hyper-V 호스트에서 관리자 권한으로 Windows PowerShell을 엽니다.  
  
2. 사용 된 [Enter-pssession](https://technet.microsoft.com/library/hh849707.aspx) 가상 머신에 연결 하는 cmdlet입니다. 가상 컴퓨터 이름 또는 GUID를 사용 하 여 세션을 만들려면 다음 명령 중 하나를 실행 합니다.  
  
    ```  
    Enter-PSSession -VMName <VMName>  
    ```  
  
    ```  
    Enter-PSSession -VMGUID <VMGUID>  
    ```  
  
3. 가상 컴퓨터에 대 한 자격 증명을 입력 합니다.   
4. 실행해야 하는 명령을 실행합니다. 이러한 명령은 세션을 만든 가상 컴퓨터에서 실행됩니다.  
  
5.  사용 하 여 작업을 완료 하는 [Exit-pssession](https://technet.microsoft.com/library/hh849743.aspx) 세션을 닫아야 합니다.   
  
    ```  
    Exit-PSSession  
    ```  
  
## <a name="run-script-or-command-with-invoke-command-cmdlet"></a>이 명령은 Invoke-command cmdlet으로 스크립트 또는 명령을 실행합니다  
[Invoke-Command](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Invoke-Command) cmdlet을 사용하여 가상 컴퓨터에서 미리 결정된 명령 집합을 실행할 수 있습니다. 다음은 PSTest가 가상 컴퓨터 이름인 Invoke-Command cmdlet을 사용하는 방법의 예제이며 실행할 스크립트(foo.ps1)는 C:/ 드라이브의 스크립트 폴더에 있습니다.  
  
```  
Invoke-Command -VMName PSTest  -FilePath C:\script\foo.ps1  
```  
  
단일 명령을 실행하려면 **-ScriptBlock** 매개 변수를 사용합니다.  
  
```  
Invoke-Command -VMName PSTest  -ScriptBlock { cmdlet }  
```  
  
## <a name="whats-required-to-use-powershell-direct"></a>PowerShell Direct를 사용 하는 데 필요한 무엇입니까?  
가상 컴퓨터에서 PowerShell Direct 세션을 만들려면  
  
-   가상 컴퓨터는 호스트에서 로컬로 실행 중이고 부팅되어야 합니다.  
  
-   Hyper-V 관리자로 호스트 컴퓨터에 로그인해야 합니다.  
  
-   가상 컴퓨터에 대해 유효한 사용자 자격 증명을 제공해야 합니다.  
  
-   호스트 운영 체제 이상을 실행 해야 Windows 10 또는 Windows Server 2016 합니다.
  
-   가상 컴퓨터 이상을 실행 해야 Windows 10 또는 Windows Server 2016 합니다.  
  
사용할 수는 [GET-VM](https://docs.microsoft.com/powershell/module/hyper-v/get-vm) cmdlet를 사용 하는 자격 증명에 Hyper-v 관리자 역할이 있는지 확인 하 고 가상 컴퓨터 호스트에서 로컬로 실행 하 고 부팅의 목록을 가져옵니다.  
  
## <a name="see-also"></a>관련 항목  
[Enter-PSSession](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Enter-PSSession)  
[Exit-PSSession](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Exit-PSSession)  
[Invoke-Command](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Invoke-Command)  
  


