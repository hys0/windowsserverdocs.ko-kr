---
title: Nano 서버 배포
description: 사용자 지정 이미지, 패키지, 드라이버, 도메인, 역할, 기능의 생성 및 배포에 대해 설명합니다.
ms.prod: windows-server-threshold
ms.service: na
manager: DonGill
ms.technology: server-nano
ms.date: 09/06/2017
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9f109c91-7c2e-4065-856c-ce9e2e9ce558
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: e61844cfb04f95723fe9d08b9bd2e8b481714eea
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2019
ms.locfileid: "66442235"
---
# <a name="deploy-nano-server"></a>Nano 서버 배포

>적용 대상: Windows Server 2016

> [!IMPORTANT]
> Windows Server, 버전 1709부터 [컨테이너 기본 OS 이미지](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image)로만 Nano 서버를 사용할 수 있습니다. [Nano 서버 변경 사항](nano-in-semi-annual-channel.md)을 확인하여 그 의미를 알아보세요. 

이 토픽에서는 Nano 서버 빠른 시작 토픽의 간단한 예제에 비해 요구 사항에 맞게 좀 더 사용자 지정된 Nano 서버 이미지를 배포하는 데 필요한 정보를 다룹니다. 정확히 원하는 기능을 사용하여 사용자 지정 Nano 서버 이미지를 만들고, VHD 또는 WIM으로 Nano 서버 이미지를 설치하고, 파일을 편집하고, 도메인을 작업하고, 여러 가지 방법으로 패키지를 처리하고, 서버 역할을 작업하는 방법에 대해 설명할 것입니다.

## <a name="nano-server-image-builder"></a>Nano 서버 이미지 작성기

Nano 서버 이미지 작성기는 그래픽 인터페이스의 도움을 받아 사용자 지정 Nano 서버 이미지 및 부팅 가능 USB 미디어를 만들 수 있는 도구입니다. 이 도구는 사용자의 입력을 기반으로, Windows Server 2016 Datacenter 또는 Standard 버전을 실행하는 Nano 서버의 설치를 간단하게 일관적으로 자동화할 수 있는 재사용 가능 PowerShell 스크립트를 생성합니다.

