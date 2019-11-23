---
title: DirectAccess에서 지원되지 않는 구성
description: 이 항목에서는 Windows Server 2016에서 지원 되지 않는 DirectAccess 구성 목록을 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 23d05e61-95c3-4e70-aa83-b9a8cae92304
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5e652083d4accf90b542a16d51e314299303954f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388844"
---
# <a name="directaccess-unsupported-configurations"></a>DirectAccess에서 지원되지 않는 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

배포를 다시 시작할 필요가 없도록 배포를 시작 하기 전에 다음의 지원 되지 않는 DirectAccess 구성 목록을 검토 하세요.  

## <a name="bkmk_frs"></a>그룹 정책 개체의 FRS (파일 복제 서비스) 배포 (SYSVOL 복제)  
도메인 컨트롤러에서 그룹 정책 개체 (SYSVOL 복제)를 배포 하기 위해 FRS (파일 복제 서비스)를 실행 하는 환경에 DirectAccess를 배포 하지 마십시오. FRS를 사용 하는 경우 DirectAccess 배포가 지원 되지 않습니다.  
  
Windows Server 2003 또는 Windows Server 2003 r 2를 실행 하는 도메인 컨트롤러가 있는 경우 FRS를 사용 합니다. 또한 이전에 Windows 2000 서버 또는 Windows Server 2003 도메인 컨트롤러를 사용 하 고 FRS에서 분산 파일 시스템 복제 (DFS-R)로 SYSVOL 복제를 마이그레이션하지 않은 경우 FRS를 사용할 수 있습니다.  
  
FRS SYSVOL 복제를 사용 하 여 DirectAccess를 배포 하는 경우 directaccess 서버 및 클라이언트 구성 정보를 포함 하는 개체 그룹 정책 DirectAccess를 의도 하지 않게 삭제할 위험이 있습니다. 이러한 개체가 삭제 되 면 DirectAccess 배포는 중단 되 고 DirectAccess를 사용 하는 클라이언트 컴퓨터는 네트워크에 연결할 수 없습니다.  
  
DirectAccess를 배포 하려는 경우 Windows Server 2003 R2 이후 버전의 운영 체제를 실행 하는 도메인 컨트롤러를 사용 해야 하며, DFS-R을 사용 해야 합니다.  
  
