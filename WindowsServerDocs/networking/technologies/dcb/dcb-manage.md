---
title: 데이터 센터 브리지 (DCB) 관리
description: 이 항목에서는 Windows PowerShell 명령을 사용 하 여 Windows Server 2016의 데이터 센터 브리지 관리 하는 방법에 알아보세요.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 1575cc7c-62a7-4add-8f78-e5d93effe93f
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: dbe9e5e4af2ddd834b5b8f38e9ffd1b403e92793
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="manage-data-center-bridging-dcb"></a>데이터 센터 브리지 (DCB) 관리

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목에서는 Windows Server 2016 또는 Windows 10을 실행 하는 컴퓨터에 설치 된 호환 DCB\ 네트워크 어댑터에 데이터 센터 브리지 \(DCB\) 구성 하도록 Windows PowerShell 명령을 사용 하는 방법에 대해 설명 합니다.

## <a name="install-dcb-in-windows-server-2016-or-windows-10"></a>Windows 10 또는 Windows Server 2016 DCB 설치

사용 하 고 DCB 설치 하는 방법에 대 한 사항에 대 한 내용은 참조 [설치 데이터 센터 브리지 (DCB) Windows Server 2016 또는 Windows 10에서](dcb-install.md)합니다.


## <a name="dcb-configurations"></a>DCB 구성 

Windows Server 2016 년 전에 모든 DCB 구성 DCB 지원 되는 모든 네트워크 어댑터를 전체적으로 적용 했습니다. 

Windows Server 2016 Global 정책 스토어 또는 개별 정책 Store\(s\) DCB 구성 적용할 수 있습니다. 개별 정책이 적용 되는 경우 모든 글로벌 정책 설정을 재정의 합니다.

다음을 수행 될 때까지 시스템 수준 교통 클래스, PFC 및 응용 프로그램 우선 순위 지정 구성 네트워크 어댑터에 적용 되지 않습니다.

1. False DCBX 의사가 비트 켜기

