---
title: Nano 서버 빠른 시작
description: 실제 또는 가상 컴퓨터에서 기본적인 Nano 서버를 신속하게 배포하는 단계
ms.prod: windows-server-threshold
ms.service: na
manager: DonGill
ms.technology: server-nano
ms.date: 09/05/2017
ms.tgt_pltfrm: na
ms.topic: get-started-article
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: 7c1623e365be71cac2fd58da5444ce4358d75309
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443563"
---
# <a name="nano-server-quick-start"></a>Nano 서버 빠른 시작

>적용 대상: Windows Server 2016

> [!IMPORTANT]
> Windows Server, 버전 1709부터 [컨테이너 기본 OS 이미지](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image)로만 Nano 서버를 사용할 수 있습니다. [Nano 서버 변경 사항](nano-in-semi-annual-channel.md)을 확인하여 그 의미를 알아보세요. 

이 섹션의 단계에 따라 DHCP로 IP 주소를 가져와서 신속하게 Nano 서버 기본 배포를 시작합니다. 가상 컴퓨터에서 Nano 서버 VHD를 실행하거나 물리적 컴퓨터에서 부팅을 실행할 수 있습니다. 단계는 약간 다릅니다.

이러한 빠른 시작 단계로 기본 사항을 시도한 후에는 [Nano 서버 배포](Deploy-Nano-Server.md)에 나와 있는 다양한 방법, 도메인 작업 등으로 고유한 사용자 지정 이미지, 패키지 관리를 만드는 정보를 확인할 수 있습니다.
  
**가상 컴퓨터에서 Nano Server**  
  
다음 단계에 따라 가상 컴퓨터에서 실행할 Nano 서버 VHD를 만듭니다.  
  
## <a name="to-quickly-deploy-nano-server-in-a-virtual-machine"></a>가상 컴퓨터에서 Nano 서버를 신속하게 배포하려면  
  
1. Windows Server 2016 ISO의 \NanoServer 폴더에서 하드 드라이브의 폴더로 *NanoServerImageGenerator* 폴더를 복사합니다.  
  
2. 관리자, NanoServerImageGenerator 폴더가 배치 하 고 사용 하 여 모듈을 가져와서 있는 폴더로 디렉터리를 변경으로 Windows PowerShell 시작 `Import-Module .\NanoServerImageGenerator -Verbose`  
   >[!NOTE]  
   >Windows PowerShell 실행 정책을 조정해야 합니다. `Set-ExecutionPolicy RemoteSigned` 제대로 작동 해야 합니다.  
  
3. 다음 명령을 실행하여 컴퓨터 이름을 설정하고 Hyper-V **게스트 드라이버**를 포함하는 Standard 버전용 VHD를 만듭니다. 명령을 실행하면 새 VHD에 대한 관리자 암호를 묻는 메시지가 표시됩니다.  
  
   `New-NanoServerImage -Edition Standard -DeploymentType Guest -MediaPath <path to root of media> -BasePath .\Base -TargetPath .\NanoServerVM\NanoServerVM.vhd -ComputerName <computer name>` 위치  
  
   -   **-MediaPath <미디어의 루트 경로\>** 는 Windows Server 2016 ISO의 콘텐츠에 대한 루트 경로를 지정합니다. 예를 들어 ISO의 콘텐츠를 해당 경로를 사용하는 d:\TP5ISO로 복사한 경우가 있습니다.  
  
   -   **-BasePath**(선택 사항)는 Nano 서버 WIM 및 패키지를 복사하기 위해 생성할 폴더를 지정합니다.  
  
   -   **-TargetPath**는 파일 이름 및 확장명을 포함한 경로를 지정합니다. 이 경로에 결과 VHD 또는 VHDX가 만들어집니다.  
  
   -   **Computer_name**은 생성 중인 Nano 서버 가상 컴퓨터가 보유할 컴퓨터 이름을 지정합니다.  
  
   **예:** `New-NanoServerImage -Edition Standard -DeploymentType Guest -MediaPath f:\ -BasePath .\Base -TargetPath .\Nano1\Nano.vhd -ComputerName Nano1`  
  
   이 예에서는 f:\\로 탑재된 ISO에서 VHD를 만듭니다. VHD를 만들면 New-NanoServerImage를 실행했던 것과 동일한 디렉터리에 있는 Base라는 폴더를 사용하고 Nano1이라는 폴더의 VHD(Nano.vhd)를 명령이 실행되는 폴더에 배치합니다. 컴퓨터 이름은 Nano1이 됩니다. 결과 VHD에는 Standard 버전의 Windows Server 2016이 포함되고 VHD는 Hyper-V 가상 컴퓨터 배포에 적합하게 됩니다. 1세대 가상 컴퓨터를 원하는 경우 -TargetPath에 대해 **.vhd** 확장명을 지정하여 VHD 이미지를 만듭니다. 2세대 가상 컴퓨터의 경우 -TargetPath에 대해 **.vhdx** 확장명을 지정하여 VHDX 이미지를 만듭니다. -TargetPath에 대해 **.wim** 확장명을 지정하여 WIM 파일을 직접 생성합니다.  
  
   > [!NOTE]  
   > New-NanoServerImage는 Windows 8.1, Windows 10, Windows Server 2012 R2 및 Windows Server 2016에서 지원됩니다.  
  
4. Hyper-V 관리자에서 새 가상 컴퓨터를 만들고 3단계에서 만든 VHD를 사용합니다.  
  
5. 가상 컴퓨터를 부팅한 다음 Hyper-V 관리자에서 가상 컴퓨터에 연결합니다.  
  
