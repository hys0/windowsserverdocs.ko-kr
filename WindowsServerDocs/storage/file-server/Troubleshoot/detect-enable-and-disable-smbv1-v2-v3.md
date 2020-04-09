---
title: Windows에서 SMBv1, SMBv2 및 SMBv3를 검색, 활성화 및 비활성화 하는 방법
description: Windows 클라이언트 및 서버 환경에서 서버 메시지 블록 프로토콜 (SMBv1, SMBv2 및 SMBv3)을 사용 하거나 사용 하지 않도록 설정 하는 방법을 설명 합니다.
author: Deland-Han
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: d6c47843dedaf45842f70d1bb408b59d63c03eb4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80815506"
---
# <a name="how-to-detect-enable-and-disable-smbv1-smbv2-and-smbv3-in-windows"></a>Windows에서 SMBv1, SMBv2 및 SMBv3를 검색, 활성화 및 비활성화 하는 방법

## <a name="summary"></a>요약

이 문서에서는 SMB 클라이언트 및 서버 구성 요소에서 smb (서버 메시지 블록) 버전 1 (SMBv1), SMBv2 (SMB 버전 2) 및 SMBv3 (smb 버전 3)를 사용 하거나 사용 하지 않도록 설정 하는 방법을 설명 합니다. 

> [!IMPORTANT]
> SMBv2 또는 SMBv3를 **사용 하지 않도록 설정 하는** 것이 좋습니다. SMBv2 또는 SMBv3을 임시 문제 해결 수단 으로만 사용 하지 않도록 설정 합니다. SMBv2 또는 SMBv3를 사용 하지 않도록 설정 하지 마세요.  

Windows 7 및 Windows Server 2008 r 2에서 SMBv2를 사용 하지 않도록 설정 하면 다음 기능이 비활성화 됩니다. 
 
- Request 그래야만-단일 네트워크 요청으로 여러 SMB 2 요청을 보낼 수 있습니다.    
- 더 큰 읽기 및 쓰기-더 빠른 네트워크 사용    
- 폴더 및 파일 속성의 캐싱-클라이언트는 폴더 및 파일의 로컬 복사본을 유지 합니다.    
- 영 속 핸들-일시적으로 연결이 끊긴 경우 서버에 대 한 연결을 투명 하 게 다시 연결할 수 있습니다.    
- 향상 된 메시지 서명-HMAC SHA-256은 MD5를 해싱 알고리즘으로 바꿉니다.    
- 파일 공유에 대 한 향상 된 확장성-서버당 사용자, 공유 및 열린 파일 수 크게 증가    
- 기호화 된 링크 지원    
- 클라이언트 oplock 임대 모델-클라이언트와 서버 간에 전송 되는 데이터를 제한 하 고 대기 시간이 긴 네트워크에서 성능을 향상 시키고 SMB 서버 확장성을 높입니다.    
- 대량 MTU 지원-gigabye (GB) 이더넷의 전체 사용    
- 향상 된 에너지 효율성-서버에 대 한 열린 파일이 있는 클라이언트는 절전 모드로 전환할 수 있습니다.    

Windows 8, Windows 8.1, Windows 10, Windows Server 2012 및 Windows Server 2016에서 SMBv3를 사용 하지 않도록 설정 하면 다음 기능 및 이전 목록에서 설명 하는 SMBv2 기능이 비활성화 됩니다. 
 
- 투명 한 장애 조치 (failover)-유지 관리 또는 장애 조치 (failover) 중 클러스터 노드에 중단 없이 클라이언트 다시    
- Scale Out – 모든 파일 클러스터 노드의 공유 데이터에 대 한 동시 액세스     
- 다중 채널-클라이언트와 서버 간에 여러 경로를 사용할 수 있는 경우 네트워크 대역폭 및 내결함성 집계  
- SMB 다이렉트 – 짧은 대기 시간 및 낮은 CPU 사용률을 포함 하 여 매우 높은 성능에 대해 RDMA 네트워킹 지원을 추가 합니다.    
- 암호화 – 종단 간 암호화를 제공 하 고 신뢰할 수 없는 네트워크의 도청 으로부터 보호 합니다.    
- 디렉터리 임대-캐싱을 통해 지점의 응용 프로그램 응답 시간을 향상 시킵니다.    
- 성능 최적화-작은 임의 읽기/쓰기 i/o에 대 한 최적화

##  <a name="more-information"></a>자세한 내용

SMBv2 프로토콜은 Windows Vista 및 Windows Server 2008에서 도입 되었습니다.