[다운로드 센터](https://www.microsoft.com/en-us/download/details.aspx?id=54065)에서 도구를 다운로드합니다. 

이 도구를 사용하려면 [Windows ADK(Assessment and Deployment Kit)](https://developer.microsoft.com/en-us/windows/hardware/windows-assessment-deployment-kit)가 필요합니다.


Nano 서버 이미지 작성기는 사용자 지정 Nano 서버 이미지를 VHD, VHDX 또는 ISO 형식으로 만들며, Nano 서버를 배포하거나 서버의 하드웨어 구성을 감지하는 부팅 가능 USB 미디어를 만들 수 있습니다. 뿐만 아니라 다음과 같은 일을 할 수 있습니다.

- 사용 조건에 동의 
- VHD, VHDX 또는 ISO 형식 만들기
- 서버 역할 추가
- 디바이스 드라이버 추가
- 컴퓨터 이름, 관리자 암호, 로그 파일 경로 및 표준 시간대 설정
- 기존 Active Directory 계정 또는 수집한 도메인 가입 blob을 사용하여 도메인에 가입
- 로컬 서브넷 외부 통신에 WinRM 사용
- 가상 LAN ID를 활성화하고 고정 IP 주소 구성
- 즉석에서 새로운 서비스 패키지 삽입
- unattend.xml이 처리된 후에 실행되는 setupcomplete.cmd 또는 다른 고객 스크립트 추가
- 직렬 포트 콘솔 액세스를 위한 EMS(응급 관리 서비스) 활성화
- 테스트 서명된 드라이버와 서명되지 않은 애플리케이션인 PowerShell 기본 셸을 사용하도록 개발 서비스 활성화
- 직렬 포트, USB, TCP/IP 또는 IEEE 1394 프로토콜을 통한 디버깅 활성화
- WinPE를 사용하여 서버를 분할하고 Nano 이미지를 설치하는 USB 미디어 만들기
- WinPE를 사용하여 기존 Nano 서버 하드웨어 구성을 검색하고 모든 세부 정보를 로그 및 화면에 보고하는 USB 미디어 만들기. 여기에는 네트워크 어댑터, MAC 주소 및 펌웨어 유형(BIOS 또는 UEFI)이 포함됩니다. 또한 검색 프로세스에서는 Server Core 드라이버 패키지에 드라이버가 포함되지 않은 시스템 및 디바이스의 모든 볼륨을 표시합니다.

이 중에서 익숙하지 않은 작업이 있으면 이 토픽의 나머지 내용과 기타 Nano 서버 토픽을 검토하여 이 도구에 필요한 정보를 입력할 수 있도록 준비하시기 바랍니다.

## <a name="BKMK_CreateImage"></a>사용자 지정 Nano 서버 이미지 만들기  
Windows Server 2016의 경우 Nano 서버가 물리적 미디어에 배포되며, 이 미디어에서 **NanoServer** 폴더를 찾을 수 있습니다. 이 폴더에는 .wim 이미지와 **Packages**라는 이름의 하위 폴더가 들어 있습니다. VHD 이미지에 서버 역할 및 기능을 추가한 다음 부팅할 때 사용하는 파일이 바로 이 패키지 파일입니다.  

PackageManagement(OneGet) PowerShell 모듈의 NanoServerPackage 공급 기업을 사용하여 이러한 패키지를 찾아서 설치할 수도 있습니다. 이 토픽의 "온라인으로 역할 및 기능 설치" 섹션을 참조하세요.  

다음 테이블은 이 Nano 서버 릴리스에 제공되는 역할 및 기능, 그리고 패키지를 설치하는 Windows PowerShell 옵션을 보여 줍니다. 일부 패키지는 -Compute 같은 고유의 Windows PowerShell 스위치를 통해 직접 설치되고, 나머지 패키지는 사용자가 -Package 매개 변수에 패키지 이름을 전달하여 설치하며, 쉼표로 구분된 목록에 결합할 수 있습니다. Get-NanoServerPackage cmdlet을 사용하여 사용 가능한 패키지를 동적으로 나열할 수 있습니다.  


|                                                                             역할 또는 기능                                                                             |                                                                                                                                                                                                          옵션                                                                                                                                                                                                           |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                     Hyper-V 역할(NetQoS 포함)                                                                     |                                                                                                                                                                                                         -Compute                                                                                                                                                                                                          |
|                                                   장애 조치(Failover) 클러스터링 및 기타 구성 요소(이 표 다음에 자세히 설명)                                                   |                                                                                                                                                                                                        -Clustering                                                                                                                                                                                                        |
| 다양한 네트워크 어댑터 및 스토리지 컨트롤러를 위한 기본 드라이버. Windows Server 2016의 Server Core 설치에 포함된 드라이버와 동일합니다. |                                                                                                                                                                                                        -OEMDrivers                                                                                                                                                                                                        |
|                                                파일 서버 역할 및 기타 저장소 구성 요소(이 표 다음에 자세히 설명)                                                 |                                                                                                                                                                                                         -Storage                                                                                                                                                                                                          |
|                                                          Windows Defender(기본 서명 파일 포함)                                                           |                                                                                                                                                                                                         -Defender                                                                                                                                                                                                         |
|                         애플리케이션 호환성을 위한 역방향 전달자. Ruby, Node.js 등 일반 애플리케이션 프레임워크를 예로 들 수 있습니다.                         |                                                                                                                                                                                                  이제는 기본적으로 포함됩니다.                                                                                                                                                                                                  |
|                                                                             DNS 서버 역할                                                                             |                                                                                                                                                                                         -Package Microsoft-NanoServer-DNS-Package                                                                                                                                                                                         |
|                                                              PowerShell DSC(필요한 상태 구성)                                                               |                                                                                                                               -Package Microsoft-NanoServer-DSC-Package<br />**참고:** 자세한 내용은 [Nano 서버에서 DSC 사용](https://msdn.microsoft.com/powershell/dsc/nanoDsc)을 참조하세요.                                                                                                                               |
|                                                                    IIS(인터넷 정보 서버)                                                                    |                                                                                                                                       -Package Microsoft-NanoServer-IIS-Package<br />**참고:** IIS 작업에 대한 자세한 내용은 [Nano 서버의 IIS](IIS-on-Nano-Server.md)를 참조하세요.                                                                                                                                        |
|                                                                   Windows 컨테이너에 대한 호스트 지원                                                                   |                                                                                                                                                                                                        -Containers                                                                                                                                                                                                        |
|                                                               System Center Virtual Machine Manager 에이전트                                                               | -Package Microsoft-NanoServer-SCVMM-Package<br />-Package Microsoft-NanoServer-SCVMM-Compute-Package<br />**참고:** SCVMM 계산 패키지는 Hyper-V를 모니터링하는 경우에만 사용하세요. VMM에서 하이퍼 수렴형 배포를 수행하는 경우에도 -Storage 매개 변수를 지정해야 합니다. 자세한 내용은 [VMM 설명서](https://technet.microsoft.com/system-center-docs/vmm/manage/manage-compute-add-nano-hyper-v)를 참조하세요. |
|                                                                 System Center Operations Manager 에이전트                                                                  |                                                                                                                 별도 설치되었습니다. 자세한 내용은 https://technet.microsoft.com/system-center-docs/om/manage/install-agent-on-nano-server 에서 System Center Operations Manager 설명서를 참조하세요.                                                                                                                 |
|                                                                 데이터 센터 브리징(DCBQoS 포함)                                                                 |                                                                                                                                                                                         -Package Microsoft-NanoServer-DCB-Package                                                                                                                                                                                         |
|                                                                     가상 컴퓨터에 배포                                                                      |                                                                                                                                                                                        -Package Microsoft-NanoServer-Guest-Package                                                                                                                                                                                        |
|                                                                     물리적 컴퓨터에 배포                                                                     |                                                                                                                                                                                        - Package Microsoft-NanoServer-Host-Package                                                                                                                                                                                        |
|     BitLocker, TPM(신뢰할 수 있는 플랫폼 모듈), 볼륨 암호화, 플랫폼 식별, 암호화 공급자 및 기타 보안 시작과 관련된 기능     |                                                                                                                                                                                    -Package Microsoft-NanoServer-SecureStartup-Package                                                                                                                                                                                    |
|                                                                    보호된 VM에 대한 Hyper-V 지원                                                                     |                                                                                                                                         -Package Microsoft-NanoServer-ShieldedVM-Package<br />**참고:** 이 패키지는 Nano 서버 Datacenter 버전에만 제공됩니다.                                                                                                                                         |
|                                                             SNMP(Simple Network Management Protocol) 에이전트                                                             |                                   -Package Microsoft-NanoServer-SNMP-Agent-Package.cab<br />**참고:** Windows Server 2016 설치 미디어에 포함되지 않습니다. 온라인에서만 사용할 수 있습니다. 자세한 내용은 [온라인으로 역할 및 기능 설치](https://technet.microsoft.com/windows-server-docs/get-started/deploy-nano-server#a-namebkmkonlineainstalling-roles-and-features-online)를 참조하세요.                                    |
|               IPv6 전환 기술(6to4, ISATAP, Port Proxy 및 Teredo)과 IP-HTTPS를 사용하여 터널 연결을 제공하는 IP 도우미 서비스               |                                -Package Microsoft-NanoServer-IPHelper-Service-Package.cab<br />**참고:** Windows Server 2016 설치 미디어에 포함되지 않습니다. 온라인에서만 사용할 수 있습니다. 자세한 내용은 [온라인으로 역할 및 기능 설치](https://technet.microsoft.com/windows-server-docs/get-started/deploy-nano-server#a-namebkmkonlineainstalling-roles-and-features-online)를 참조하세요.                                 |

> [!NOTE]  
> 이 옵션을 사용하여 패키지를 설치하면 선택한 서버 미디어 로캘에 따라 해당 언어 팩도 함께 설치됩니다. 이미지 로캘에 대해 명명된 하위 폴더의 설치 미디어에서 사용 가능한 언어 팩과 해당 로캘 약어를 찾을 수 있습니다.  

> [!NOTE]  
> -Storage 매개 변수를 사용하여 파일 서비스를 설치하는 경우 파일 서비스는 실제로 사용할 수 없습니다. 서버 관리자를 사용하여 원격 컴퓨터에서 이 기능을 사용하도록 설정해야 합니다. 

### <a name="failover-clustering-items-installed-by-the--clustering-parameter"></a>-Clustering 매개 변수로 설치된 장애 조치(Failover) 클러스터링 항목

- 장애 조치(Failover) 클러스터링 역할
- VM 장애 조치(Failover) 클러스터링
- 저장소 공간 다이렉트(S2D)
- 저장소 서비스 품질
- 볼륨 복제 클러스터링
- SMB 감시 서비스


### <a name="file-and-storage-items-installed-by-the--storage-parameter"></a>-Storage 매개 변수로 설치된 파일 및 저장소 항목

- 파일 서버 역할
- 데이터 중복 제거
- MSDSM(Microsoft 장치별 모듈) 드라이버를 포함한 다중 경로 I/O
- ReFS(v1 및 v2)
- iSCSI 초기자(iSCSI 대상은 아님)
- 저장소 복제본
- SMI-S를 지원하는 저장소 관리 서비스
- SMB 감시 서비스
- 동적 볼륨
- Windows 저장소 관리를 위한 기본 Windows 저장소 공급자




### <a name="installing-a-nano-server-vhd"></a>Nano 서버 VHD 설치  
이 예에서는 네트워크 공유의 Nano 서버 설치 미디어로 시작하여 지정된 컴퓨터 이름이 있고 Hyper-V 게스트 드라이버가 포함된 GPT 기반 VHDX 이미지를 만듭니다. 관리자 권한 Windows PowerShell 프롬프트에서 다음 cmdlet을 시작합니다.  

`Import-Module <Server media location>\NanoServer\NanoServerImageGenerator; New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\server_en-us -BasePath .\Base -TargetPath .\FirstStepsNano.vhdx -ComputerName FirstStepsNano`  

이 cmdlet은 다음 작업을 모두 수행합니다.  

1.  기본 버전으로 Standard 선택  

2.  관리자 암호 요청  

3.  \\\Path\To\Media\server_en-us into .\Base에서 설치 미디어 복사  

4.  WIM 이미지를 VHD로 변환. (대상 경로 인수의 파일 확장명은 1세대 가상 컴퓨터용 MBR 기반 VHD를 만드는지 아니면 2세대 가상 컴퓨터용 GPT 기반 VHDX를 만드는지 여부를 결정.)  

5.  그 결과로 얻은 VHD를 .\FirstStepsNano.vhdx에 복사  

6.  지정된 대로 이미지의 관리자 암호 설정  

7.  이미지의 컴퓨터 이름을 FirstStepsNano로 설정  

8.  Hyper-V 게스트 드라이버 설치  

이 모든 작업의 결과로 .\FirstStepsNano.vhdx 이미지가 생성됩니다.  

이 cmdlet은 실행되면서 로그를 생성하고 실행이 완료되면 사용자에게 로그 위치를 알려 줍니다. 도우미 스크립트를 통해 수행된 WIM-VHD 변환은 %TEMP%\Convert-WindowsImage\\\<GUID&gt;에 고유의 로그를 생성합니다(\<GUID&gt;는 변환 세션별 고유 식별자).  

동일한 기본 경로를 사용하는 한, 이 cmdlet을 실행할 때마다 미디어 경로 매개 변수를 생략할 수 있습니다. 이 cmdlet은 기본 경로의 캐시된 파일을 사용하기 때문입니다. 기본 경로를 지정하지 않으면 이 cmdlet은 TEMP 폴더에 기본 경로를 생성합니다. 다른 원본 미디어를 사용하고 싶지만 기본 경로가 같으면 미디어 경로 매개 변수를 지정해야 합니다.  

>[!NOTE]  
>이제 Nano 서버 버전을 지정하여 Standard 또는 Datacenter 버전을 빌드할 수 있습니다. -Edition 매개 변수를 사용하여 *Standard* 또는 *Datacenter* 버전을 지정합니다.  

기존 이미지가 있는 경우 *Edit-NanoServerImage* cmdlet을 사용하여 기존 이미지를 필요한 대로 수정할 수 있습니다.  

컴퓨터 이름을 지정하지 않으면 임의의 이름이 생성됩니다.  

### <a name="installing-a-nano-server-wim"></a>Nano 서버 WIM 설치  

1. Windows Server 2016 ISO의 \NanoServer 폴더에서 컴퓨터의 로컬 폴더로 *NanoServerImageGenerator* 폴더를 복사합니다.  
2. 관리자 권한으로 Windows PowerShell을 시작하고, NanoServerImageGenerator 폴더가 있는 폴더로 디렉터리를 변경한 다음 `Import-Module .\NanoServerImageGenerator -Verbose`를 사용하여 모듈을 가져옵니다.  

   >[!NOTE]  
   >Windows PowerShell 실행 정책을 조정해야 합니다. `Set-ExecutionPolicy RemoteSigned`는 제대로 작동해야 합니다.  

Hyper-V 호스트 역할을 수행할 Nano 서버 이미지를 만들려면 다음을 실행합니다.  

`New-NanoServerImage -Edition Standard -DeploymentType Host -MediaPath <path to root of media> -BasePath .\Base -TargetPath .\NanoServerPhysical\NanoServer.wim -ComputerName <computer name> -OEMDrivers -Compute -Clustering`  

위치  
-   -MediaPath는 Windows Server 2016이 포함된 DVD 미디어 또는 ISO 이미지의 루트입니다.  
-   -BasePath는 Nano 서버 이진 파일의 복사본을 포함하게 되므로 나중에 실행할 때 -MediaPath를 지정할 필요 없이 New-NanoServerImage -BasePath를 사용할 수 있습니다.  
-   -TargetPath에는 선택한 역할 및 기능이 들어 있는 결과 .wim 파일이 포함됩니다. .wim 확장명을 지정해야 합니다.  
-   -Compute는 Hyper-V 역할을 추가합니다.  
-   -OemDrivers는 다양한 일반 드라이버를 추가합니다.  

관리자 암호를 입력하라는 메시지가 표시될 것입니다.  

자세한 내용은 `Get-Help New-NanoServerImage -Full`를 실행하십시오.  

WinPE로 부팅하여 방금 만든 .wim 파일을 WinPE에서 액세스할 수 있는지 확인합니다. 예를 들어 .wim 파일을 USB 플래시 드라이브의 부팅 가능 WinPE 이미지로 복사할 수 있습니다.  

WinPE가 부팅되면 Diskpart.exe를 사용하여 대상 컴퓨터의 하드 드라이브를 준비합니다. 다음 Diskpart 명령을 실행합니다(UEFI 및 GPT를 사용하지 않는 경우 그에 따라 적절하게 수정).  

> [!WARNING]  
> 다음 명령은 하드 드라이브의 모든 데이터를 삭제합니다.  

**Diskpart.exe Select disk 0 Clean Convert GPT Create partition efi size=100 Format quick FS=FAT32 label="System" Assign letter="s" Create partition msr size=128 Create partition primary Format quick FS=NTFS label="NanoServer" Assign letter="n" List volume Exit**  

Nano 서버 이미지를 적용합니다(.wim 파일의 경로 조정).  

**Dism.exe /apply-image /imagefile:.\NanoServer.wim /index:1 /applydir:n:\ Bcdboot.exe n:\Windows /s s:**  

DVD 미디어 또는 USB 드라이브를 제거하고 **Wpeutil.exe Reboot** 명령을 사용하여 시스템을 다시 부팅합니다.  


### <a name="editing-files-on-nano-server-locally-and-remotely"></a>로컬 및 원격으로 Nano 서버의 파일 편집  
 어떤 방법을 사용하든 Windows PowerShell 원격 작업을 사용할 때와 마찬가지로 Nano 서버에 연결합니다.  

 Nano 서버에 연결한 후에는 파일의 상대 또는 절대 경로를 다음과 같이 psEdit 명령에 전달하여 로컬 컴퓨터에 있는 파일을 편집할 수 있습니다.   
`psEdit C:\Windows\Logs\DISM\dism.log` 또는 `psEdit .\myScript.ps1`  

`Enter-PSSession -ComputerName "192.168.0.100" -Credential ~\Administrator` 명령으로 원격 세션을 시작한 다음 파일의 상대 또는 절대 경로를 다음과 같이 psEdit 명령에 전달하여 원격 Nano 서버에 있는 파일을 편집합니다.   
`psEdit C:\Windows\Logs\DISM\dism.log`  

## <a name="BKMK_online"></a>온라인으로 역할 및 기능 설치  
> [!NOTE]
> 미디어 또는 온라인 저장소에서 선택적 Nano 서버 패키지를 설치하는 경우에는 최근 보안 픽스가 포함되지 않습니다. 옵션 패키지와 기본 운영 체제 간의 버전 불일치를 방지하기 위해 옵션 패키지를 설치하는 즉시 [최신 누적 업데이트](https://technet.microsoft.com/windows-server-docs/get-started/update-nano-server)를 설치한 **후** 서버를 다시 시작해야 합니다.

### <a name="installing-roles-and-features-from-a-package-repository"></a>패키지 리포지토리에서 역할 및 기능 설치  
PackageManagement PowerShell 모듈의 NanoServerPackage 공급자를 사용하여 온라인 패키지 리포지토리에서 Nano 서버 패키지를 찾아 설치할 수 있습니다. 이 공급자를 설치하려면 다음 cmdlet을 사용합니다.

```powershell
Install-PackageProvider NanoServerPackage
Import-PackageProvider NanoServerPackage
```

>[!NOTE]
>Install-PackageProvider를 실행할 때 오류가 발생하면 다음과 같이 [최신 누적 업데이트](https://technet.microsoft.com/windows-server-docs/get-started/update-nano-server)([KB3206632](https://support.microsoft.com/kb/3206632) 이상)를 설치했는지 확인하거나 Save-Module을 사용합니다. 

```powershell
Save-Module -Path "$Env:ProgramFiles\WindowsPowerShell\Modules\" -Name NanoServerPackage -MinimumVersion 1.0.1.0
Import-PackageProvider NanoServerPackage
```

이 공급자를 설치하여 가져온 후에는 Nano 서버 패키지 작업을 위해 특별히 설계된 cmdlet을 사용하여 Nano 서버 패키지를 검색, 다운로드 및 설치할 수 있습니다.

```powershell
Find-NanoServerPackage  
Save-NanoServerPackage  
Install-NanoServerPackage
```  

또한 일반 PackageManagement cmdlet을 사용하여 NanoServerPackage 공급자를 지정할 수도 있습니다.

```powershell
Find-Package -ProviderName NanoServerPackage
Save-Package -ProviderName NanoServerPackage
Install-Package -ProviderName NanoServerPackage
Get-Package -ProviderName NanoServerPackage
```

이러한 cmdlet을 Nano 서버의 Nano 서버 패키지와 함께 사용하려면 `-ProviderName NanoServerPackage`를 추가합니다. -ProviderName 매개 변수를 추가하지 않으면 PackageManagement가 모든 공급자를 반복합니다. 이러한 cmdlet에 대해 자세히 알아보려면 `Get-Help <cmdlet>`을 실행하세요. 다음은 몇 가지 일반적인 사용 예제입니다.

### <a name="searching-for-nano-server-packages"></a>Nano 서버 패키지 검색  
`Find-NanoServerPackage` 또는 `Find-Package -ProviderName NanoServerPackage`를 사용하여 온라인 리포지토리에서 사용할 수 있는 Nano 서버 패키지 목록을 검색 및 반환할 수 있습니다. 예를 들어 모든 최신 패키지 목록을 가져올 수 있습니다.

```powershell
Find-NanoServerPackage
```

`Find-Package -ProviderName NanoServerPackage -DisplayCulture`를 실행하면 사용 가능한 모든 문화권이 표시됩니다.

미국 영어와 같은 특정 로캘 버전이 필요한 경우 `Find-NanoServerPackage -Culture en-us` 또는  
`Find-Package -ProviderName NanoServerPackage -Culture en-us` 또는 `Find-Package -Culture en-us -DisplayCulture`.

패키지 이름으로 특정 패키지를 찾으려면 -Name 매개 변수를 사용합니다. 이 매개 변수에는 와일드카드도 사용할 수 있습니다. 예를 들어 이름에 VMM이 포함된 모든 패키지를 찾으려면 `Find-NanoServerPackage -Name *VMM*` 또는 `Find-Package -ProviderName NanoServerPackage -Name *VMM*`을 사용합니다.

-RequiredVersion, -MinimumVersion 또는 -MaximumVersion 매개 변수를 사용하여 특정 버전을 찾을 수 있습니다. 사용 가능한 모든 버전을 찾으려면 -AllVersions를 사용합니다. 그렇지 않으면 최신 버전만 반환됩니다. 예를 들면 `Find-NanoServerPackage -Name *VMM* -RequiredVersion 10.0.14393.0`와 같습니다. 또는 모든 버전을 찾으려면: `Find-Package -ProviderName NanoServerPackage -Name *VMM* -AllVersions`

### <a name="installing-nano-server-packages"></a>Nano 서버 패키지 설치  
`Install-NanoServerPackage` 또는 `Install-Package -ProviderName NanoServerPackage`를 사용하여 Nano 서버 패키지(종속성 패키지가 있는 경우 종속성 패키지 포함)를 Nano 서버에 로컬로 또는 오프라인 이미지에 설치할 수 있습니다. 이들은 모두 파이프라인으로부터 입력을 받아들입니다.

온라인 Nano 서버에 최신 버전의 Nano 서버 패키지를 설치하려면 `Install-NanoServerPackage -Name Microsoft-NanoServer-Containers-Package` 또는 `Install-Package -Name Microsoft-NanoServer-Containers-Package`를 사용합니다. PackageManagement는 Nano 서버의 문화권을 사용합니다.

오프라인 이미지에 Nano 서버 패키지를 설치하고, 다음과 같이 특정 버전 및 문화권을 지정할 수 있습니다.

`Install-NanoServerPackage -Name Microsoft-NanoServer-DCB-Package -Culture de-de -RequiredVersion 10.0.14393.0 -ToVhd C:\MyNanoVhd.vhd`

또는

`Install-Package -Name Microsoft-NanoServer-DCB-Package -Culture de-de -RequiredVersion 10.0.14393.0 -ToVhd C:\MyNanoVhd.vhd`

다음은 파이프라인을 통한 패키지 검색 결과를 설치 cmdlet으로 전송하는 몇 가지 예입니다.  

`Find-NanoServerPackage *dcb* | Install-NanoServerPackage`는 이름에 "dcb"가 포함된 패키지를 찾아서 설치합니다.

`Find-Package *nanoserver-compute-* | Install-Package`는 이름에 "nanoserver-compute-"가 포함된 패키지를 찾아서 설치합니다.

`Find-NanoServerPackage -Name *nanoserver-compute* | Install-NanoServerPackage -ToVhd C:\MyNanoVhd.vhd`는 이름에 "compute"가 포함된 패키지를 찾아서 오프라인 이미지에 설치합니다.

`Find-Package -ProviderName NanoserverPackage *nanoserver-compute-* | Install-Package -ToVhd C:\MyNanoVhd.vhd`는 이름에 "nanoserver-compute-"가 포함된 패키지와 똑같은 방식으로 작동합니다.

### <a name="downloading-nano-server-packages"></a>Nano 서버 패키지 다운로드  

`Save-NanoServerPackage` 또는 `Save-Package`를 사용하면 패키지를 다운로드하여 설치하지 않고 저장할 수 있습니다. 두 cmdlet은 모두 파이프라인으로부터 입력을 받아들입니다.

예를 들어 Nano 서버 패키지를 다운로드하고 와일드카드 경로와 일치하는 디렉터리에 저장하려면 `Save-NanoServerPackage -Name Microsoft-NanoServer-DNS-Package -Path C:\`를 사용합니다. 이 예에서는 -Culture가 지정되지 않았기 때문에 로컬 컴퓨터의 문화권이 사용됩니다. 버전을 지정하지 않아 최신 버전이 저장됩니다.

`Save-Package -ProviderName NanoServerPackage -Name Microsoft-NanoServer-IIS-Package -Path C:\ -Culture it-IT -MinimumVersion 10.0.14393.0`은 특정 버전을 이탈리아 언어 및 로캘로 저장합니다.

이러한 예제와 같이 파이프라인을 통해 결과를 전송할 수 있습니다.

`Find-NanoServerPackage -Name *containers* -MaximumVersion 10.2 -MinimumVersion 1.0 -Culture es-ES | Save-NanoServerPackage -Path C:\`

또는

`Find-Package -ProviderName NanoServerPackage -Name *shield* -Culture es-ES | Save-Package -Path`

### <a name="inventory-installed-packages"></a>인벤토리가 설치된 패키지
`Get-Package`를 사용하여 어떤 Nano 서버 패키지가 설치되었는지 검색할 수 있습니다. 예를 들어 `Get-Package -ProviderName NanoserverPackage`로 Nano 서버에 어떤 패키지가 있는지 살펴볼 수 있습니다.

예를 들어 오프라인 이미지에 설치된 Nano 서버 패키지를 확인하려면 `Get-Package -ProviderName NanoserverPackage -FromVhd C:\MyNanoVhd.vhd`를 실행합니다.


### <a name="installing-roles-and-features-from-local-source"></a>로컬 원본에서 역할 및 기능 설치  
서버 역할 및 기타 패키지를 오프라인으로 설치하는 것이 좋지만, 컨테이너 시나리오에서 온라인으로(Nano 서버가 실행 중인 상태로) 설치해야 할 수도 있습니다. 이렇게 하려면 다음 단계를 따르십시오.  

1.  설치 미디어의 패키지 폴더를 실행 중인 Nano 서버에(예: C:\packages) 로컬로 복사합니다.  

2.  다른 컴퓨터에서 새 Unattend.xml 파일을 만들어 Nano 서버에 복사합니다. 이 XML 콘텐츠를 복사하여 이전에 만든 XML 파일에 붙여 넣습니다(이 예에서는 IIS 패키지 설치 방법을 소개).  



```  
<?xml version="1.0" encoding="utf-8"?>
    <unattend xmlns="urn:schemas-microsoft-com:unattend">  
    <servicing>  
        <package action="install">  
            <assemblyIdentity name="Microsoft-NanoServer-IIS-Feature-Package" version="10.0.14393.0" processorArchitecture="amd64" publicKeyToken="31bf3856ad364e35" language="neutral" />  
            <source location="c:\packages\Microsoft-NanoServer-IIS-Package.cab" />  
        </package>  
        <package action="install">  
            <assemblyIdentity name="Microsoft-NanoServer-IIS-Feature-Package" version="10.0.14393.0" processorArchitecture="amd64" publicKeyToken="31bf3856ad364e35" language="en-US" />  
            <source location="c:\packages\en-us\Microsoft-NanoServer-IIS-Package_en-us.cab" />  
        </package>  
    </servicing>  
    <cpi:offlineImage cpi:source="" xmlns:cpi="urn:schemas-microsoft-com:cpi" />  
</unattend>  
```  




3. 새로 만든(또는 복사한) XML 파일에서, \packages를 패키지 콘텐츠를 복사한 디렉터리로 편집합니다.  

4. 새로 만든 XML 파일이 있는 디렉터리로 전환하고 다음 명령을 실행합니다.  

   **dism /online /apply-unattend:.\unattend.xml**  



5. 다음 명령을 실행하여 패키지와 관련 언어 팩이 올바르게 설치되었는지 확인합니다.  

   **dism /online /get-packages**  

   "패키지 ID: Microsoft-NanoServer-IIS-Package~31bf3856ad364e35~amd64~en-US~10.0.10586.0"이 두 번 나열되고, 릴리스 유형: 언어 팩이 한 번 나열되고, 릴리스 유형: 기능 팩이 한 번 나열되어야 합니다.  

## <a name="customizing-an-existing-nano-server-vhd"></a>기존 Nano 서버 VHD 사용자 지정  
이 예제처럼 Edit-NanoServerImage cmdlet을 사용하여 기존 VHD의 세부 정보를 변경할 수 있습니다.  

`Edit-NanoServerImage   -BasePath .\Base   -TargetPath .\BYOVHD.vhd`  

이 cmdlet은 New-NanoServerImage와 동일한 작업을 수행하지만 WIM을 VHD로 변환하는 대신 기존 이미지를 변경합니다. -MediaPath 및 -MaxSize를 제외하고 New-NanoServerImage와 동일한 매개 변수를 지원하므로 이러한 매개 변수를 사용하여 초기 VHD 만들어야만 Edit-NanoServerImage를 사용하여 변경할 수 있습니다.  

## <a name="additional-tasks-you-can-accomplish-with-new-nanoserverimage-and-edit-nanoserverimage"></a>New-NanoServerImage 및 Edit-NanoServerImage로 할 수 있는 추가 작업  

### <a name="joining-domains"></a>도메인 가입  
New-NanoServerImage는 도메인에 가입하는 두 가지 방법을 제공합니다. 둘 다 오프라인 도메인 프로비전을 사용하지만, 하나는 blob을 수집하여 조인을 수행합니다. 이 예제에서, cmdlet은 로컬 컴퓨터의 Contoso 도메인에 대한 도메인 blob(당연히 Contoso 도메인의 일부여야 함)을 수집한 후 blob을 사용하여 오프라인에서 이미지를 프로비전합니다.  

`New-NanoServerImage -Edition Standard -DeploymentType Host -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\JoinDomHarvest.vhdx -ComputerName JoinDomHarvest -DomainName Contoso`  

이 cmdlet이 완료되면 Active Directory 컴퓨터 목록에서 "JoinDomHarvest"라는 컴퓨터를 찾아야 합니다.  

또한 도메인에 가입되지 않은 컴퓨터에서 이 cmdlet을 사용할 수 있습니다. 이렇게 하려면 도메인에 가입된 컴퓨터에서 blob을 수집한 다음 해당 blob를 cmdlet에 직접 입력합니다. 다른 컴퓨터에서 이러한 blob을 수집할 때 blob에는 이미 해당 컴퓨터의 이름이 포함되어 있으므로 *-ComputerName* 매개 변수를 추가하려고 시도하면 오류가 발생합니다.  

다음 명령으로 blob을 수집할 수 있습니다.  

**djoin**  
 **/Provision**  
 **/Domain Contoso**  
 **/Machine JoiningDomainsNoHarvest**  
 **/SaveFile JoiningDomainsNoHarvest.djoin**  

수집된 blob을 사용하여 New-NanoServerImage 실행:  

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\JoinDomNoHrvest.vhd -DomainBlobPath .\Path\To\Domain\Blob\JoinDomNoHrvestContoso.djoin`  

도메인에 향후 Nano 서버와 컴퓨터 이름이 같은 노드가 이미 있는 경우 `-ReuseDomainNode` 매개 변수를 추가하여 컴퓨터 이름을 다시 사용할 수 있습니다.  

### <a name="adding-additional-drivers"></a>드라이버 추가
Nano 서버는 다양한 네트워크 어댑터 및 스토리지 컨트롤러를 위한 기본 드라이버가 포함된 패키지를 제공합니다. 하지만 사용자의 네트워크 어댑터에 필요한 드라이버가 없을 수도 있습니다. 이 경우 다음 단계에 따라 작업 시스템에서 드라이버를 찾아서 추출한 다음 Nano 서버 이미지에 추가할 수 있습니다.

1. Nano 서버를 실행할 물리적 컴퓨터에 Windows Server 2016을 설치합니다.
2. 디바이스 관리자를 열고 다음 범주에 속하는 디바이스를 확인합니다.
3. 네트워크 어댑터
4. 스토리지 컨트롤러
5. 디스크 드라이브
6. 이러한 범주에 속하는 각 디바이스마다 디바이스 이름을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다. 열리는 대화 상자에서 **드라이버** 탭을 클릭한 다음 **드라이버 정보**를 클릭합니다.
7. 나타나는 드라이버의 파일 이름 및 경로를 기록해 둡니다. 예를 들어 드라이버 파일이 e1i63x64.sys이고 C:\Windows\System32\Drivers에 있다고 가정해 봅시다.
8. 명령 프롬프트에서 dir e1i*.sys /s /b를 사용하여 모든 드라이버 파일을 검색하고 모든 인스턴스를 검색합니다. 이 예제에서는 경로 C:\Windows\System32\DriverStore\FileRepository\net1ic64.inf_amd64_fafa7441408bbecd\e1i63x64.sys에도 드라이버 파일이 있습니다.
9. 관리자 권한 명령 프롬프트에서, Nano 서버 VHD가 있는 디렉터리로 이동하여 다음 명령을 실행합니다. **md mountdir**

    **dism\dism /Mount-Image /ImageFile:.\NanoServer.vhd /Index:1 /MountDir:.\mountdir**

    **dism\dism /Add-Driver /image:.\mountdir /driver: C:\Windows\System32\DriverStore\FileRepository\net1ic64.inf_amd64_fafa7441408bbecd**

    **dism\dism /Unmount-Image /MountDir:.\MountDir /Commit**
10. 필요한 드라이버 파일마다 이러한 단계를 반복합니다.

> [!NOTE]  
> 드라이버를 보관하는 폴더에 SYS 파일과 해당하는 INF 파일이 모두 있어야 합니다. 또한 Nano 서버는 서명된 64\-비트 드라이버만 지원합니다. 

### <a name="injecting-drivers"></a>드라이버 삽입  
Nano 서버는 다양한 네트워크 어댑터 및 저장소 컨트롤러를 위한 기본 드라이버가 포함된 패키지를 제공합니다. 하지만 사용자의 네트워크 어댑터에 필요한 드라이버가 없을 수도 있습니다. 이 구문을 사용하여 New-NanoServerImage가 사용 가능한 드라이버의 디렉터리를 검색하여 Nano 서버 이미지에 삽입하도록 만들 수 있습니다.  

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\InjectingDrivers.vhdx -DriverPath .\Extra\Drivers`  

> [!NOTE]
> 드라이버를 보관하는 폴더에 SYS 파일과 해당하는 INF 파일이 모두 있어야 합니다. 또한 Nano 서버는 서명된 64비트 드라이버만 지원합니다.

-DriverPath 매개 변수를 사용하여 경로 배열을 드라이버 .inf 파일로 전달할 수도 있습니다.

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\InjectingDrivers.vhdx -DriverPath .\Extra\Drivers\netcard64.inf`

### <a name="connecting-with-winrm"></a>WinRM에 연결  
(동일한 서브넷에 있지 않은 다른 컴퓨터에서) WinRM(Windows Remote Management)을 사용하여 Nano 서버 컴퓨터에 연결하려면 Nano 서버 이미지의 인바운드 TCP 트래픽에 사용할 5985 포트를 엽니다. 이 cmdlet을 사용합니다.  

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\ConnectingOverWinRM.vhd -EnableRemoteManagementPort`  

### <a name="setting-static-ip-addresses"></a>고정 IP 주소 설정  
고정 IP 주소를 사용하도록 Nano 서버 이미지를 구성하려면 Get-NetAdapter, netsh 또는 Nano 서버 복구 콘솔을 사용하여 수정하려는 인터페이스의 이름 또는 색인을 찾습니다. 이 예제와 같이 -Ipv6Address, -Ipv6Dns, -Ipv4Address, -Ipv4SubnetMask, -Ipv4Gateway 및 -Ipv4Dns 매개 변수를 사용하여 구성을 지정합니다.  

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\StaticIpv4.vhd -InterfaceNameOrIndex Ethernet -Ipv4Address 192.168.1.2 -Ipv4SubnetMask 255.255.255.0 -Ipv4Gateway 192.168.1.1 -Ipv4Dns 192.168.1.1`  

### <a name="custom-image-size"></a>사용자 지정 이미지 크기  
이 예제와 같이 -MaxSize 매개 변수를 사용하여 Nano 서버 이미지가 VHD 또는 VHDX를 동적으로 확장하도록 구성할 수 있습니다.  

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\BigBoss.vhd -MaxSize 100GB`  

### <a name="embedding-custom-data"></a>사용자 지정 데이터 포함  
사용자 고유의 스크립트 또는 이진 파일을 Nano 서버 이미지에 포함하려면 -CopyPath 매개 변수를 사용하여 복사할 파일 및 디렉터리 배열을 전달합니다. -CopyPath 매개 변수는 파일 및 디렉터리의 대상 경로를 지정하기 위해 해시 테이블도 받아들일 수 있습니다.

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\BigBoss.vhd -CopyPath .\tools`

### <a name="running-custom-commands-after-the-first-boot"></a>첫 번째 부팅 후 사용자 지정 명령 실행
setupcomplete.cmd의 일부로 사용자 지정 명령을 실행하려면 -SetupCompleteCommand 매개 변수를 사용하여 명령 배열을 전달합니다.

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -SetupCompleteCommand @("echo foo", "echo bar")`


### <a name="running-custom-powershell-scripts-as-part-of-image-creation"></a>이미지 생성의 일환으로 사용자 지정 PowerShell 스크립트 실행
이미지 생성 프로세스의 일환으로 사용자 지정 PowerShell 스크립트를 실행하려면 -OfflineScriptPath 매개 변수를 사용하여 .ps1 스크립트로 경로 배열을 전달합니다. 이러한 스크립트에서 인수를 사용할 경우 -OfflineScriptArgument를 사용하여 추가 인수의 해시 테이블을 스크립트에 전달합니다.

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -OfflineScriptPath C:\MyScripts\custom.ps1 -OfflineScriptArgument @{Param1="Value1"; Param2="Value2"}`


### <a name="support-for-development-scenarios"></a>개발 시나리오 지원
Nano 서버에서 개발 및 테스트하려는 경우 -Development를 사용할 수 있습니다. 그러면 PowerShell을 기본 로컬 셸로 설정하고, 서명되지 않은 드라이버를 설치하고, 디버거 이진 파일을 복사하고, 디버깅을 위한 포트를 열고, 테스트 서명을 사용하고, 개발자 라이선스 없이 AppX 패키지를 설치할 수 있습니다.

`New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -Development`


### <a name="custom-unattend-file"></a>사용자 지정 무인 파일  
사용자 고유의 무인 파일을 사용하려면 -UnattendPath 매개 변수를 사용합니다.  

`New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -UnattendPath \\path\to\unattend.xml`  

이 무인 파일에서 관리자 암호 또는 컴퓨터 이름을 지정하면 -AdministratorPassword 및 -ComputerName을 통해 설정된 값이 재정의됩니다. 

> [!NOTE]
> Nano 서버는 무인 파일을 통한 TCP/IP 설정을 지원하지 않습니다. Setupcomplete.cmd를 사용하여 TCP/IP 설정을 구성할 수 있습니다.

### <a name="collecting-log-files"></a>로그 파일 수집
이미지를 생성하는 동안 로그 파일을 수집하려면 -LogPath 매개 변수를 사용하여 모든 로그 파일이 복사될 디렉터리를 지정합니다.

`New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -LogPath C:\Logs`


> [!NOTE]
> New-NanoServerImage 및 Edit-NanoServerImage의 일부 매개 변수는 내부용으로만 사용되며 무시해도 됩니다. 여기에는 -SetupUI 및 -Internal 매개 변수가 포함됩니다.


## <a name="installing-apps-and-drivers"></a>앱 및 드라이버 설치
[comment]: # (Xumin Sun에서 버그 #68620.)  

### <a name="windows-server-app-installer"></a>Windows Server 앱 설치 관리자
WSA(Windows Server 응용 프로그램) 설치 관리자는 Nano 서버를 안정적으로 설치할 수 있는 옵션을 제공합니다. MSI(Windows Installer)는 Nano 서버에서 지원되지 않으므로 Microsoft 이외 제품에 사용할 수 있는 유일한 설치 기술은 WSA입니다. WSA는 선언적 매니페스트를 사용하여 애플리케이션을 안전하고 안정적으로 설치 및 운영하도록 설계된 Windows 앱 패키지 기술을 활용합니다. WSA는 Windows Server 관련 확장을 지원하도록 Windows 앱 패키지 설치 관리자를 확장하며, WSA가 드라이버 설치를 지원하지 않는 제한이 있습니다.

WSA 패키지를 만들어서 Nano 서버에 설치하려면 게시자와 패키지 소비자 양쪽의 개입이 필요합니다.

패키지 게시자는 다음을 수행해야 합니다.

1. [Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk)를 설치합니다. WSA 패키지를 만드는 데 필요한 MakeAppx, MakeCert, Pvk2Pfx, SignTool 도구가 포함되어 있습니다.
2. 매니페스트를 선언합니다. [WSA 매니페스트 확장 스키마](https://msdn.microsoft.com/library/windows/apps/mt670653.aspx)에 따라 AppxManifest.xml 매니페스트 파일을 만듭니다.
3. **MakeAppx** 도구를 사용하여 WSA 패키지를 만듭니다.
4. **MakeCert** 및 **Pvk2Pfx** 도구를 사용하여 인증서를 만든 다음 **Signtool**을 사용하여 패키지를 서명합니다.

다음으로 패키지 소비자는 다음 단계를 수행해야 합니다.

1. [  *Import-Certificate*](https://technet.microsoft.com/library/hh848630) PowerShell cmdlet을 실행하여 위의 4단계에서 만든 게시자의 인증서를 Nano 서버의 certStoreLocation인 “Cert:\LocalMachine\TrustedPeople”로 가져옵니다. 예를 들면 다음과 같습니다. `Import-Certificate -FilePath ".\xyz.cer" -CertStoreLocation "Cert:\LocalMachine\TrustedPeople"`
2. [  **Add-AppxPackage**](https://technet.microsoft.com/library/mt575516(v=wps.620).aspx) PowerShell cmdlet을 실행하여 Nano 서버에 응용 프로그램을 설치하고 Nano 서버에 WSA 패키지를 설치합니다. 예를 들면 다음과 같습니다. `Add-AppxPackage wsaSample.appx`

#### <a name="additional-resources-for-creating-apps"></a>앱 만들기에 대한 추가 리소스
WSA는 Microsoft Store에 호스트되지는 않지만 Windows 앱 패키지 기술의 서버 확장입니다. WSA를 사용하여 앱을 게시하려는 경우 다음 토픽이 앱 패키지 파이프라인을 익히는 데 도움을 줄 것입니다.

- [기본 패키지 매니페스트를 만드는 방법](https://msdn.microsoft.com/library/windows/desktop/br211475.aspx)
- [앱 패키지 작성 도구(MakeAppx.exe)](https://msdn.microsoft.com/library/windows/desktop/hh446767(v=vs.85).aspx)
- [앱 패키지 서명 인증서를 만드는 방법](https://msdn.microsoft.com/library/windows/desktop/jj835832(v=vs.85).aspx)
- [SignTool](https://msdn.microsoft.com/library/windows/desktop/aa387764(v=vs.85).aspx)

### <a name="installing-drivers-on-nano-server"></a>Nano 서버에 드라이버 설치
INF 드라이버 패키지를 사용하여 Nano 서버에 Microsoft 이외의 드라이버를 설치할 수 있습니다. 여기에는 플러그 앤 플레이(PnP) 드라이버 패키지와 파일 시스템 필터 드라이버 패키지가 모두 포함됩니다. 네트워크 필터 드라이버는 현재 Nano 서버에서 지원되지 않습니다.

PnP와 파일 시스템 필터 드라이버 패키지는 범용 드라이버 요구 사항 및 설치 프로세스뿐 아니라 서명 같은 일반 드라이버 패키지 지침도 준수해야 합니다. 그에 대한 설명은 다음 위치에서 확인할 수 있습니다.

- [드라이버 서명](https://msdn.microsoft.com/windows/hardware/drivers/install/driver-signing)
- [범용 INF 파일 사용](https://msdn.microsoft.com/windows/hardware/drivers/install/using-a-configurable-inf-file)

#### <a name="installing-driver-packages-offline"></a>오프라인으로 드라이버 패키지 설치

지원되는 드라이버 패키지는 [DISM.exe](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/dism-driver-servicing-command-line-options-s14) 또는 [DISM PowerShell](https://technet.microsoft.com/library/dn376497.aspx) cmdlet을 통해 오프라인으로 Nano 서버에 설치할 수 있습니다.

#### <a name="installing-driver-packages-online"></a>온라인으로 드라이버 패키지 설치
PnP 드라이버 패키지는 [PnpUtil](https://msdn.microsoft.com/library/windows/hardware/ff550419(v=vs.85).aspx)을 사용하여 온라인으로 Nano 서버에 설치할 수 있습니다. PnP 이외의 드라이버 패키지를 온라인으로 설치하는 방법은 현재 Nano 서버에서 지원되지 않습니다.






--------------------------------------------------  


## <a name="BKMK_JoinDomain"></a>Nano 서버를 도메인에 가입  

### <a name="to-add-nano-server-to-a-domain-online"></a>Nano 서버를 온라인으로 도메인에 추가하려면  

1.  이 명령을 사용하여 이미 Windows 임계값 서버를 실행 중인 도메인의 컴퓨터에서 데이터 blob을 수집합니다.  

    `djoin.exe /provision /domain <domain-name> /machine <machine-name> /savefile .\odjblob`  

    이렇게 하면 "odjblob"이라는 파일에 데이터 blob이 저장됩니다.  

2.  다음 명령을 사용하여 "odjblob" 파일을 Nano 서버 컴퓨터에 복사합니다.  

    **net use z: \\\\\<Nano 서버의 ip 주소>\c$**  

    > [!NOTE]  
    > net use 명령이 실패하면 Windows 방화벽 규칙을 조정해야 합니다. 이렇게 하려면 먼저 관리자 권한 명령 프롬프트를 열고, Windows PowerShell을 시작한 후 다음 명령을 사용하여 Windows PowerShell 원격 기능으로 Nano 서버 컴퓨터에 연결합니다.  
    >   
    > `Set-Item WSMan:\localhost\Client\TrustedHosts "<IP address of Nano Server>"`  
    >   
    > `$ip = "<ip address of Nano Server>"`  
    >   
    > `Enter-PSSession -ComputerName $ip -Credential $ip\Administrator`  
    >   
    > 메시지가 나타나면 관리자 암호를 입력한 다음 이 명령을 실행하여 방화벽 규칙을 설정합니다.  
    >   
    > **netsh advfirewall firewall set rule group="File and Printer Sharing" new enable=yes**  
    >   
    > `Exit-PSSession`을 사용하여 Windows PowerShell을 종료한 다음 net use 명령을 다시 시도합니다. 명령이 성공하면 계속해서 Nano 서버에 "odjblob" 파일 콘텐츠를 복사합니다.  

    **md z:\Temp**  

    **copy odjblob z:\Temp**  

3.  Nano 서버를 가입하려는 도메인을 확인하고 해당 DNS가 구성되었는지 확인합니다. 또한 도메인 또는 도메인 컨트롤러의 이름 확인이 예상대로 작동하는지 확인합니다. 이렇게 하려면 먼저 관리자 권한 명령 프롬프트를 열고, Windows PowerShell을 시작한 후 다음 명령을 사용하여 Windows PowerShell 원격 기능으로 Nano 서버 컴퓨터에 연결합니다.  

    `Set-Item WSMan:\localhost\Client\TrustedHosts "<IP address of Nano Server>"`  

    `$ip = "<ip address of Nano Server>"`  

    `Enter-PSSession -ComputerName $ip -Credential $ip\Administrator`  

    메시지가 나타나면 관리자 암호를 입력합니다. Nano 서버에서는 Nslookup을 사용할 수 없으므로 Resolve-DNSName을 사용하여 이름 확인을 검증할 수 있습니다.

4. 이름 확인에 성공하면 동일한 Windows PowerShell 세션에서 이 명령을 실행하여 도메인에 가입합니다.  

    `djoin /requestodj /loadfile c:\Temp\odjblob /windowspath c:\windows /localos`  

5.  Nano 서버 컴퓨터를 다시 시작한 다음 Windows PowerShell 세션을 종료합니다.  

    `shutdown /r /t 5`  

    `Exit-PSSession`  

6.  Nano 서버를 도메인에 가입한 후에는 Nano 서버의 관리자 그룹에 도메인 사용자 계정을 추가합니다.

7. 보안을 위해 이 명령을 사용하여 신뢰할 수 있는 호스트 목록에서 Nano 서버를 제거합니다.`Set-Item WSMan:\localhost\client\TrustedHosts ""` 

**한 번에 도메인에 가입하는 대체 방법**  

먼저 이 명령을 사용하여 이미 도메인에 있는 Windows 임계값 서버를 실행 중인 다른 컴퓨터에서 데이터 blob을 수집합니다.  

`djoin.exe /provision /domain <domain-name> /machine <machine-name> /savefile .\odjblob`  

"odjblob" 파일을 열고(메모장에서), 콘텐츠를 복사한 다음 아래 Unattend.xml 파일의 \<AccountData> 섹션에 붙여 넣습니다.  

이 Unattend.xml 파일을 C:\NanoServer 폴더에 넣은 후, 다음 명령을 사용하여 VHD를 탑재하고 `offlineServicing` 섹션의 설정을 적용합니다.  

**dism\dism /Mount-ImagemediaFile:.\NanoServer.vhd /Index:1 /MountDir:.\mountdir**  

**dism\dismmedia:.\mountdir /Apply-Unattend:.\unattend.xml**  

"Panther" 폴더를 만들고(설치하는 동안 Windows 시스템에서 파일을 저장하는 데 사용하며, 자세한 내용은 [Windows 7, Windows Server 2008 R2 및 Windows Vista 설치 로그 파일 위치](https://support.microsoft.com/en-us/kb/927521) 참조), 이 폴더에 Unattend.xml 파일을 복사하고, 다음 명령을 사용하여 VHD를 탑재 해제합니다.  

**md .\mountdir\windows\panther**  

**copy .\unattend.xml .\mountdir\windows\panther**  

**dism\dism /Unmount-Image /MountDir:.\mountdir /Commit**  

이 VHD에서 처음으로 Nano 서버를 부팅하면 다른 설정이 적용됩니다.  

Nano 서버를 도메인에 가입한 후에는 Nano 서버의 관리자 그룹에 도메인 사용자 계정을 추가합니다.  

## <a name="working-with-server-roles-on-nano-server"></a>Nano 서버에서 서버 역할 작업

### <a name="using-hyper-v-on-nano-server"></a>Nano 서버에 Hyper-V 사용  
Hyper-V는 Windows Server의 Server Core 모드에서 작동하는 것과 똑같은 방식으로 Nano 서버에서 작동하지만, 두 가지 예외가 있습니다.  

-   모든 관리를 원격으로 수행해야 하며 관리 컴퓨터가 Nano 서버와 동일한 Windows Server 빌드를 실행해야 합니다. 이전 버전의 Hyper-V 관리자 또는 Hyper-V Windows PowerShell cmdlet은 작동하지 않습니다.  

-   RemoteFX는 사용할 수 없습니다.  

이 릴리스에서는 다음 Hyper-V 기능이 검증되었습니다.  

-   Hyper-V를 사용하도록 설정  

-   1세대 및 2세대 가상 컴퓨터 만들기  

-   가상 스위치 만들기  

-   가상 컴퓨터를 시작하고 Windows 게스트 운영 체제를 실행  
- Hyper-V 복제본  



가상 머신을 실시간으로 마이그레이션하려면 SMB 공유에 가상 머신을 만들거나 기존 SMB 공유에 있는 리소스를 기존 가상 머신에 연결해야 합니다. 인증을 올바르게 구성하는 것이 중요합니다. 이 작업을 수행하는 두 가지 옵션이 있습니다.  

**제한된 위임**  

제한된 위임은 이전 릴리스와 정확히 동일한 방식으로 작동합니다. 자세한 내용은 다음 문서를 참조하세요.  

-   [Hyper-V 원격 관리를 사용하도록 설정 - SMB 및 항상 사용 가능한 SMB에 대해 제한된 위임 구성](http://blogs.msdn.com/b/taylorb/archive/2012/03/20/enabling-hyper-v-remote-management-configuring-constrained-delegation-for-smb-and-highly-available-smb.aspx)  

-   [Hyper-V 원격 관리를 사용하도록 설정 - 클러스터링되지 않은 실시간 마이그레이션에 대해 제한된 위임 구성](http://blogs.msdn.com/b/taylorb/archive/2012/03/20/enabling-hyper-v-remote-management-configuring-constrained-delegation-for-non-clustered-live-migration.aspx)  

**CredSSP**  

먼저 이 토픽의 "Windows PowerShell 원격 기능 사용" 섹션을 참조하여 CredSSP를 사용하도록 설정하고 테스트하세요. 그런 다음 관리 컴퓨터에서 Hyper-V 관리자를 사용하여 "다른 사용자로 연결" 옵션을 선택합니다. Hyper-V 관리자가 CredSSP를 사용할 것입니다. 현재 계정을 사용하는 경우 이 작업을 수행해야 합니다.  

Hyper-V용 Windows PowerShell cmdlet은 CimSession 또는 Credential 매개 변수 중 CredSSP와 호환되는 것을 사용할 수 있습니다.  

### <a name="BKMK_Failover"></a>Nano 서버에서 장애 조치(failover) 클러스터링 사용  
장애 조치(failover) 클러스터링은 Windows Server의 Server Core 모드에서 작동하는 것과 동일한 방식으로 Nano 서버에서 작동하지만 않지만 다음 사항을 염두에 두어야 합니다.  

-   장애 조치(Failover) 클러스터 관리자 또는 Windows PowerShell을 사용하여 클러스터를 원격으로 관리해야 합니다.  

-   모든 Nano 서버 클러스터 노드는 Windows Server의 클러스터 노드와 마찬가지로 동일한 도메인에 가입되어야 합니다.  

-   도메인 계정은 Windows Server의 클러스터 노드와 마찬가지로 모든 Nano 서버 노드에 대한 관리자 권한을 갖고 있어야 합니다.  

-   모든 명령은 관리자 권한 명령 프롬프트에서 실행해야 합니다.  

> [!NOTE]  
> 또한 일부 기능은 이 릴리스에서 지원되지 않습니다.  
>   
> -   로컬 Nano 서버에서 Windows PowerShell을 통해 장애 조치(failover) 클러스터링 cmdlet을 실행할 수 없습니다.  
> -   Hyper-V 및 파일 서버 이외의 다른 역할을 클러스터링합니다.  

다음 Windows PowerShell cmdlet은 장애 조치(failover) 클러스터 관리에 매우 유용하게 사용됩니다.  

다음 명령으로 새 클러스터를 만들 수 있습니다. `New-Cluster -Name <clustername> -Node <comma-separated cluster node list>`  

새 클러스터를 설정했으면 모든 노드에서 `Set-StorageSetting -NewDiskPolicy OfflineShared`를 실행해야 합니다.  

다음 명령으로 클러스터에 노드 추가 `Add-ClusterNode -Name <comma-separated cluster node list>  -Cluster <clustername>`  

다음 명령으로 클러스터에서 노드 제거 `Remove-ClusterNode -Name <comma-separated cluster node list>  -Cluster <clustername>`  

다음 명령으로 스케일 아웃 파일 서버 만들기 `Add-ClusterScaleoutFileServerRole -name <sofsname> -cluster <clustername>`  

[Microsoft.FailoverClusters.PowerShell](https://technet.microsoft.com/library/ee461009.aspx)에서 장애 조치(failover) 클러스터링에 대한 추가 cmdlet을 찾을 수 있습니다.  

### <a name="BKMK_DNS"></a>Nano 서버에서 DNS 서버 사용  
Nano 서버에 DNS 서버 역할을 제공하려면 이미지에 Microsoft-NanoServer-DNS-Package를 추가합니다(이 토픽의 "사용자 지정 Nano 서버 이미지 만들기" 참조). Nano 서버가 실행되면 Nano 서버에 연결한 후 관리자 권한 Windows PowerShell 콘솔에서 다음 명령을 실행하여 이 기능을 사용하도록 설정합니다.  

`Enable-WindowsOptionalFeature -Online -FeatureName DNS-Server-Full-Role`  

### <a name="BKMK_IIS"></a>Nano 서버에서 IIS 사용  
IIS(인터넷 정보 서비스) 역할을 사용하는 단계는 [Nano 서버의 IIS](IIS-on-Nano-Server.md)를 참조하세요. 

### <a name="using-mpio-on-nano-server"></a>Nano Server에서 MPIO 사용
MPIO를 사용하는 단계는 [Nano 서버의 MPIO](MPIO-on-Nano-Server.md)를 참조하세요. 

### <a name="BKMK_SSH"></a>Nano 서버에서 SSH 사용
Nano 서버에 SSH를 설치하고 OpenSSH 프로젝트에 사용하는 방법에 대한 자세한 지침은 [Win32-OpenSSH wiki](https://github.com/PowerShell/Win32-OpenSSH/wiki)를 참조하세요.

## <a name="appendix-sample-unattendxml-file-that-joins-nano-server-to-a-domain"></a>부록: Nano 서버를 도메인에 가입하는 샘플 Unattend.xml 파일  

> [!NOTE]  
> "odjblob"을 무인 파일에 붙여 넣을 때 odjblob 콘텐츠의 후행 공백을 삭제해야 합니다.  

```  
<?xml version='1.0' encoding='utf-8'?>  
<unattend xmlns="urn:schemas-microsoft-com:unattend" xmlns:wcm="https://schemas.microsoft.com/WMIConfig/2002/State" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  

  <settings pass="offlineServicing">  
    <component name="Microsoft-Windows-UnattendedJoin" processorArchitecture="amd64" publicKeyToken="31bf3856ad364e35" language="neutral" versionScope="nonSxS">  
        <OfflineIdentification>                
           <Provisioning>    
             <AccountData> AAAAAAARUABLEABLEABAoAAAAAAAMABSUABLEABLEABAwAAAAAAAAABbMAAdYABc8ABYkABLAABbMAAEAAAAMAAA0ABY4ABZ8ABbIABa0AAcIABY4ABb8ABZUABAsAAAAAAAQAAZoABNUABOYABZYAANQABMoAAOEAAMIAAOkAANoAAMAAAXwAAJAAAAYAAA0ABY4ABZ8ABbIABa0AAcIABY4ABb8ABZUABLEAALMABLQABU0AATMABXAAAAAAAKdf/mhfXoAAUAAAQAAAAb8ABLQABbMABcMABb4ABc8ABAIAAAAAAb8ABLQABbMABcMABb4ABc8ABLQABb0ABZIAAGAAAAsAAR4ABTQABUAAAAAAACAAAQwABZMAAZcAAUgABVcAAegAARcABKkABVIAASwAAY4ABbcABW8ABQoAAT0ABN8AAO8ABekAAJMAAVkAAZUABckABXEABJUAAQ8AAJ4AAIsABZMABdoAAOsABIsABKkABQEABUEABIwABKoAAaAABXgABNwAAegAAAkAAAAABAMABLIABdIABc8ABY4AADAAAA4AAZ4ABbQABcAAAAAAACAAkKBW0ID8nJDWYAHnBAXE77j7BAEWEkl+lKB98XC2G0/9+Wd1DJQW4IYAkKBAADhAnKBWEwhiDAAAM2zzDCEAM6IAAAgAAAAAAAQAAAAAAAAAAAABwzzAAA  
</AccountData>  
           </Provisioning>    
         </OfflineIdentification>    
    </component>  
  </settings>  

  <settings pass="oobeSystem">  
    <component name="Microsoft-Windows-Shell-Setup" processorArchitecture="amd64" publicKeyToken="31bf3856ad364e35" language="neutral" versionScope="nonSxS">  
      <UserAccounts>  
        <AdministratorPassword>  
           <Value>Tuva</Value>  
           <PlainText>true</PlainText>  
        </AdministratorPassword>  
      </UserAccounts>  
      <TimeZone>Pacific Standard Time</TimeZone>  
    </component>  
  </settings>  

  <settings pass="specialize">  
    <component name="Microsoft-Windows-Shell-Setup" processorArchitecture="amd64" publicKeyToken="31bf3856ad364e35" language="neutral" versionScope="nonSxS">  
      <RegisteredOwner>My Team</RegisteredOwner>  
      <RegisteredOrganization>My Corporation</RegisteredOrganization>  
    </component>  
  </settings>  
</unattend>  
```  

