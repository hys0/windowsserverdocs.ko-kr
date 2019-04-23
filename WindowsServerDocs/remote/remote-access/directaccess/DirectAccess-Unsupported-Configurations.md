---
title: DirectAccess에서 지원되지 않는 구성
description: 이 항목에서는 Windows Server 2016에서 지원 되지 않는 DirectAccess 구성의 목록을 제공합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-da
ms.topic: article
ms.assetid: 23d05e61-95c3-4e70-aa83-b9a8cae92304
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 49fa86883e6a590ac8f7dcf0c724f87af419f88e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828854"
---
# <a name="directaccess-unsupported-configurations"></a>DirectAccess에서 지원되지 않는 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

배포를 다시 시작할 필요가 없도록 하려면 배포를 시작 하기 전에 다음과 같은 지원 되지 않는 DirectAccess 구성 검토 합니다.  

## <a name="bkmk_frs"></a>그룹 정책 개체 (SYSVOL 복제)의 파일 복제 서비스 FRS () 배포  
도메인 컨트롤러 복제 서비스 FRS (파일) 배포 그룹 정책 개체 (SYSVOL 복제)를 실행 하는 환경에서 DirectAccess를 배포 하지 않습니다. FRS.를 사용 하는 경우에 directaccess 배포가 지원 되지 않습니다.  
  
Windows Server 2003 또는 Windows Server 2003 R2를 실행 하는 도메인 컨트롤러가 있는 경우 FRS를 사용 하는 합니다. 또한 사용할 수 있습니다 FRS 경우 이전에 Windows 2000 Server 또는 Windows Server 2003 도메인 컨트롤러 되지 SYSVOL 복제에서에서 마이그레이션한 FRS 분산 파일 시스템 복제 (Dfs-r)에 있습니다.  
  
FRS SYSVOL 복제를 사용 하 여 DirectAccess를 배포 하는 경우 DirectAccess 서버 및 클라이언트 구성 정보를 포함 하는 위험 의도치 않은 삭제 DirectAccess 그룹 정책 개체입니다. 이러한 개체가 삭제 하는 경우에 DirectAccess 배포에는 중단 저하 되 고 DirectAccess를 사용 하는 클라이언트 컴퓨터는 네트워크에 연결할 수 없습니다.  
  
DirectAccess를 배포 하려는 경우 Windows Server 2003 R2 이상의 운영 체제를 실행 하는 도메인 컨트롤러를 사용 해야 하 고. DFS를 사용 해야 합니다.  
  