6. 3단계의 스크립트를 실행하는 동안 제공했던 관리자 및 암호를 사용하여 복구 콘솔에 로그온합니다(이 가이드의 "Nano 서버 복구 콘솔" 섹션 참조).  
   > [!NOTE]  
   > 복구 콘솔은 기본적인 키보드 기능만 지원합니다. 키보드 표시등, 10-키 섹션, 키보드 레이아웃 전환(예: caps lock 및 number lock)은 지원되지 않습니다.
  
7. Nano 서버 가상 컴퓨터의 IP 주소를 가져오고 Windows PowerShell 원격 기능 또는 기타 원격 관리 도구를 사용하여 가상 컴퓨터에 연결하여 원격으로 관리합니다.  
  
**물리적 컴퓨터에서 Nano Server**  
  
미리 설치된 장치 드라이버를 사용하여 물리적 컴퓨터에서 Nano 서버를 실행할 VHD를 만들 수도 있습니다. 사용자의 하드웨어를 부팅 또는 네트워크에 연결하기 위해서 아직 제공되지 않은 드라이버가 필요한 경우 이 가이드의 "드라이버 추가" 섹션의 단계를 따릅니다.  
  
## <a name="to-quickly-deploy-nano-server-on-a-physical-computer"></a>물리적 컴퓨터에서 Nano 서버를 신속하게 배포하려면  
  
1.  Windows Server 2016 ISO의 \NanoServer 폴더에서 하드 드라이브의 폴더로 *NanoServerImageGenerator* 폴더를 복사합니다.  
  
2.  관리자, NanoServerImageGenerator 폴더가 배치 하 고 사용 하 여 모듈을 가져와서 있는 폴더로 디렉터리를 변경으로 Windows PowerShell 시작 `Import-Module .\NanoServerImageGenerator -Verbose`  
  
>[!NOTE]  
>Windows PowerShell 실행 정책을 조정해야 합니다. `Set-ExecutionPolicy RemoteSigned` 제대로 작동 해야 합니다.  
  
3. 다음 명령을 실행하여 컴퓨터 이름을 설정하고 OEM 드라이버를 포함하는 VHD를 만듭니다. 명령을 실행하면 새 VHD에 대한 관리자 암호를 묻는 메시지가 표시됩니다.  
  
   `New-NanoServerImage -Edition Standard -DeploymentType Host -MediaPath <path to root of media> -BasePath .\Base -TargetPath .\NanoServerPhysical\NanoServer.vhd -ComputerName <computer name> -OEMDrivers -Compute -Clustering` 위치  
  
   -   **-MediaPath <미디어의 루트 경로\>** 는 Windows Server 2016 ISO의 콘텐츠에 대한 루트 경로를 지정합니다. 예를 들어 ISO의 콘텐츠를 해당 경로를 사용하는 d:\TP5ISO로 복사한 경우가 있습니다.  
  
   -   **BasePath**는 Nano 서버 WIM 및 패키지를 복사하기 위해 생성할 폴더를 지정합니다. (이 매개 변수는 선택 사항입니다.)  
  
   -   **TargetPath**는 파일 이름 및 확장명을 포함한 경로를 지정합니다. 이 경로에 결과 VHD 또는 VHDX가 만들어집니다.  
  
   -   **Computer_name**은 생성 중인 Nano 서버의 컴퓨터 이름입니다.  
  
   **예:** `New-NanoServerImage -Edition Standard -DeploymentType Host -MediaPath F:\ -BasePath .\Base -TargetPath .\Nano1\NanoServer.vhd -ComputerName Nano-srv1 -OEMDrivers -Compute -Clustering`  
  
   이 예에서는 F:\\로 탑재된 ISO에서 VHD를 만듭니다. VHD를 만들면 New-NanoServerImage를 실행했던 것과 동일한 디렉터리에 있는 Base라는 폴더를 사용하고 Nano1이라는 폴더의 VHD를 명령이 실행되는 폴더에 배치합니다. 컴퓨터 이름은 Nano-srv1이 되고 대부분의 일반적인 하드웨어에 대해 OEM 드라이버가 설치되며 Hyper-V 역할 및 클러스터링 기능을 사용할 수 있습니다. Standard Nano 버전이 사용됩니다.  
  
4. Nano 서버 VHD를 실행하려는 물리적 서버에 관리자로 로그인합니다.  
  
5. 이 스크립트가 물리적 컴퓨터에 생성할 VHD를 복사하고 이 새로운 VHD에서 부팅하도록 구성합니다. 이를 위해 다음 단계를 수행합니다.  
  
   1.  생성된 VHD를 탑재합니다. 이 예에서는 D:\\ 아래에 탑재됩니다.  
  
   2.  **bcdboot d:\windows**를 실행합니다.  
  
   3.  VHD를 분리합니다.  
  
6. 물리적 컴퓨터를 Nano 서버 VHD로 부팅합니다.  
  
7. 3단계의 스크립트를 실행하는 동안 제공했던 관리자 및 암호를 사용하여 복구 콘솔에 로그온합니다(이 가이드의 "Nano 서버 복구 콘솔" 섹션 참조).
   > [!NOTE]  
   > 복구 콘솔은 기본적인 키보드 기능만 지원합니다. 키보드 표시등, 10-키 섹션, 키보드 레이아웃 전환(예: caps lock 및 number lock)은 지원되지 않습니다. 
  
8. Nano 서버 컴퓨터의 IP 주소를 가져오고 Windows PowerShell 원격 기능 또는 기타 원격 관리 도구를 사용하여 가상 컴퓨터에 연결하여 원격으로 관리합니다.  