FRS에서 DFS-R로 마이그레이션하는 방법에 대 한 자세한 내용은 [SYSVOL 복제 마이그레이션 가이드: frs to DFS 복제](https://technet.microsoft.com/library/dd640019(v=ws.10).aspx)를 참조 하세요.  
  
## <a name="bkmk_nap"></a>DirectAccess 클라이언트에 대 한 네트워크 액세스 보호  
NAP (네트워크 액세스 보호)는 원격 클라이언트 컴퓨터가 회사 네트워크에 대 한 액세스 권한을 부여 하기 전에 해당 정책을 충족 하는지 여부를 확인 하는 데 사용 됩니다. NAP는 Windows Server 2012 r 2에서 사용 되지 않으며 Windows Server 2016에는 포함 되어 있지 않습니다. 이러한 이유로 NAP를 사용 하 여 DirectAccess를 새로 배포 하는 것은 권장 되지 않습니다. DirectAccess 클라이언트 보안을 위한 다른 끝점 제어 방법이 권장 됩니다.  
  
## <a name="bkmk_multi"></a>Windows 7 클라이언트에 대 한 멀티 사이트 지원  
DirectAccess를 멀티 사이트 배포에 구성 하면 Windows 10&reg;, Windows&reg; 8.1 및 Windows&reg; 8 클라이언트에서 가장 가까운 사이트에 연결 하는 기능이 있습니다.  Windows 7&reg; 클라이언트 컴퓨터에는 동일한 기능이 없습니다. Windows 7 클라이언트에 대 한 사이트 선택은 정책 구성 시 특정 사이트로 설정 되며, 이러한 클라이언트는 위치에 관계 없이 항상 지정 된 사이트에 연결 됩니다.  
  
## <a name="bkmk_user"></a>사용자 기반 액세스 제어  
DirectAccess 정책은 사용자 기반이 아닌 컴퓨터 기반입니다. 회사 네트워크에 대 한 액세스를 제어 하는 DirectAccess 사용자 정책을 지정 하는 것은 지원 되지 않습니다.  
  
## <a name="bkmk_policy"></a>DirectAccess 정책 사용자 지정  
Directaccess는 DirectAccess 설치 마법사, 원격 액세스 관리 콘솔 또는 원격 액세스 Windows PowerShell cmdlet을 사용 하 여 구성할 수 있습니다. Directaccess 설치 마법사 이외의 수단을 사용 하 여 directaccess를 구성 하는 방법 (예: 서버 또는 클라이언트에서 직접 또는 기본 정책 설정을 수동으로 수정 하는 그룹 정책 것과 같은 directaccess)을 구성 하는 것은 지원 되지 않습니다. 이러한 수정으로 인해 구성을 사용할 수 없게 될 수 있습니다.  
  
## <a name="bkmk_kerb"></a>KerbProxy 인증  
시작 마법사를 사용 하 여 DirectAccess 서버를 구성 하면 컴퓨터 및 사용자 인증에 KerbProxy 인증을 사용 하도록 DirectAccess 서버가 자동으로 구성 됩니다. 따라서 Windows 10&reg;, Windows 8.1 또는 Windows 8 클라이언트만 배포 되는 단일 사이트 배포에 대해서만 시작 마법사를 사용 해야 합니다.  
  
또한 KerbProxy 인증과 함께 다음 기능을 사용 하면 안 됩니다.  
  
-   외부 부하 분산 장치 또는 Windows 로드를 사용 하 여 부하 분산   
    기가  
  
-   스마트 카드나 OTP (일회용 암호)가 필요한 2 단계 인증  
  
KerbProxy 인증을 사용 하는 경우 다음 배포 계획은 지원 되지 않습니다.  
  
-   Multisite.  
  
-   Windows 7 클라이언트에 대 한 DirectAccess 지원.  
  
-   강제 터널링. 강제 터널링을 사용할 때 KerbProxy 인증을 사용 하지 않도록 설정 하려면 마법사를 실행 하는 동안 다음 항목을 구성 합니다.  
  
    -   강제 터널링 사용  
  
    -   Windows 7 클라이언트에 DirectAccess 사용  
  
> [!NOTE]  
> 이전 배포의 경우 인증서 기반 컴퓨터 및 사용자 인증에 2-터널 구성을 사용 하는 고급 구성 마법사를 사용 해야 합니다. 자세한 내용은 [고급 설정을 사용 하 여 단일 DirectAccess 서버 배포](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)를 참조 하세요.  
  
## <a name="bkmk_isa"></a>ISATAP 사용  
ISATAP는 IPv4 전용 회사 네트워크에서 IPv6 연결을 제공 하는 전환 기술입니다. 단일 DirectAccess 서버를 배포 하는 중소 규모의 조직으로 제한 되며 DirectAccess 클라이언트의 원격 관리를 허용 합니다. 멀티 사이트, 부하 분산 또는 다중 도메인 환경에서 ISATAP를 배포 하는 경우 DirectAccess를 구성 하기 전에이를 제거 하거나 네이티브 IPv6 배포로 이동 해야 합니다.  
  
## <a name="bkmk_iphttps"></a>IPHTTPS 및 OTP (일회용 암호) 끝점 구성  
IPHTTPS를 사용 하는 경우에는 부하 분산 장치와 같은 다른 장치가 아닌 DirectAccess 서버에서 IPHTTPS 연결을 종료 해야 합니다. 마찬가지로 OTP (일회용 암호) 인증 중에 생성 되는 대역 외 SSL(Secure Sockets Layer) (SSL) 연결은 DirectAccess 서버에서 종료 해야 합니다. 이러한 연결의 끝점 사이에 있는 모든 장치는 통과 모드에서 구성 해야 합니다.  
  
## <a name="bkmk_ft"></a>OTP 인증을 사용 하 여 터널 강제 적용  
OTP 및 강제 터널링을 사용 하 여 2 단계 인증을 사용 하는 DirectAccess 서버를 배포 하지 마십시오. 그렇지 않으면 OTP 인증에 실패 합니다. DirectAccess 서버와 DirectAccess 클라이언트 간에는 대역 외 SSL(Secure Sockets Layer) (SSL) 연결이 필요 합니다. 이 연결에는 DirectAccess 터널 외부에서 트래픽을 전송 하기 위한 예외가 필요 합니다. 강제 터널 구성에서는 모든 트래픽이 DirectAccess 터널을 통해 전달 되어야 하며 터널이 설정 된 후에는 예외가 허용 되지 않습니다. 따라서 강제 터널 구성에서는 OTP 인증을 사용할 수 없습니다.  
  
## <a name="bkmk_rodc"></a>읽기 전용 도메인 컨트롤러를 사용 하 여 DirectAccess 배포  
DirectAccess 서버는 읽기/쓰기 도메인 컨트롤러에 대 한 액세스 권한이 있어야 하며 RODC (읽기 전용 도메인 컨트롤러)에서 제대로 작동 하지 않습니다.  
  
읽기/쓰기 도메인 컨트롤러는 다음을 비롯 한 다양 한 이유로 필요 합니다.  
  
-   DirectAccess 서버에서 원격 액세스 MMC (Microsoft Management Console)를 열려면 읽기-쓰기 도메인 컨트롤러가 필요 합니다.  
  
-   Directaccess 서버는 directaccess 클라이언트와 DirectAccess 서버 그룹 정책 개체 (Gpo)를 읽고 써야 합니다.  
  
-   DirectAccess 서버는 주 PDCe (도메인 컨트롤러 에뮬레이터)에서 특별히 클라이언트 GPO를 읽고 씁니다.  
  
이러한 요구 사항으로 인해 RODC를 사용 하 여 DirectAccess를 배포 하지 마십시오.  
  