SMBv3 프로토콜은 Windows 8 및 Windows Server 2012에서 도입 되었습니다.

SMBv2 및 SMBv3 기능에 대 한 자세한 내용은 다음 문서를 참조 하세요.

[Server Message Block 개요](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831795(v=ws.11))

[SMB의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff625695(v=ws.10))  

## <a name="how-to-gracefully-remove-smb-v1-in-windows-81-windows-10-windows-2012-r2-and-windows-server-2016"></a>Windows 8.1, Windows 10, Windows 2012 R2 및 Windows Server 2016에서 SMB v1을 적절 하 게 제거 하는 방법

#### <a name="windows-server-2012-r2--2016-powershell-methods"></a>Windows Server 2012 R2 & 2016: PowerShell 메서드

##### <a name="smb-v1"></a>SMB v1

- 탐색 

  ```PowerShell
  Get-WindowsFeature FS-SMB1
  ```

- 하지 

  ```PowerShell
  Disable-WindowsOptionalFeature -Online -FeatureName smb1protocol
  ```

- 활성화 

  ```PowerShell
  Enable-WindowsOptionalFeature -Online -FeatureName smb1protocol
  ```

##### <a name="smb-v2v3"></a>SMB v2/v3

- 탐색
  
  ```PowerShell
  Get-SmbServerConfiguration | Select EnableSMB2Protocol
  ```

- 하지

  ```PowerShell
  Set-SmbServerConfiguration -EnableSMB2Protocol $false
  ```

- 활성화

  ```PowerShell
  Set-SmbServerConfiguration -EnableSMB2Protocol $true 
  ```

#### <a name="windows-server-2012-r2-and-windows-server-2016-server-manager-method-for-disabling-smb"></a>Windows Server 2012 R2 및 Windows Server 2016: SMB를 사용 하지 않도록 설정 하는 서버 관리자 방법

##### <a name="smb-v1"></a>SMB v1

![서버 관리자-Dashboard 메서드](media/detect-enable-and-disable-smbv1-v2-v3-1.png)

#### <a name="windows-81-and-windows-10-powershell-method"></a>Windows 8.1 및 Windows 10: PowerShell 메서드

##### <a name="smb-v1-protocol"></a>SMB v1 프로토콜

- 탐색 
  
  ```PowerShell
  Get-WindowsOptionalFeature –Online –FeatureName SMB1Protocol
  ```

- 하지 

  ```PowerShell
  Disable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol
  ```

- 활성화 

  ```PowerShell
  Enable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol
  ```

##### <a name="smb-v2v3protocol"></a>SMB v2/v3 프로토콜

- 탐색 
  
  ```PowerShell
  Get-SmbServerConfiguration | Select EnableSMB2Protocol
  ```

- 하지 
  
  ```PowerShell
  Set-SmbServerConfiguration –EnableSMB2Protocol $false
  ```

- 활성화

  ```PowerShell
  Set-SmbServerConfiguration –EnableSMB2Protocol $true
  ```

#### <a name="windows-81-and-windows-10-add-or-remove-programs-method"></a>Windows 8.1 및 Windows 10: 프로그램 추가/제거 방법

![프로그램 추가/제거 클라이언트 방법](media/detect-enable-and-disable-smbv1-v2-v3-2.png)

## <a name="how-to-detect-status-enable-and-disable-smb-protocols-on-the-smb-server"></a>SMB 서버의 상태를 검색 하 고, SMB 프로토콜을 사용 하도록 설정 하 고, 사용 하지 않도록 설정 하는 방법

### <a name="for-windows-8-and-windows-server-2012"></a>Windows 8 및 Windows Server 2012

Windows 8 및 Windows Server 2012에는 새로운 **SMBServerConfiguration** windows PowerShell cmdlet이 도입 되었습니다. Cmdlet을 사용 하면 서버 구성 요소에서 SMBv1, SMBv2 및 SMBv3 프로토콜을 사용 하거나 사용 하지 않도록 설정할 수 있습니다.  

> [!NOTE]   
> Windows 8 또는 Windows Server 2012에서 SMBv2를 사용 하거나 사용 하지 않도록 설정 하는 경우 SMBv3도 사용 하거나 사용 하지 않도록 설정 됩니다. 이 동작은 이러한 프로토콜이 같은 스택을 공유 하기 때문에 발생 합니다.     

**SMBServerConfiguration** cmdlet을 실행 한 후에는 컴퓨터를 다시 시작 하지 않아도 됩니다. 

##### <a name="smb-v1-on-smb-server"></a>SMB 서버의 SMB v1

