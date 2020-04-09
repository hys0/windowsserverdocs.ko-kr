---
title: PowerShell Direct를 사용 하 여 Windows 가상 머신 관리
description: PowerShell Direct를 사용 하 여 네트워크 또는 원격 연결을 사용 하지 않고 가상 컴퓨터를 관리 하는 방법에 대 한 지침을 제공 합니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: b5715c02-a90f-4de9-a71e-0fc09093ba2d
author: kbdazure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: c4a051de2d8f62c38ae0c44b1a62d5bf9df339e8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859436"
---
# <a name="manage-windows-virtual-machines-with-powershell-direct"></a>PowerShell Direct를 사용 하 여 Windows 가상 머신 관리

>적용 대상: Windows 10, Windows Server 2016, Windows Server 2019
  
PowerShell Direct를 사용 하 여 windows 10, windows server 2016 또는 windows Server 2019 Hyper-v 호스트에서 Windows 10, Windows Server 2016 또는 Windows Server 2019 가상 컴퓨터를 원격으로 관리할 수 있습니다. PowerShell Direct는 Hyper-v 호스트 또는 가상 컴퓨터의 네트워크 구성 또는 원격 관리 설정에 관계 없이 가상 컴퓨터 내에서 Windows PowerShell 관리를 허용 합니다. 이를 통해 Hyper-V 관리자는 스크립트 가상 컴퓨터 관리 및 구성을 더욱 쉽게 자동화할 수 있습니다.  
  
PowerShell Direct를 실행하는 방법은 두 가지가 있습니다.  
  
- PSSession cmdlet을 사용 하 여 PowerShell Direct 세션 만들기 및 종료
  
- Invoke 명령 cmdlet을 사용 하 여 스크립트 또는 명령 실행
  
이전 가상 컴퓨터를 관리하는 경우 가상 컴퓨터 연결(VMConnect)을 사용하거나 [가상 컴퓨터에 대한 가상 네트워크를 구성합니다](https://technet.microsoft.com/library/cc816585.aspx).  
  
## <a name="create-and-exit-a-powershell-direct-session-using-pssession-cmdlets"></a>PSSession cmdlet을 사용 하 여 PowerShell Direct 세션 만들기 및 종료  
  
1. Hyper-V 호스트에서 관리자 권한으로 Windows PowerShell을 엽니다.  
  
2. [Enter-PSSession](https://technet.microsoft.com/library/hh849707.aspx) cmdlet을 사용 하 여 가상 컴퓨터에 연결 합니다. 다음 명령 중 하나를 실행 하 여 가상 머신 이름 또는 GUID를 사용 하 여 세션을 만듭니다.  
  
    ```  
    Enter-PSSession -VMName <VMName>  
    ```  
  
    ```  
    Enter-PSSession -VMGUID <VMGUID>  
    ```  
  
3. 가상 컴퓨터에 대 한 자격 증명을 입력 합니다.   
4. 실행해야 하는 명령을 실행합니다. 이러한 명령은 세션을 만든 가상 컴퓨터에서 실행됩니다.  
  
5.  완료 되 면 [종료 PSSession](https://technet.microsoft.com/library/hh849743.aspx) 을 사용 하 여 세션을 닫습니다.   
  
    ```  
    Exit-PSSession  
    ```  
  
## <a name="run-script-or-command-with-invoke-command-cmdlet"></a>Invoke 명령 cmdlet을 사용 하 여 스크립트 또는 명령 실행  
[Invoke-Command](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Invoke-Command) cmdlet을 사용하여 가상 컴퓨터에서 미리 결정된 명령 집합을 실행할 수 있습니다. 다음은 PSTest가 가상 컴퓨터 이름인 Invoke-Command cmdlet을 사용하는 방법의 예제이며 실행할 스크립트(foo.ps1)는 C:/ 드라이브의 스크립트 폴더에 있습니다.  
  
```  
Invoke-Command -VMName PSTest  -FilePath C:\script\foo.ps1  
```  
  
단일 명령을 실행하려면 **-ScriptBlock** 매개 변수를 사용합니다.  
  
```  
Invoke-Command -VMName PSTest  -ScriptBlock { cmdlet }  
```  
  
## <a name="whats-required-to-use-powershell-direct"></a>PowerShell Direct를 사용 하려면 무엇이 필요 한가요?  
가상 컴퓨터에서 PowerShell Direct 세션을 만들려면  
  
-   가상 컴퓨터는 호스트에서 로컬로 실행 중이고 부팅되어야 합니다.  
  
-   Hyper-V 관리자로 호스트 컴퓨터에 로그인해야 합니다.  
  
-   가상 컴퓨터에 대해 유효한 사용자 자격 증명을 제공해야 합니다.  
  
-   호스트 운영 체제에서 Windows 10 또는 Windows Server 2016 이상을 실행 해야 합니다.
  
-   가상 컴퓨터는 Windows 10 또는 Windows Server 2016 이상을 실행 해야 합니다.  
  
Hyper-v cmdlet을 사용 [하 여 사용](https://docs.microsoft.com/powershell/module/hyper-v/get-vm) 중인 자격 증명에 hyper-v 관리자 역할이 있는지 확인 하 고 호스트에서 로컬로 실행 되 고 부팅 되는 가상 컴퓨터의 목록을 가져올 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[Enter-PSSession](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Enter-PSSession)  
[종료-PSSession](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Exit-PSSession)  
[Invoke 명령](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Invoke-Command)  
  


