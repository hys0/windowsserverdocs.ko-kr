---
title: 관리 데이터 센터 브리징 (DCB)
description: 이 항목에서는 Windows PowerShell 명령을 사용 하 여 Windows Server 2016의 데이터 센터 브리징를 관리 하는 방법에 대 한 지침을 제공 합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 1575cc7c-62a7-4add-8f78-e5d93effe93f
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3912bb6048a06a4656b5b27ccec8f8fb3f5b114b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847414"
---
# <a name="manage-data-center-bridging-dcb"></a>관리 데이터 센터 브리징 (DCB)

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 Windows PowerShell 명령을 사용 하 여 데이터 센터 브리징을 구성 하는 방법에 대 한 지침을 제공 \(DCB\) DCB에서\-호환 되는 네트워크 어댑터 중 하나를 실행 하는 컴퓨터에 설치 된 Windows Server 2016 또는 Windows 10입니다.

## <a name="install-dcb-in-windows-server-2016-or-windows-10"></a>Windows Server 2016 또는 Windows 10에서 DCB를 설치 합니다.

사용 하 여 및 DCB를 설치 하는 방법에 대 한 필수 구성 요소에 대 한 내용은 참조 하세요 [설치 센터 브리징 (DCB (데이터) Windows Server 2016 또는 Windows 10에서](dcb-install.md)합니다.


## <a name="dcb-configurations"></a>DCB 구성 

Windows Server 2016 이전의 모든 DCB 구성 DCB를 지 원하는 모든 네트워크 어댑터에 보편적으로 적용 되었습니다. 

Windows Server 2016에서 구성을 적용할 수 있습니다 DCB 전역 정책 저장소 또는 개별 정책 저장소\(s\)입니다. 개별 정책이 적용 된 경우 모든 전역 정책 설정을 재정의 됩니다.

다음을 수행 될 때까지 시스템 수준에서 트래픽 클래스, PFC 및 응용 프로그램 우선 순위 할당의 구성은 네트워크 어댑터에 적용 되지 않습니다.

1. False로 DCBX 감수 비트를 설정 합니다.

2. 네트워크 어댑터에 DCB를 사용 하도록 설정 합니다. 참조 [을 사용 하도록 설정 하 고 네트워크 어댑터에 DCB 설정을 표시](#bkmk_enabledcb)합니다.

>[!NOTE]
>DCBX 통해 스위치에서 DCB를 구성 하려는 경우 참조 [DCBX 설정](#BKMK_DCBX_Settings)

DCBX 감수 비트 DCB 사양에 설명 되어 있습니다. 경우는 기꺼이 장치의 비트가 true 이면 장치를 통해 DCBX 원격 장치에서 구성을 적용 하려고 합니다. 장치의 감수 비트가 false로 설정 된 경우 장치가 원격 장치에서 모든 구성 시도 거부 하 고 로컬 구성에만 적용 됩니다.

Windows Server 2016에서 DCB를 설치 하지 않은 경우 감수 비트 값 관련해 서 운영 체제는 운영 체제 설정이 없는 로컬 네트워크 어댑터에 적용 하기 때문에 관련 아닙니다. DCB를 설치한 후 감수 비트의 기본값은 true입니다. 이 디자인을 사용 하면 네트워크 어댑터는 원격 피어 로부터 받았을 수 있습니다 하는 모든 구성 되도록 합니다.

네트워크 어댑터를 DCBX을 지원 하지 않으면 원격 장치에서 구성 되지 수신지 않습니다. 운영 체제에서 구성에서 수신 하지만 DCBX 해야만 감수 비트가 false로 설정 합니다.

## <a name="set-the-willing-bit"></a>감수 비트 설정

트래픽 클래스와 PFC, 네트워크 어댑터에서 응용 프로그램 우선 순위 할당의 운영 체제 구성을 적용할 또는 원격 장치에서 구성을 재정의 하기만 \-있는 경우 \-다음 명령을 실행할 수 있습니다.

>[!NOTE]
>DCB Windows PowerShell 명령 이름 이름 문자열에 "DCB" 대신 "QoS"를 포함 합니다. QoS 및 DCB를 원활 하 게 QoS 관리 환경을 제공 하기 위해 Windows Server 2016에 통합 되어 때문입니다.

    
    Set-NetQosDcbxSetting -Willing $FALSE
    
    Confirm
    Are you sure you want to perform this action?
    Set-NetQosDcbxSetting -Willing $false
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"):
    

설정 하려는 비트의 상태를 표시 하려면 다음 명령을 사용할 수 있습니다.

    
    Get-NetQosDcbxSetting
    
    Willing PolicySetIfIndex IfAlias
    ------- ---------------- -------
    False   Global  
    

## <a name="dcb-configuration-on-network-adapters"></a>네트워크 어댑터에 DCB 구성

네트워크 어댑터에서 DCB를 사용 하도록 설정 스위치에서 네트워크 어댑터에 전파 구성을 볼 수 있습니다.

DCB 구성에는 다음 단계를 포함합니다.

1.  DCB 설정을 포함 하는 시스템 수준에서 구성 합니다.

    a. 트래픽 클래스 관리
    
    b. 우선 순위 흐름 제어 (PFC) 설정
    
    다. 응용 프로그램 우선 순위 할당
    
    d. DCBX 설정

2. 네트워크 어댑터에 대해 DCB를 구성 합니다.



##  <a name="dcb-traffic-class-management"></a>DCB 트래픽 클래스 관리

다음은 트래픽 클래스 관리용 Windows PowerShell 명령 예제입니다.

### <a name="create-a-traffic-class"></a>트래픽 클래스 만들기

사용할 수는 **새로 만들기-NetQosTrafficClass** 트래픽 클래스를 만드는 명령입니다.

    
    New-NetQosTrafficClass -Name SMB -Priority 4 -BandwidthPercentage 30 -Algorithm ETS
    
    Name Algorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ---- --------- ------------ -------- ---------------- -------
    SMB  ETS   30   4Global
      

기본적으로 모든 802.1p 값에는 물리적 링크의 대역폭의 100%를 기본 트래픽 클래스에 매핑됩니다. 합니다 **새로 만들기-NetQosTrafficClass** 매핑되는 모든 패킷 802.1p 우선 순위 태그가 지정 되는 값 4, 명령은 새 트래픽 클래스를 만듭니다. 전송 선택 알고리즘 \(TSA\) ETS 있고 대역폭의 30%입니다.

최대 7 새 트래픽 클래스를 만들 수 있습니다. 기본 트래픽 클래스를 포함 하 여에 있을 수 있습니다 최대 8 트래픽 클래스 시스템입니다. 그러나 DCB 가능 네트워크 어댑터를은 하드웨어에서 클래스를 트래픽 대부분을 지원 하지 않습니다. 네트워크 어댑터에서 수용할 수 보다 더 많은 트래픽 클래스를 만들고 해당 네트워크 어댑터에서 DCB를 사용 하도록 설정한을 미니 포트 드라이버의 운영 체제 오류를 보고 합니다. 이 오류는 이벤트 로그에 기록 됩니다.

모든 생성된 된 트래픽 클래스에 대 한 대역폭 예약 총 대역폭의 99%를 초과할 수 없습니다. 기본 트래픽 클래스에는 항상 자체에 대 한 예약 된 대역폭의 1% 이상에 있습니다.

### <a name="display-traffic-classes"></a>트래픽 클래스를 표시 합니다.

사용할 수는 **Get-netqostrafficclass** 트래픽 클래스를 보려면 명령입니다.

    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   70   0-3,5-7  Global
    SMB ETS   30   4Global  
    
### <a name="modify-a-traffic-class"></a>트래픽 클래스를 수정 합니다.

사용할 수는 **집합 NetQosTrafficClass** 트래픽 클래스를 만드는 명령입니다. 

    Set-NetQosTrafficClass -Name SMB -BandwidthPercentage 50

사용할 수는 **Get-netqostrafficclass** 설정을 확인 하는 명령입니다.

    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   50   0-3,5-7  Global
    SMB ETS   50   4Global   
    

트래픽 클래스를 만든 후 해당 설정을 변경할 수 있습니다 독립적으로 유지 합니다. 변경할 수 있습니다 설정에는 다음이 포함 됩니다.

1. 대역폭 할당 \(-BandwidthPercentage\)

2. TSA (\-알고리즘\)

3. 우선 순위 매핑 \(-우선 순위\)

### <a name="remove-a-traffic-class"></a>트래픽 클래스를 제거 합니다.

사용할 수는 **제거 NetQosTrafficClass** 트래픽 클래스를 삭제 하는 명령입니다.

>[!IMPORTANT]
>기본 트래픽 클래스를 제거할 수 없습니다.


    Remove-NetQosTrafficClass -Name SMB

사용할 수는 **Get-netqostrafficclass** 설정을 확인 하는 명령입니다.
    
    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   100  0-7  Global
    

트래픽 클래스를 제거한 후 802.1p 값에 매핑된 기본 트래픽 클래스를 트래픽 클래스는 다시 매핑됩니다. 트래픽 클래스에 대 한 예약 된 모든 대역폭 트래픽 클래스를 제거할 때 기본 트래픽 클래스 할당에 반환 됩니다.

## <a name="per-network-interface-policies"></a>각 네트워크 인터페이스 정책

위의 예에서는 모든 전역 정책을 설정합니다. 다음은 설정 NIC 당 정책 가져오기 하는 방법의 예입니다. 

"PolicySet" 필드가 AdapterSpecific 전역에서 변경 됩니다. 경우 AdapterSpecific 정책이 표시 됩니다. 이러한 인터페이스 색인 \(ifIndex\) 이름과 인터페이스 \(ifAlias\) 도 표시 됩니다.

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

다음은 우선 순위 흐름 제어 설정에 대 한 명령 예제입니다. 개별 어댑터에 대 한 이러한 설정은 지정할 수도 있습니다.

### <a name="enable-and-display-priority-flow-control-for-global-and-interface-specific-use-cases"></a>설정 및 전역 및 특정 인터페이스에 대 한 표시 우선 순위 흐름 제어 사용 사례

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


### <a name="disable-priority-flow-control-global-and-interface-specific"></a>우선 순위 흐름 제어를 사용 하지 않도록 설정 (전역 및 특정 인터페이스)

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

다음은 우선 순위 할당의 예입니다.

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

이전 명령은 SMB에 대 한 새 정책을 만듭니다. – SMB는 TCP 포트 445 (SMB에 대 한 예약 됨된)와 일치 하는 수신함 필터. 하면 패킷이 네트워크 미니 포트 드라이버에 패킷을 전달 되기 전에 802.1p 값 4 사용 하 여 운영 체제에서 태그 되도록 445 TCP 포트에 전송 됩니다.

– SMB 외에도 다른 기본 필터 – iSCSI (일치 하는 TCP 포트 3260) ","-NFS (일치 하는 TCP 포트 2049) ","-LiveMigration (일치 하는 TCP 포트 6600) ","-FCOE (EtherType 0x8906 일치) "및" – NetworkDirect를 포함 합니다.

NetworkDirect는 추상 계층 네트워크 어댑터에서 RDMA 구현을 기반으로 만듭니다. Network Direct 포트를 통해 – NetworkDirect은 따라야 합니다.

기본 필터 외에도 (첫 번째 예와 아래), 응용 프로그램의 실행 파일 이름이 나 IP 주소, 포트 또는 프로토콜 (에서처럼 두 번째 예제) 트래픽을 분류할 수 있습니다.

**실행 파일 이름으로**

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


**IP 주소 포트 또는 프로토콜**

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

### <a name="modify-qos-policy"></a>QoS 정책을 수정합니다

아래와 같이 QoS 정책을 수정할 수 있습니다.


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

## <a name="dcb-configuration-on-network-adapters"></a>네트워크 어댑터에 DCB 구성

네트워크 어댑터에 DCB 구성은 위에서 설명한 시스템 수준에서 DCB 구성에 무관 합니다. 

DCB는 Windows Server 2016의 설치 여부에 관계 없이 다음 명령을 항상 실행할 수 있습니다. 

스위치에서 DCB를 구성 하 고 네트워크 어댑터에 구성을 전파 하는 데 DCBX 의존 하는 경우에 어떤 구성을 수신 하 고 네트워크 어댑터에 DCB를 사용 하도록 설정 하면 운영 체제 측면에서 네트워크 어댑터에 적용을 검사할 수 있습니다.

###  <a name="bkmk_enabledcb"></a>사용 하도록 설정 하 고 네트워크 어댑터에 DCB 설정 표시

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

### <a name="disable-dcb-on-network-adapters"></a>네트워크 어댑터에서 DCB를 사용 하지 않도록 설정

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
## <a name="bkmk_wps"></a>DCB에 대 한 Windows PowerShell 명령

Windows Server 2016 및 Windows Server 2012 R2에 대 한 DCB Windows PowerShell 명령이 있습니다. Windows Server 2016에서 Windows Server 2012 R2에 대 한 모든 명령을 사용할 수 있습니다.

### <a name="windows-server-2016-windows-powershell-commands-for-dcb"></a>DCB에 대 한 Windows Server 2016 Windows PowerShell 명령

다음 항목에서는 Windows Server 2016에 대 한 모든 데이터 센터 브리징에 대 한 Windows PowerShell cmdlet 설명과 구문을 제공 \(DCB\) 서비스 품질 \(QoS\)\-관련 cmdlet. cmdlet은 cmdlet의 시작 부분에 있는 동사에 따라 사전순으로 나열됩니다.

- [DcbQoS Module](https://technet.microsoft.com/itpro/powershell/windows/dcbqos/dcbqos)

### <a name="windows-server-2012-r2-windows-powershell-commands-for-dcb"></a>DCB에 대 한 Windows Server 2012 R2 Windows PowerShell 명령

다음 항목에서는 Windows Server 2012 R2에 대 한 모든 데이터 센터 브리징에 대 한 Windows PowerShell cmdlet 설명과 구문을 제공 \(DCB\) 서비스 품질 \(QoS\)\-관련 cmdlet. cmdlet은 cmdlet의 시작 부분에 있는 동사에 따라 사전순으로 나열됩니다.

- [데이터 센터 브리징 (DCB) 품질의 Windows PowerShell의 QoS (서비스) Cmdlet](https://technet.microsoft.com/library/hh967440.aspx)
