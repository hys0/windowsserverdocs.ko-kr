---
title: 데이터 센터 브리징 관리 (DCB)
description: 이 항목에서는 windows PowerShell 명령을 사용 하 여 Windows Server 2016에서 데이터 센터 브리징을 관리 하는 방법에 대 한 지침을 제공 합니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 1575cc7c-62a7-4add-8f78-e5d93effe93f
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d61287b82cd6d3b869b1120d3cb21b3c8792bd1e
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312758"
---
# <a name="manage-data-center-bridging-dcb"></a>데이터 센터 브리징 관리 (DCB)

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 windows PowerShell 명령을 사용 하 여 Windows Server 2016 또는 Windows 10을 실행 하는 컴퓨터에 설치 된\-DCB 호환 가능 네트워크 어댑터에서 DCB\) \(데이터 센터 브리징를 구성 하는 방법에 대 한 지침을 제공 합니다.

## <a name="install-dcb-in-windows-server-2016-or-windows-10"></a>Windows Server 2016 또는 Windows 10에서 DCB 설치

를 사용 하기 위한 필수 구성 요소 및 DCB 설치 방법에 대 한 자세한 내용은 [Windows Server 2016 또는 windows 10에서 데이터 센터 브리징 설치 (DCB)](dcb-install.md)를 참조 하세요.


## <a name="dcb-configurations"></a>DCB 구성 

Windows Server 2016 이전에는 모든 DCB 구성이 DCB을 지 원하는 모든 네트워크 어댑터에 전체적으로 적용 되었습니다. 

Windows Server 2016에서는 DCB 구성을 전역 정책 저장소 또는 개별 정책 저장소\(s\)적용할 수 있습니다. 개별 정책을 적용 하면 모든 전역 정책 설정이 재정의 됩니다.

시스템 수준의 트래픽 클래스, PFC 및 응용 프로그램 우선 순위 할당 구성은 다음 작업을 수행할 때까지 네트워크 어댑터에 적용 되지 않습니다.

1. DCBX의 비트를 false로 설정

2. 네트워크 어댑터에서 DCB를 사용 하도록 설정 합니다. [네트워크 어댑터에서 DCB 설정 사용 및 표시](#bkmk_enabledcb)를 참조 하세요.

>[!NOTE]
>DCBX을 통해 스위치에서 DCB을 구성 하려면 [dcbx 설정](#dcb-configuration-on-network-adapters)을 참조 하세요.

DCBX은 DCB 사양에 설명 되어 있습니다. 장치에서 할 일 비트가 true로 설정 된 경우 장치는 DCBX을 통해 원격 장치에서 구성을 허용 합니다. 장치에서 할 일 비트가 false로 설정 된 경우 장치는 원격 장치의 모든 구성 시도를 거부 하 고 로컬 구성만 적용 합니다.

DCB가 Windows Server 2016에 설치 되어 있지 않은 경우 운영 체제에 네트워크 어댑터에 적용 되는 로컬 설정이 없으므로 운영 체제에서 문제가 발생 하는 것과 같은 문제가 발생 합니다. DCB를 설치한 후에는 기본 비트의 기본값은 true입니다. 이 설계를 통해 네트워크 어댑터는 원격 피어에서 받은 모든 구성을 유지할 수 있습니다.

네트워크 어댑터가 DCBX을 지원 하지 않는 경우 원격 장치에서 구성을 수신 하지 않습니다. 운영 체제에서 구성을 수신 하지만 DCBX을 위한 비트가 false로 설정 된 후에만 구성 됩니다.

## <a name="set-the-willing-bit"></a>의사 비트 설정

네트워크 어댑터에 대 한 트래픽 클래스, PFC 및 응용 프로그램 우선 순위 할당의 운영 체제 구성을 적용 하거나 단순히 원격 장치에서 구성을 재정의 하는 경우 (\) 다음 명령을 실행할 수 있습니다.

>[!NOTE]
>DCB Windows PowerShell 명령 이름에는 이름 문자열에 "DCB" 대신 "QoS"가 포함 됩니다. 이는 QoS 및 DCB이 Windows Server 2016에 통합 되어 원활한 QoS 관리 환경을 제공 하기 때문입니다.

    
    Set-NetQosDcbxSetting -Willing $FALSE
    
    Confirm
    Are you sure you want to perform this action?
    Set-NetQosDcbxSetting -Willing $false
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"):
    

사용자의 비트 설정 상태를 표시 하려면 다음 명령을 사용할 수 있습니다.

    
    Get-NetQosDcbxSetting
    
    Willing PolicySetIfIndex IfAlias
    ------- ---------------- -------
    False   Global  
    

## <a name="dcb-configuration-on-network-adapters"></a>네트워크 어댑터의 DCB 구성

네트워크 어댑터에서 DCB를 사용 하도록 설정 하면 스위치에서 네트워크 어댑터로 전파 되는 구성을 확인할 수 있습니다.

DCB 구성에는 다음 단계가 포함 됩니다.

1.  다음을 포함 하는 시스템 수준에서 DCB 설정을 구성 합니다.

    a. 트래픽 클래스 관리
    
    b. PFC (우선 순위 흐름 제어) 설정
    
    c. 응용 프로그램 우선 순위 할당
    
    . DCBX 설정

2. 네트워크 어댑터에서 DCB를 구성 합니다.



##  <a name="dcb-traffic-class-management"></a>DCB Traffic 클래스 관리

트래픽 클래스 관리를 위한 Windows PowerShell 명령의 예는 다음과 같습니다.

### <a name="create-a-traffic-class"></a>트래픽 클래스 만들기

**Get-netqostrafficclass** 명령을 사용 하 여 traffic 클래스를 만들 수 있습니다.

    
    New-NetQosTrafficClass -Name SMB -Priority 4 -BandwidthPercentage 30 -Algorithm ETS
    
    Name Algorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ---- --------- ------------ -------- ---------------- -------
    SMB  ETS   30   4Global
      

기본적으로 모든 802.1 p 값은 실제 링크 대역폭의 100%를 포함 하는 기본 트래픽 클래스에 매핑됩니다. **Get-netqostrafficclass** 명령은 802.1 p 우선 순위 값 4로 태그가 지정 된 패킷이 매핑되는 새 트래픽 클래스를 만듭니다. 전송 선택 알고리즘 \(TSA\)은 (는), 대역폭의 30%가 있습니다.

최대 7 개의 새 트래픽 클래스를 만들 수 있습니다. 기본 트래픽 클래스를 포함 하 여 시스템에는 최대 8 개의 트래픽 클래스가 있을 수 있습니다. 그러나 DCB 가능 네트워크 어댑터는 하드웨어에서 많은 트래픽 클래스를 지원 하지 않을 수 있습니다. 네트워크 어댑터에서 수용할 수 있는 것 보다 더 많은 트래픽 클래스를 만들 때 해당 네트워크 어댑터에서 DCB를 사용 하도록 설정 하면 미니 포트 드라이버가 운영 체제에 오류를 보고 합니다. 오류는 이벤트 로그에 기록 됩니다.

만들어진 모든 트래픽 클래스에 대 한 대역폭 예약의 합계는 대역폭의 99%를 초과할 수 없습니다. 기본 트래픽 클래스에는 항상 1% 이상의 대역폭이 예약 되어 있습니다.

### <a name="display-traffic-classes"></a>트래픽 클래스 표시

**Get-netqostrafficclass** 명령을 사용 하 여 트래픽 클래스를 볼 수 있습니다.

    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   70   0-3,5-7  Global
    SMB ETS   30   4Global  
    
### <a name="modify-a-traffic-class"></a>트래픽 클래스 수정

**Get-netqostrafficclass** 명령을 사용 하 여 traffic 클래스를 만들 수 있습니다. 

    Set-NetQosTrafficClass -Name SMB -BandwidthPercentage 50

그런 다음 **get-netqostrafficclass** 명령을 사용 하 여 설정을 볼 수 있습니다.

    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   50   0-3,5-7  Global
    SMB ETS   50   4Global   
    

트래픽 클래스를 만든 후에는 해당 설정을 독립적으로 변경할 수 있습니다. 변경할 수 있는 설정은 다음과 같습니다.

1. 대역폭 할당 \(-BandwidthPercentage\)

2. TSA (\-알고리즘\)

3. 우선 순위 매핑 \(우선 순위\)

### <a name="remove-a-traffic-class"></a>트래픽 클래스 제거

**Get-netqostrafficclass** 명령을 사용 하 여 traffic 클래스를 삭제할 수 있습니다.

>[!IMPORTANT]
>기본 트래픽 클래스를 제거할 수 없습니다.


    Remove-NetQosTrafficClass -Name SMB

그런 다음 **get-netqostrafficclass** 명령을 사용 하 여 설정을 볼 수 있습니다.
    
    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   100  0-7  Global
    

트래픽 클래스를 제거 하면 해당 traffic 클래스에 매핑된 802.1 p 값이 기본 트래픽 클래스에 다시 매핑됩니다. 트래픽 클래스에 대해 예약 된 모든 대역폭은 트래픽 클래스가 제거 될 때 기본 트래픽 클래스 할당으로 반환 됩니다.

## <a name="per-network-interface-policies"></a>네트워크 별 인터페이스 정책

위의 모든 예제에서는 전역 정책을 설정 합니다. 다음은 NIC 별 정책을 설정 하 고 가져오는 방법에 대 한 예입니다. 

"PolicySet" 필드가 전역에서 AdapterSpecific으로 변경 됩니다. AdapterSpecific 정책이 표시 되 면 인터페이스 인덱스 \(ifIndex\) 및 인터페이스 이름 \(ifAlias\)도 표시 됩니다.

```
PS C:\> Get-NetQosTrafficClass

Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
[Default]   ETS       100          0-7              Global


PS C:\> Get-NetQosTrafficClass -InterfaceAlias M1

Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
[Default]   ETS       100          0-7              AdapterSpecific  4       M1


PS C:\> New-NetQosTrafficClass -Name SMBGlobal -BandwidthPercentage 30 -Priority 4 -Algorithm ETS

Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
SMBGlobal   ETS       30           4                Global


PS C:\> New-NetQosTrafficClass -Name SMBforM1 -BandwidthPercentage 30 -Priority 4 -Algorithm ETS -Interfac


Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
SMBforM1    ETS       30           4                AdapterSpecific  4       M1


PS C:\> Get-NetQosTrafficClass

Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
[Default]   ETS       70           0-3,5-7          Global
SMBGlobal   ETS       30           4                Global


PS C:\> Get-NetQosTrafficClass -InterfaceAlias M1

Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
[Default]   ETS       70           0-3,5-7          AdapterSpecific  4       M1
SMBforM1    ETS       30           4                AdapterSpecific  4       M1


```

## <a name="priority-flow-control-settings"></a>우선 순위 흐름 제어 설정:

우선 순위 흐름 제어 설정에 대 한 명령 예제는 다음과 같습니다. 이러한 설정은 개별 어댑터에도 지정할 수 있습니다.

### <a name="enable-and-display-priority-flow-control-for-global-and-interface-specific-use-cases"></a>전역 및 인터페이스 특정 사용 사례에 대 한 우선 순위 흐름 제어를 설정 하 고 표시 합니다.

```
PS C:\> Enable-NetQosFlowControl -Priority 4
PS C:\> Enable-NetQosFlowControl -Priority 3 -InterfaceAlias M1
PS C:\> Get-NetQosFlowControl

Priority   Enabled    PolicySet        IfIndex IfAlias
--------   -------    ---------        ------- -------
0          False      Global
1          False      Global
2          False      Global
3          False      Global
4          True       Global
5          False      Global
6          False      Global
7          False      Global

PS C:\> Get-NetQosFlowControl -InterfaceAlias M1

Priority   Enabled    PolicySet        IfIndex IfAlias
--------   -------    ---------        ------- -------
0          False      AdapterSpecific  4       M1
1          False      AdapterSpecific  4       M1
2          False      AdapterSpecific  4       M1
3          True       AdapterSpecific  4       M1
4          False      AdapterSpecific  4       M1
5          False      AdapterSpecific  4       M1
6          False      AdapterSpecific  4       M1
7          False      AdapterSpecific  4       M1  

```


### <a name="disable-priority-flow-control-global-and-interface-specific"></a>우선 순위 흐름 제어 사용 안 함 (전역 및 인터페이스 특정)

```
PS C:\> Disable-NetQosFlowControl -Priority 4
PS C:\> Disable-NetQosFlowControl -Priority 3 -InterfaceAlias m1
PS C:\> Get-NetQosFlowControl

Priority   Enabled    PolicySet        IfIndex IfAlias
--------   -------    ---------        ------- -------
0          False      Global
1          False      Global
2          False      Global
3          False      Global
4          False      Global
5          False      Global
6          False      Global
7          False      Global


PS C:\> Get-NetQosFlowControl -InterfaceAlias M1

Priority   Enabled    PolicySet        IfIndex IfAlias
--------   -------    ---------        ------- -------
0          False      AdapterSpecific  4       M1
1          False      AdapterSpecific  4       M1
2          False      AdapterSpecific  4       M1
3          False      AdapterSpecific  4       M1
4          False      AdapterSpecific  4       M1
5          False      AdapterSpecific  4       M1
6          False      AdapterSpecific  4       M1
7          False      AdapterSpecific  4       M1  

```

##  <a name="application-priority-assignment"></a>응용 프로그램 우선 순위 할당

우선 순위 할당의 예는 다음과 같습니다.

### <a name="create-qos-policy"></a>QoS 정책 만들기

```
PS C:\> New-NetQosPolicy -Name "SMB Policy" -PriorityValue8021Action 4

Name           : SMB Policy
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
JobObject      :
PriorityValue  : 4

```

이전 명령은 SMB에 대 한 새 정책을 만듭니다. – SMB는 TCP 포트 445 (SMB 용으로 예약 됨)와 일치 하는 수신함 필터입니다. 패킷이 TCP 포트 445로 전송 되 면 패킷이 네트워크 미니 포트 드라이버로 전달 되기 전에 운영 체제에서 802.1 p 값 4로 태그를 지정 합니다.

– SMB 외에도 기타 기본 필터는 – iSCSI (일치 하는 tcp 포트 3260),-NFS (tcp 포트 2049 일치),-LiveMigration (TCP 포트 6600 일치),-FCOE (일치 하는 EtherType 0x8906) 및 – NetworkDirect를 포함 합니다.

NetworkDirect는 네트워크 어댑터의 RDMA 구현 위에 만드는 추상 계층입니다. – NetworkDirect 뒤에는 네트워크 Direct 포트가와 야 합니다.

기본 필터 외에도, 응용 프로그램의 실행 파일 이름 (아래의 첫 번째 예제에서와 같이) 또는 IP 주소, 포트 또는 프로토콜 (두 번째 예제에 표시 된 대로)을 기준으로 트래픽을 분류할 수 있습니다.

**실행 파일 이름별**

```
PS C:\> New-NetQosPolicy -Name background -AppPathNameMatchCondition "C:\Program files (x86)\backup.exe" -PriorityValue8021Action 1

Name           : background
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
AppPathName    : C:\Program files (x86)\backup.exe
JobObject      :
PriorityValue  : 1

```


**IP 주소 포트 또는 프로토콜 별**

```
PS C:\> New-NetQosPolicy -Name "Network Management" -IPDstPrefixMatchCondition 10.240.1.0/24 -IPProtocolMatchCondition both -NetworkProfile all -PriorityValue8021Action 7

Name           : Network Management
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
JobObject      :
IPProtocol     : Both
IPDstPrefix    : 10.240.1.0/24
PriorityValue  : 7

```

### <a name="display-qos-policy"></a>QoS 정책 표시

```
PS C:\> Get-NetQosPolicy

Name           : background
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
AppPathName    : C:\Program files (x86)\backup.exe
JobObject      :
PriorityValue  : 1

Name           : Network Management
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
JobObject      :
IPProtocol     : Both
IPDstPrefix    : 10.240.1.0/24
PriorityValue  : 7

Name           : SMB Policy
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
JobObject      :
PriorityValue  : 4

```

### <a name="modify-qos-policy"></a>QoS 정책 수정

다음과 같이 QoS 정책을 수정할 수 있습니다.


```
PS C:\> Set-NetQosPolicy -Name "Network Management" -IPSrcPrefixMatchCondition 10.235.2.0/24 -IPProtocolMatchCondition both -PriorityValue8021Action 7
PS C:\> Get-NetQosPolicy

Name           : Network Management
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
JobObject      :
IPProtocol     : Both
IPSrcPrefix    : 10.235.2.0/24
IPDstPrefix    : 10.240.1.0/24
PriorityValue  : 7


```

### <a name="remove-qos-policy"></a>QoS 정책 제거

```
PS C:\> Remove-NetQosPolicy -Name "Network Management"

Confirm
Are you sure you want to perform this action?
Remove-NetQosPolicy -Name "Network Management" -Store GPO:localhost
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): y  

```

## <a name="dcb-configuration-on-network-adapters"></a>네트워크 어댑터의 DCB 구성

네트워크 어댑터에 대 한 DCB 구성은 위에 설명 된 시스템 수준의 DCB 구성과 독립적입니다. 

DCB가 Windows Server 2016에 설치 되었는지 여부에 관계 없이 항상 다음 명령을 실행할 수 있습니다. 

스위치에서 DCB을 구성 하 고 DCBX을 사용 하 여 구성을 네트워크 어댑터에 전파 하는 경우 네트워크 어댑터에서 DCB을 사용 하도록 설정 하면 운영 체제 쪽에서 네트워크 어댑터에 대해 받아서 적용 되는 구성을 확인할 수 있습니다.

###  <a name="enable-and-display-dcb-settings-on--network-adapters"></a><a name="bkmk_enabledcb"></a>네트워크 어댑터에서 DCB 설정 사용 및 표시

```
PS C:\> Enable-NetAdapterQos M1
PS C:\> Get-NetAdapterQos

Name                       : M1
Enabled                    : True
Capabilities               :                       Hardware     Current
                                                   --------     -------
                             MacSecBypass        : NotSupported NotSupported
                             DcbxSupport         : None         None
                             NumTCs(Max/ETS/PFC) : 8/8/8        8/8/8

OperationalTrafficClasses  : TC TSA    Bandwidth Priorities
                             -- ---    --------- ----------
                              0 ETS    70%       0-3,5-7
                              1 ETS    30%       4

OperationalFlowControl     : All Priorities Disabled
OperationalClassifications : Protocol  Port/Type Priority
                             --------  --------- --------
                             Default             1


```

### <a name="disable-dcb-on-network-adapters"></a>네트워크 어댑터에서 DCB 사용 안 함

```
PS C:\> Disable-NetAdapterQos M1
PS C:\> Get-NetAdapterQos M1

Name         : M1
Enabled      : False
Capabilities :                       Hardware     Current
                                     --------     -------
               MacSecBypass        : NotSupported NotSupported
               DcbxSupport         : None         None
               NumTCs(Max/ETS/PFC) : 8/8/8        0/0/0  

```
## <a name="windows-powershell-commands-for-dcb"></a><a name="bkmk_wps"></a>DCB 용 Windows PowerShell 명령

Windows Server 2016 및 Windows Server 2012 r 2에 대 한 Windows PowerShell 명령 DCB 있습니다. Windows server 2016에서 Windows Server 2012 r 2에 대 한 모든 명령을 사용할 수 있습니다.

### <a name="windows-server-2016-windows-powershell-commands-for-dcb"></a>DCB 용 windows Server 2016 Windows PowerShell 명령

Windows Server 2016에 대 한 다음 항목에서는 모든 데이터 센터 브리징 \(DCB\) 서비스 품질 \(QoS\)\-특정 cmdlet에 대 한 Windows PowerShell cmdlet 설명 및 구문을 제공 합니다. 또한 cmdlet의 첫 부분에 있는 동사를 기준으로 알파벳 순서에 따라 cmdlet을 나열합니다.

- [DcbQoS 모듈](https://technet.microsoft.com/itpro/powershell/windows/dcbqos/dcbqos)

### <a name="windows-server-2012-r2-windows-powershell-commands-for-dcb"></a>DCB 용 windows Server 2012 R2 Windows PowerShell 명령

Windows Server 2012 r 2의 다음 항목에서는 모든 데이터 센터 브리징 \(DCB\) 서비스 품질 \(QoS\)\-특정 cmdlet에 대 한 Windows PowerShell cmdlet 설명 및 구문을 제공 합니다. 또한 cmdlet의 첫 부분에 있는 동사를 기준으로 알파벳 순서에 따라 cmdlet을 나열합니다.

- [Windows PowerShell의 DCB (데이터 센터 브리징) QoS (서비스 품질) Cmdlet](https://technet.microsoft.com/library/hh967440.aspx)