FRS에서 DFS-R로 마이그레이션에 대 한 내용은 참조는 [SYSVOL 복제 마이그레이션 가이드: FRS에서 DFS 복제로](https://technet.microsoft.com/library/dd640019(v=ws.10).aspx)합니다.  
  
## <a name="bkmk_nap"></a>DirectAccess 클라이언트에 대 한 네트워크 액세스 보호  
네트워크 액세스 보호 (NAP)는 원격 클라이언트 컴퓨터가 회사 네트워크에 대 한 액세스를 부여 하기 전에 IT 정책을 충족 하는지 확인 하는 데 사용 됩니다. NAP는 Windows Server 2012 R2에 사용이 중단 및 Windows Server 2016에 포함 되지 않습니다. 이러한 이유로 NAP를 사용 하 여 DirectAccess의 새 배포를 시작 권장 되지 않습니다. DirectAccess 클라이언트의 보안에 대 한 끝점 컨트롤의 다른 메서드를 사용 하는 것이 좋습니다.  
  
## <a name="bkmk_multi"></a>Windows 7 클라이언트에 대 한 멀티 사이트 지원  
DirectAccess 멀티 사이트 배포에서 Windows 10 구성 된 경우&reg;, Windows&reg; 8.1 및 Windows&reg; 8 클라이언트를 가장 가까운 사이트로 연결 하는 기능이 있습니다.  Windows 7&reg; 클라이언트 컴퓨터가 동일한 기능이 없습니다. Windows 7 클라이언트에 대 한 사이트 선택 정책 구성 시 특정 사이트에 설정 되어 및 이러한 클라이언트는 항상 해당 위치에 관계 없이 지정 된 사이트에 연결 됩니다.  
  
## <a name="bkmk_user"></a>사용자 기반 액세스 제어  
DirectAccess 정책을 따라, 컴퓨터 기반 사용자가 아닌 경우 회사 네트워크에 대 한 액세스를 제어 하는 DirectAccess 사용자 정책을 지정 하는 것은 지원 되지 않습니다.  
  
## <a name="bkmk_policy"></a>DirectAccess 정책을 사용자 지정  
DirectAccess는 DirectAccess 설치 마법사, 원격 액세스 관리 콘솔 또는 원격 액세스 Windows PowerShell cmdlet을 사용 하 여 구성할 수 있습니다. DirectAccess 설치 마법사 이외의 모든 수단을 사용 하 여 DirectAccess를 구성, DirectAccess 그룹 정책 개체를 직접 수정 하거나 서버 또는 클라이언트의 기본 정책 설정을 수동으로 수정 등 지원 되지 않습니다. 이러한 수정 사항을 사용할 수 없는 구성 될 수 있습니다.  
  
## <a name="bkmk_kerb"></a>KerbProxy 인증  
시작 마법사를 사용 하 여 DirectAccess 서버를 구성할 때 DirectAccess 서버는 자동으로 컴퓨터에 대 한 KerbProxy 인증과 사용자 인증을 사용 하도록 구성 됩니다. 이 때문에 사용 해야 시작 마법사 단일 사이트 배포에 있는 Windows 10&reg;, Windows 8.1 또는 Windows 8 클라이언트를 배포 합니다.  
  
또한 다음과 같은 기능이 해서는 안 KerbProxy 인증을 사용 합니다.  
  
-   외부 부하 분산 장치 또는 Windows 로드를 사용 하 여 분산   
    분산 장치  
  
-   스마트 카드 또는 OTP (일회용 암호)은 필요한 2 단계 인증  
  
KerbProxy 인증을 사용 하는 경우에 다음 배포 계획은 지원 되지 않습니다.  
  
-   멀티 사이트입니다.  
  
-   DirectAccess는 Windows 7 클라이언트에 대 한 지원.  
  
-   강제 터널링 합니다. KerbProxy 인증 강제 터널링을 사용 하는 경우 사용 되지 않습니다 되도록 마법사를 실행 하는 동안 다음 항목을 구성 합니다.  
  
    -   강제 터널링을 사용 하도록 설정  
  
    -   DirectAccess에 대 한 Windows 7 클라이언트를 사용 하도록 설정  
  
> [!NOTE]  
> 이전 배포의 경우 인증서 기반 컴퓨터 및 사용자 인증을 사용 하 여 이중 터널 구성을 사용 하는 고급 구성 마법사를 사용 해야 합니다. 자세한 내용은 [고급 설정을 사용 하 여 단일 DirectAccess 서버 배포](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)합니다.  
  
## <a name="bkmk_isa"></a>ISATAP를 사용 하 여  
ISATAP는 IPv4 전용 회사 네트워크에서 IPv6 연결을 제공 하는 전환 기술입니다. 단일 DirectAccess 서버 배포를 사용 하 여 소규모 및 중간 규모 조직은 제한 됩니다 및 DirectAccess 클라이언트를 원격으로 관리할 수 있습니다. ISATAP deployedin 멀티 사이트, 부하 분산 또는 환경과 경우 제거 하거나 DirectAccess를 구성 하기 전에 네이티브 IPv6 배포로 이동 해야 합니다.  
  
## <a name="bkmk_iphttps"></a>IPHTTPS 및 OTP (일회용 암호) 끝점 구성  
IPHTTPS를 사용 하는 경우 IPHTTPS 연결 부하 분산 장치 등의 다른 장치에 없는 DirectAccess 서버에서 종료 해야 합니다. 마찬가지로, OTP (일회용 암호) 인증 중에 만든 대역의 Secure Sockets Layer (SSL) 연결 DirectAccess 서버에서 종료 해야 합니다. 이러한 연결 끝점 사이의 모든 장치는 통과 모드로 구성 되어야 합니다.  
  
## <a name="bkmk_ft"></a>OTP 인증을 사용 하 여 강제 터널  
OTP 및 강제 터널링을 사용 하 여 2 단계 인증을 사용 하 여 DirectAccess 서버를 배포 하지 않습니다 또는 OTP 인증에 실패 합니다. 에서는 대역의 Secure Sockets Layer (SSL) 연결을 DirectAccess 서버와 DirectAccess 클라이언트가 필요 합니다. 이 연결 DirectAccess 터널 외부 트래픽을 보내도록 예외가 필요 합니다. 강제 터널 구성에서 모든 트래픽이 DirectAccess 터널을 통과 해야 하 고 없음 예외는 터널이 설정 되 면 허용 됩니다. 이 인해 없습니다 강제 터널 구성에서 OTP 인증을 해야 합니다.  
  
## <a name="bkmk_rodc"></a>읽기 전용 도메인 컨트롤러를 사용 하 여 DirectAccess를 배포합니다.  
DirectAccess 서버 읽기 전용 도메인 컨트롤러에 액세스할 수 있어야 하 고 읽기 전용 도메인 컨트롤러 (RODC) 사용 하 여 제대로 작동 하지 않습니다.  
  
읽기 전용 도메인 컨트롤러는 다음과 같은 여러 가지 이유로 필요 합니다.  
  
-   DirectAccess 서버에서 읽기 전용 도메인 컨트롤러를 원격 액세스 Microsoft Management Console (MMC)을 열려면 필요 합니다.  
  
-   DirectAccess 서버 읽기 및 DirectAccess 클라이언트와 DirectAccess 서버 그룹 정책 개체 (Gpo)를 작성 해야 합니다.  
  
-   DirectAccess 서버를 읽고 주 도메인 컨트롤러 에뮬레이터 (PDCe)에서 특히 클라이언트 GPO에 씁니다.  
  
이러한 요구 사항으로 인해 RODC 사용 하 여 DirectAccess를 배포 하지 않습니다.  
  