- 탐색 
  
  ```PowerShell
  Get-SmbServerConfiguration | Select EnableSMB1Protocol
  ```

- 하지 

  ```PowerShell
  Set-SmbServerConfiguration -EnableSMB1Protocol $false
  ```

- 활성화 
  ```PowerShell
  Set-SmbServerConfiguration -EnableSMB1Protocol $true
  ```

자세한 내용은 [Microsoft의 서버 저장소](https://techcommunity.microsoft.com/t5/Storage-at-Microsoft/Stop-using-SMB1/ba-p/425858)를 참조 하세요. 
##### <a name="smb-v2v3-on-smb-server"></a>SMB 서버에서 SMB v2/v3

- 탐색

  ```PowerShell
  Get-SmbServerConfiguration | Select EnableSMB2Protocol
  ```

- 하지 
  
  ```PowerShell
  Set-SmbServerConfiguration -EnableSMB2Protocol $false
  ```

- 활성화
  
  ```PowerShell
  Set-SmbServerConfiguration -EnableSMB2Protocol $true
  ```

### <a name="for-windows-7-windows-server-2008-r2-windows-vista-and-windows-server-2008"></a>Windows 7, windows Server 2008 R2, Windows Vista 및 Windows Server 2008의 경우

Windows 7, Windows Server 2008 R2, Windows Vista 또는 Windows Server 2008 SMB 서버에서 SMB 프로토콜을 사용 하거나 사용 하지 않도록 설정 하려면 Windows PowerShell 또는 레지스트리 편집기를 사용 합니다. 

#### <a name="powershell-methods"></a>PowerShell 메서드

> [!NOTE]
> 이 방법에는 powershell 2.0 이상 버전이 필요 합니다.

##### <a name="smb-v1-on-smb-server"></a>SMB 서버의 SMB v1

탐색

```PowerShell
Get-Item HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters | ForEach-Object {Get-ItemProperty $_.pspath}
```

기본 구성 = 사용 (레지스트리 키가 만들어지지 않음). 따라서 SMB1 값이 반환 되지 않습니다.

하지

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB1 -Type DWORD -Value 0 –Force
```

활성화  

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB1 -Type DWORD -Value 1 –Force
```  

**참고** 이러한 변경을 수행한 후에는 컴퓨터를 다시 시작 해야 합니다. 자세한 내용은 [Microsoft의 서버 저장소](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)를 참조 하세요. 
##### <a name="smb-v2v3-on-smb-server"></a>SMB 서버에서 SMB v2/v3

탐색  

```PowerShell
Get-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters | ForEach-Object {Get-ItemProperty $_.pspath} 
```

하지

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB2 -Type DWORD -Value 0 –Force  
```

활성화

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB2 -Type DWORD -Value 1 –Force 
```

> [!NOTE]
> 이러한 변경을 수행한 후에는 컴퓨터를 다시 시작 해야 합니다. 

#### <a name="registry-editor"></a>레지스트리 편집기

> [!IMPORTANT]
> 이 섹션의 단계를 신중하게 따릅니다. 레지스트리를 잘못 수정하면 심각한 문제가 발생할 수 있습니다. 수정하기 전에, 문제가 발생할 경우를 대비하여 [복원을 위해 레지스트리를 백업](https://support.microsoft.com/help/322756)해 두세요.
 
SMB 서버에서 SMBv1를 사용 하거나 사용 하지 않도록 설정 하려면 다음 레지스트리 키를 구성 합니다.

**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters**

```
Registry entry: SMB1
REG_DWORD: 0 = Disabled
REG_DWORD: 1 = Enabled
Default: 1 = Enabled (No registry key is created)
```

SMB 서버에서 SMBv2를 사용 하거나 사용 하지 않도록 설정 하려면 다음 레지스트리 키를 구성 합니다. 

**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters**

```
Registry entry: SMB2
REG_DWORD: 0 = Disabled
REG_DWORD: 1 = Enabled
Default: 1 = Enabled (No registry key is created) 
```

> [!NOTE]
> 변경한 후에는 컴퓨터를 다시 시작 해야 합니다. 

## <a name="how-to-detect-status-enable-and-disable-smb-protocols-on-the-smb-client"></a>SMB 클라이언트에서 상태를 검색 하 고 SMB 프로토콜을 사용 하도록 설정 하 고 해제 하는 방법

### <a name="for-windows-vista-windows-server-2008-windows-7-windows-server-2008-r2-windows-8-and-windows-server-2012"></a>Windows Vista, windows Server 2008, windows 7, Windows Server 2008 R2, Windows 8 및 Windows Server 2012의 경우

> [!NOTE]
> Windows 8 또는 Windows Server 2012에서 SMBv2를 사용 하거나 사용 하지 않도록 설정 하는 경우 SMBv3도 사용 하거나 사용 하지 않도록 설정 됩니다. 이 동작은 이러한 프로토콜이 같은 스택을 공유 하기 때문에 발생 합니다. 

##### <a name="smb-v1-on-smb-client"></a>SMB 클라이언트의 SMB v1

- 검색
  
  ```cmd
  sc.exe qc lanmanworkstation
  ```

- 하지
  
  ```cmd
  sc.exe config lanmanworkstation depend= bowser/mrxsmb20/nsi
  sc.exe config mrxsmb10 start= disabled
  ```

- 활성화

  ```cmd
  sc.exe config lanmanworkstation depend= bowser/mrxsmb10/mrxsmb20/nsi
  sc.exe config mrxsmb10 start= auto
  ```

자세한 내용은 [Microsoft 서버 저장소](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/) 를 참조 하세요. 
##### <a name="smb-v2v3-on-smb-client"></a>SMB 클라이언트의 SMB v2/v3

- 탐색

  ```cmd
  sc.exe qc lanmanworkstation
  ```

- 하지

  ```cmd
  sc.exe config lanmanworkstation depend= bowser/mrxsmb10/nsi
  sc.exe config mrxsmb20 start= disabled 
  ```

- 활성화

  ```cmd
  sc.exe config lanmanworkstation depend= bowser/mrxsmb10/mrxsmb20/nsi
  sc.exe config mrxsmb20 start= auto
  ```

> [!NOTE]
> - 관리자 권한 명령 프롬프트에서 다음 명령을 실행 해야 합니다.    
> - 이러한 변경을 수행한 후에는 컴퓨터를 다시 시작 해야 합니다.    
 

## <a name="disable-smbv1-server-with-group-policy"></a>그룹 정책에서 SMBv1 서버 사용 안 함

이 절차에서는 레지스트리에서 다음과 같은 새 항목을 구성 합니다.

**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters** 

- 레지스트리 항목: **SMB1** 
- REG_DWORD: **0** = 사용 안 함   

그룹 정책를 사용 하 여이를 구성 하려면 다음 단계를 수행 합니다.
 
1. 열기는 **그룹 정책 관리 콘솔**합니다. 새 기본 설정 항목을 추가할 그룹 정책 개체를 마우스 오른쪽 단추로 클릭한 다음 **편집**을 클릭합니다.

2. 콘솔 트리의 **컴퓨터 구성**에서 **기본 설정** 폴더를 확장 한 다음 **Windows 설정** 폴더를 확장 합니다.

3. **레지스트리** 노드를 마우스 오른쪽 단추로 클릭 하 고 **새로 만들기**를 가리킨 다음 **레지스트리 항목**을 선택 합니다.

   ![레지스트리-새 레지스트리 항목](media/detect-enable-and-disable-smbv1-v2-v3-3.png)    
 
**새 레지스트리 속성**대화 상자에서 다음을 선택 합니다. 
 
- **작업**: 만들기    
- **Hive**: HKEY_LOCAL_MACHINE    
- **키 경로**: SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters    
- **값 이름**: SMB1    
- **값 형식**: REG_DWORD    
- **값 데이터**: 0    
 
![새 레지스트리 속성-일반](media/detect-enable-and-disable-smbv1-v2-v3-4.png)

이렇게 하면 SMBv1 서버 구성 요소가 사용 되지 않습니다. 이 그룹 정책는 도메인에 필요한 모든 워크스테이션, 서버 및 도메인 컨트롤러에 적용 해야 합니다.

> [!NOTE]
>지원 되지 않는 운영 체제 또는 선택한 제외 (예: Windows XP)를 제외 하도록  [WMI 필터](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc947846(v=ws.10)) 를 설정할 수도 있습니다.

> [!IMPORTANT]
> 레거시 Windows XP 또는 이전 버전의 Linux 및 타사 시스템 (SMBv2 또는 SMBv3를 지원 하지 않음)이 SMB v1을 사용 하지 않도록 설정 된 SYSVOL 또는 다른 파일 공유에 대 한 액세스를 요구 하는 경우에는 주의 해야 합니다.     

## <a name="disable-smbv1-client-with-group-policy"></a>그룹 정책에서 SMBv1 Client 사용 안 함

SMBv1 client를 사용 하지 않도록 설정 하려면 서비스 레지스트리 키를 업데이트 하 여 **MRxSMB10** 시작을 사용 하지 않도록 설정한 다음 **MRxSMB10** 에 대 한 종속성을 **LanmanWorkstation** 에 대 한 항목에서 제거 하 여 **MRxSMB10** 를 먼저 시작 하지 않고 정상적으로 시작할 수 있도록 해야 합니다.

그러면 레지스트리에서 다음 2 개 항목의 기본값이 업데이트 되 고 바뀝니다. 

**HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\services\mrxsmb10** 

레지스트리 항목: **시작** REG_DWORD: **4**= 사용 안 함

**HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Services\LanmanWorkstation** 

레지스트리 항목: **DependOnService** REG_MULTI_SZ: **"브라우저", "MRxSmb20", "NSI"**   

> [!NOTE]
>이제 종속성으로 제거 되는 기본 포함 MRxSMB10를  합니다.

그룹 정책를 사용 하 여이를 구성 하려면 다음 단계를 수행 합니다.
 
1. 열기는 **그룹 정책 관리 콘솔**합니다. 새 기본 설정 항목을 추가할 그룹 정책 개체를 마우스 오른쪽 단추로 클릭한 다음 **편집**을 클릭합니다.

2. 콘솔 트리의 **컴퓨터 구성**에서 **기본 설정** 폴더를 확장 한 다음 **Windows 설정** 폴더를 확장 합니다.

3. **레지스트리** 노드를 마우스 오른쪽 단추로 클릭 하 고 **새로 만들기**를 가리킨 다음 **레지스트리 항목**을 선택 합니다.    

4. **새 레지스트리 속성** 대화 상자에서 다음을 선택 합니다. 
 
   - **작업**: 업데이트
   - **Hive**: HKEY_LOCAL_MACHINE
   - **키 경로**: SYSTEM\CurrentControlSet\services\mrxsmb10
   - **값 이름**: 시작
   - **값 형식**: REG_DWORD
   - **값 데이터**: 4
 
   ![시작 속성-일반](media/detect-enable-and-disable-smbv1-v2-v3-5.png)

5. 그런 다음 방금 사용 하지 않도록 설정 된 **MRxSMB10** 에 대 한 종속성을 제거 합니다.

   **새 레지스트리 속성** 대화 상자에서 다음을 선택 합니다. 
 
   - **작업**: Replace
   - **Hive**: HKEY_LOCAL_MACHINE
   - **키 경로**: SYSTEM\CurrentControlSet\Services\LanmanWorkstation
   - **값 이름**: DependOnService
   - **값 형식**: REG_MULTI_SZ 
   - **값 데이터**:
      - 브라우저
      - MRxSmb20
      - NSI
 
   > [!NOTE]
   > 이러한 세 문자열은 글머리 기호를 포함 하지 않습니다 (다음 스크린샷 참조).

   ![DependOnService 속성](media/detect-enable-and-disable-smbv1-v2-v3-6.png) 

   기본값에는 여러 버전의 Windows에서 **MRxSMB10** 포함 되어 있으므로이를 다중 값 문자열로 바꾸면 **MRxSMB10** 를 **LanmanServer** 에 대 한 종속성으로 제거 하 고 위의 4 개 값만 아래로 이동 하는 것이 적용 됩니다.

   > [!NOTE]
   > 그룹 정책 관리 콘솔 사용 하는 경우 따옴표 또는 쉼표를 사용할 필요가 없습니다. 개별 줄에 각 항목을 입력 하기만 하면 됩니다.

6. 대상 시스템을 다시 시작 하 여 SMB v1 비활성화를 완료 합니다.

### <a name="summary"></a>요약

모든 설정이 동일한 GPO (그룹 정책 개체)에 있으면 그룹 정책 관리에 다음 설정이 표시 됩니다.

![그룹 정책 관리 편집기-레지스트리](media/detect-enable-and-disable-smbv1-v2-v3-7.png) 

### <a name="testing-and-validation"></a>테스트 및 유효성 검사

구성 된 후에는 정책을 복제 및 업데이트할 수 있습니다. 테스트에 필요한 경우 명령 프롬프트에서 **gpupdate/force** 를 실행 하 고 대상 컴퓨터를 검토 하 여 레지스트리 설정이 올바르게 적용 되었는지 확인 합니다. 환경의 다른 모든 시스템에서 SMB v2 및 SMB v3이 작동 하는지 확인 합니다.

> [!NOTE]
> 대상 시스템을 다시 시작 하는 것을 잊지 마세요.