2. 네트워크 어댑터에서 DCB 사용 합니다. 참조 [사용 하도록 설정 하 고 네트워크 어댑터에 DCB 설정을 표시](#bkmk_enabledcb)합니다.

>[!NOTE]
>DCBX 통해 스위치에서 DCB 구성 하려는 경우 [DCBX 설정](#BKMK_DCBX_Settings)

DCBX 의사가 비트 DCB 사양에 설명 되어 있습니다. 디바이스에서 의사가 비트도 설정 됩니다 진정한, 디바이스는 DCBX 통해 원격 디바이스에서 구성에 동의 합니다. 디바이스에서 의사가 비트 false를 설정 된 경우 디바이스의 원격 디바이스의 모든 구성 시도 거부 하 고 로컬 구성에만 적용 됩니다.

Windows Server 2016에 설치 되어 있지 않으면 DCB 의사가 비트 값 관련해 서 운영 체제는 운영 체제에는 로컬 네트워크 어댑터에 적용 설정이 때문에 관련있지 않습니다. DCB이 설치 된 후 의사가 약간의 기본값이 그렇습니다. 이 디자인 네트워크 어댑터를를 계속 무엇이 든 구성 자신의 원격 피어에서 받은 있을 수 있습니다.

네트워크 어댑터 DCBX를 지원 하지 않는 경우 원격 디바이스에서 구성 받을 절대 수 있습니다. 운영 체제의 구성에서 수신 있지만 DCBX 후에 의사가 비트 false로 설정 됩니다.

## <a name="set-the-willing-bit"></a>기꺼이 비트 설정

교통 클래스, PFC, 및 응용 프로그램, 네트워크 어댑터에 우선 순위 지정 구성 운영 체제를 적용 하기 위해 하거나 간단히의 원격 디바이스에서 구성 재정의 \-있을 경우 \-다음 명령의 실행할 수 있습니다.

>[!NOTE]
>DCB Windows PowerShell 명령 이름 이름 문자열의 "DCB" 대신 "QoS" 포함 됩니다. 원활 하 게 QoS 관리 환경을 제공 하도록 Windows Server 2016 통합 되어 QoS 및 DCB 하기 때문입니다.

    
    Set-NetQosDcbxSetting -Willing $FALSE
    
    Confirm
    Are you sure you want to perform this action?
    Set-NetQosDcbxSetting -Willing $false
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"):
    

설정 의사가 약간의 상태를 표시 하려면 다음 명령을 사용할 수 있습니다.

    
    Get-NetQosDcbxSetting
    
    Willing PolicySetIfIndex IfAlias
    ------- ---------------- -------
    False   Global  
    

## <a name="dcb-configuration-on-network-adapters"></a>네트워크 어댑터에 DCB 구성

DCB 네트워크 어댑터를 사용 하면 네트워크 어댑터에 스위치를에서 전파 구성 볼 수 있습니다.

DCB 구성 다음 단계를 포함합니다.

1.  포함 된 시스템 수준 DCB 설정의 구성 합니다.

    한 합니다. 교통 관리
    
    B 합니다. 우선 순위 흐름 제어 (PFC) 설정
    
    C 합니다. 응용 프로그램 우선 순위 지정
    
    D 합니다. DCBX 설정

2. 네트워크 어댑터에 DCB을 구성 합니다.



##  <a name="dcb-traffic-class-management"></a>DCB 교통 관리

다음은 교통 관리에 대 한 Windows PowerShell 명령 예입니다.

### <a name="create-a-traffic-class"></a>교통 클래스 만들기

사용할 수는 **새로 NetQosTrafficClass** 교통 클래스 만드는 명령을 합니다.

    
    New-NetQosTrafficClass -Name SMB -Priority 4 -BandwidthPercentage 30 -Algorithm ETS
    
    Name Algorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ---- --------- ------------ -------- ---------------- -------
    SMB  ETS   30   4Global
      

기본적으로 모든 802.1 p 값은 100%의 실제 연결 대역폭에는 기본 교통 클래스에 매핑됩니다. **새로 NetQosTrafficClass** 명령은 새 교통 클래스, 가치 4 802.1 p 순위가 태그가 지정 하는 모든 패킷을에 매핑됩니다. 전송 선택 알고리즘 \(TSA\) ETS 이며 대역폭의 30% 합니다.

새 최대 7 교통 클래스 만들 수 있습니다. 기본 교통 클래스 포함 될 수도 있습니다 최대 8 교통 클래스 시스템에서. 그러나 DCB 가능 네트워크 어댑터는 클래스 하드웨어에서를 교통 많은 지원 하지 않습니다. 네트워크 어댑터에서 지원 될 것 보다 더 많은 교통 클래스 만들고 DCB 해당 네트워크 어댑터에서 사용 하는 경우 미니 드라이버는 오류 운영 체제에 보고 합니다. 오류는 이벤트 로그에 기록 됩니다.

모든 만든된 교통 클래스 대역폭 예약 합계 99% 대역폭의 초과 하지 않을 수 있습니다. 기본 교통 클래스는 항상 자체에 예약 된 대역폭 1% 이상의 있습니다.

### <a name="display-traffic-classes"></a>디스플레이 교통 클래스

사용할 수 있는 **Get NetQosTrafficClass** 교통 클래스 보려고 명령이 합니다.

    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   70   0-3,5-7  Global
    SMB ETS   30   4Global  
    
### <a name="modify-a-traffic-class"></a>교통 클래스 수정

사용할 수는 **설정 NetQosTrafficClass** 교통 클래스 만드는 명령을 합니다. 

    Set-NetQosTrafficClass -Name SMB -BandwidthPercentage 50

사용할 수 있습니다의 **Get NetQosTrafficClass** 명령을 설정을 볼 수 있습니다.

    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   50   0-3,5-7  Global
    SMB ETS   50   4Global   
    

교통 클래스를 만든 다음 해당 설정을 변경할 수 있습니다 독립적으로 합니다. 변경할 수 있는 설정은 다음과 같습니다.

1. 대역폭이 할당 \(-BandwidthPercentage\)

2. TSA (\-Algorithm\)

3. 매핑 \(-Priority\) 우선 순위 부여

### <a name="remove-a-traffic-class"></a>교통 클래스 제거

사용할 수는 **제거 NetQosTrafficClass** 교통 클래스 삭제 명령을 합니다.

>[!IMPORTANT]
>기본 교통 클래스를 제거할 수 없습니다.


    Remove-NetQosTrafficClass -Name SMB

사용할 수 있습니다의 **Get NetQosTrafficClass** 명령을 설정을 볼 수 있습니다.
    
    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   100  0-7  Global
    

교통 클래스를 제거한 후 802.1 p 가치에 매핑됩니다 기본 교통 클래스 교통 클래스를 다시 매핑할 됩니다. 기본 교통 클래스 할당 교통 클래스 제거 되 면 교통 클래스도 예약 된 모든 대역폭 반환 됩니다.

## <a name="per-network-interface-policies"></a>-네트워크 인터페이스 정책

위 예제 모든 전 세계 정책을 설정합니다. 다음은 설정 NIC 정책 다운로드 하는 방법 몇 가지 있습니다. 

"PolicySet" 필드 AdapterSpecific 전 세계의 변경합니다. AdapterSpecific 정책을 표시 되 고 인터페이스 색인 \(ifIndex\) 인터페이스 이름 \(ifAlias\)도 표시 됩니다.

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

## <a name="priority-flow-control-settings"></a>우선 순위 플로 컨트롤 설정은 다음과 같습니다.

플로 제어 우선 순위 설정에 대 한 명령 예입니다. 개별 어댑터에 대 한 이러한 설정은 지정 수 있습니다.

### <a name="enable-and-display-priority-flow-control-for-global-and-interface-specific-use-cases"></a>사용 하 고 전 세계 및 인터페이스 특정 디스플레이 우선 순위 플로 제어 사례 사용

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


### <a name="disable-priority-flow-control-global-and-interface-specific"></a>우선 순위 흐름 제어를 사용 하지 않도록 설정 (전 세계와 관련 인터페이스)

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

##  <a name="application-priority-assignment"></a>응용 프로그램 우선 순위 지정

다음은 우선 순위 지정의 예입니다.

### <a name="create-qos-policy"></a>정책 QoS 만들기

```
PS C:\> New-NetQosPolicy -Name "SMB Policy" -PriorityValue8021Action 4

Name           : SMB Policy
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
JobObject      :
PriorityValue  : 4

```

이전 명령을 SMB 새 정책을 만듭니다. – SMB TCP 포트 445 (SMB 예약된)와 일치 하는 받은 편지함 필터입니다. 패킷이 TCP 포트 802.1 p 4 하기 전에 값이 운영 체제 태그가 지정 됩니다 445로 전송 패킷이는 네트워크 미니 드라이버를 전달 됩니다.

-SMB, 뿐만 아니라 다른 기본 필터 – iSCSI (일치 하는 TCP 포트 3260),-NFS (일치 하는 TCP 포트 2049),-LiveMigration (일치 하는 TCP 포트 6600),-(EtherType 0x8906 일치) FCOE 및 – NetworkDirect 포함 됩니다.

NetworkDirect 모든 네트워크 어댑터에 RDMA 구현 위에 작성 된 추상화 계층입니다. – NetworkDirect 네트워크 직접 포트가 따라야 합니다.

기본 필터 뿐만 아니라 응용 프로그램의 실행 파일 이름 (예: 첫 번째 아래의 예제) 하거나 IP 주소, 포트 또는 프로토콜 (같이 두 번째 예제에서) 여 트래픽을 분류 수 있습니다.

**실행 파일 이름에서**

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

### <a name="display-qos-policy"></a>디스플레이 QoS 정책

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

### <a name="modify-qos-policy"></a>수정 QoS 정책

아래와 같이 QoS 정책의 수정할 수 있습니다.


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

### <a name="remove-qos-policy"></a>QoS 정책을 제거합니다

```
PS C:\> Remove-NetQosPolicy -Name "Network Management"

Confirm
Are you sure you want to perform this action?
Remove-NetQosPolicy -Name "Network Management" -Store GPO:localhost
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): y  

```

## <a name="dcb-configuration-on-network-adapters"></a>네트워크 어댑터에 DCB 구성

네트워크 어댑터에 DCB 구성은 위에서 설명한 시스템 수준 DCB 구성 다릅니다. 

Windows Server 2016에 DCB 설치 되어 있는지 여부에 관계 없이 언제 든 지 뒤 다음 명령의 실행할 수 있습니다. 

스위치를에서 DCB 구성 하 고 네트워크 어댑터에 대 한 구성 전파 DCBX에 의존 하는 경우 어떤 구성 수신 하 고 네트워크 어댑터에서 운영 체제에 적용 DCB 네트워크 어댑터에서 사용 하도록 설정한 후에 확인할 수 있습니다.

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

### <a name="disable-dcb-on-network-adapters"></a>네트워크 어댑터에 DCB 사용 안 함

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
## <a name="bkmk_wps"></a>Windows PowerShell DCB에 대 한 명령

Windows Server 2016 및 Windows Server 2012 r 2에 대 한 명령 DCB Windows PowerShell 가지가 있습니다. Windows Server 2016에 Windows Server 2012 r 2에 대 한 모든 명령을 사용할 수 있습니다.

### <a name="windows-server-2016-windows-powershell-commands-for-dcb"></a>Windows Server 2016 Windows PowerShell DCB에 대 한 명령

Windows Server 2016에 대 한 다음 항목에 대 한 모든 데이터 센터 브리지 \(DCB\) Windows PowerShell cmdlet 설명 및 구문 제공 서비스 품질 \ (QoS\) \-specific cmdlet 합니다. Cmdlet 동사 cmdlet의 왼쪽 끝에 따라 사전순으로 나열 됩니다.

- [DcbQoS 모듈](https://technet.microsoft.com/itpro/powershell/windows/dcbqos/dcbqos)

### <a name="windows-server-2012-r2-windows-powershell-commands-for-dcb"></a>Windows Server 2012 r 2 Windows PowerShell 명령을 DCB

Windows Server 2012 r 2에 대 한 다음 항목에 대 한 모든 데이터 센터 브리지 \(DCB\) Windows PowerShell cmdlet 설명 및 구문 제공 서비스 품질 \ (QoS\) \-specific cmdlet 합니다. Cmdlet 동사 cmdlet의 왼쪽 끝에 따라 사전순으로 나열 됩니다.

- [데이터 센터에서 Windows PowerShell Cmdlet 서비스의 품질 (DCB) 브리지](https://technet.microsoft.com/library/hh967440.aspx)
