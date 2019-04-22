---
title: OTP 인증을 통한 원격 액세스 배포
description: 이 항목은 Windows Server 2016에서 OTP 인증을 사용 하 여 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b1b2fe70-7956-46e8-a3e3-43848868df09
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ecb4503c6f8cbc08f2175a33a41929491e4a2b7f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59811994"
---
# <a name="deploy-remote-access-with-otp-authentication"></a>OTP 인증을 통한 원격 액세스 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2016

 Windows Server 2016 및 Windows Server 2012 DirectAccess 및 라우팅 및 원격 액세스 서비스를 결합 \(RRAS\) VPN 단일 원격 액세스 역할을 합니다.   

## <a name="BKMK_OVER"></a>시나리오 설명  
이 시나리오는 원격 액세스에서 directaccess를 사용 하는 서버 두 개를 사용 하 여 DirectAccess 클라이언트 사용자를 인증 하도록 구성 된\-일회용 암호 비율 \(OTP\) 표준 활성 외에도 인증 디렉터리 자격 증명입니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
이 시나리오의 배포를 시작하기 전에 다음 목록에서 중요한 요구 사항을 검토하세요.  
  
-   [고급 설정을 사용 하 여 단일 DirectAccess 서버 배포](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md) OTP를 배포 하기 전에 배포 해야 합니다.  
  
-   Windows 7 클라이언트 DCA 2.0를 사용 하 여 OTP를 지원 하도록 해야 합니다.  
  
-   OTP는 PIN 변경을 지원하지 않습니다.  
  
-   공개 키 인프라를 배포해야 합니다.  
  
    자세한 내용은 다음을 참조하세요. [테스트 랩 가이드 미니 모듈: 에 Windows Server 2012에 대 한 기본 PKI](https://social.technet.microsoft.com/wiki/contents/articles/7862.test-lab-guide-mini-module-basic-pki-for-windows-server-2012.aspx)  
  
-   DirectAccess 관리 콘솔 또는 Windows PowerShell cmdlet 외부에서 정책을 변경 하는 것은 지원 되지 않습니다.  
  
## <a name="in-this-scenario"></a>이 시나리오의 내용  
OTP 인증 시나리오는 다음과 같은 단계로 구성됩니다.  
  
1.  [고급 설정 사용 하 여 단일 DirectAccess 서버 배포](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)합니다. OTP를 구성 하기 전에 단일 원격 액세스 서버 배포 되어야 합니다. 단일 서버 계획 및 배포 디자인과 계획 및 인증서를 배포, DNS와 Active Directory 설정, 원격 액세스 서버 설정, DirectAccess 클라이언트 배포 및 준비를 구성, 네트워크 토폴로지를 구성 포함 인트라넷 서버입니다.  
  
2.  [OTP 인증을 사용 하 여 원격 액세스 계획](https://docs.microsoft.com/windows-server/remote/remote-access/ras/otp/plan/plan-remote-access-with-otp-authentication)합니다. 단일 서버에 필요한 계획을 하는 것 외에도 OTP Microsoft 인증 기관에 대 한 계획이 필요 \(CA\) OTP;와 반지름에 대 한 인증서 템플릿 및\-OTP 서버를 사용 하도록 설정 합니다. 계획에서 특정 사용자를 강력한 제외 하려면 보안 그룹에 대 한 요구 사항이 포함 될 수 있습니다 \(OTP 또는 스마트 카드\) 인증 합니다. 다중에서 OTP 구성에 대 한 정보에 대 한\-환경에 포리스트를 참조 하십시오 [다중 포리스트 배포 구성](../../ras/multi-forest/Configure-a-Multi-Forest-Deployment.md)합니다.  
  
3.  [OTP 인증을 사용 하 여 DirectAccess 구성](/configure/Configure-RA-with-OTP-Authentication.md)합니다. OTP 배포 다양 한 구성 단계, OTP 인증을 OTP 서버를 구성, 원격 액세스 서버의 OTP 설정을 구성 및 DirectAccess 클라이언트 설정 업데이트에 대 한 인프라 준비를 포함 하 여 구성 됩니다.  
  
4.  [Troubleshoot an OTP Deployment] ((/troubleshoot/Troubleshoot-an-OTP-Deployment.md)입니다. 이 문제 해결 섹션에는 많은 OTP 인증을 사용 하 여 원격 액세스를 배포할 때 발생할 수 있는 가장 일반적인 오류를 설명 합니다.  
  
## <a name="BKMK_APP"></a>실제 응용 프로그램  
DirectAccess 배포의 보안을 강화 하는 OTP를 사용 하 여 보안 하는 증가 합니다. 사용자가 내부 네트워크에 대한 액세스 권한을 얻으려면 OTP 자격 증명이 있어야 합니다. Windows 10 또는 Windows 8 클라이언트 컴퓨터 또는 DirectAccess 연결 길잡이 사용 하 여 네트워크 연결에서 사용할 수 있는 작업 공간 연결을 통해 OTP 자격 증명을 제공 하는 사용자 \(DCA\) 실행 클라이언트 컴퓨터 Windows 7입니다. OTP 인증 프로세스는 다음과 같습니다.  
  
1.  DirectAccess 인프라 서버에 액세스할 도메인 자격 증명을 입력 하는 DirectAccess 클라이언트 \(인프라 터널을 통해\)합니다.  특정 IKE 오류로 인해 내부 네트워크에 대한 연결을 사용할 수 없는 경우, 클라이언트 컴퓨터의 작업 공간 연결에서 자격 증명이 필요함을 사용자에게 알립니다. 클라이언트 컴퓨터에서 Windows 7을 pop 실행\-를 표시 하는 스마트 카드 자격 증명을 요청 합니다.  
  
2.  입력 된 OTP 자격 증명은 원격 액세스 서버로 짧은 요청과 함께 SSL을 통해 전송 됩니다\-용어 스마트 카드 로그온 인증서입니다.  
  
3.  원격 액세스 서버는 RADIUS 사용 하 여 OTP 자격 증명의 유효성 검사를 시작\-기반 OTP 서버.  
  
4.  성공하면 원격 액세스 서버가 해당 등록 기관 인증서를 사용하여 인증서 요청에 서명하고 다시 DirectAccess 클라이언트 컴퓨터로 보냅니다.  
  
5.  DirectAccess 클라이언트 컴퓨터 ca 서명 된 인증서 요청을 전달 하 고 Kerberos SSP에서 사용 하기 위해 등록된 된 인증서를 저장\/AP 합니다.  
  
6.  클라이언트 컴퓨터는 이 인증서를 사용하여 표준 스마트 카드 Kerberos 인증을 투명하게 수행합니다.  
  
## <a name="BKMK_NEW"></a>역할과이 시나리오에 포함 된 기능  
다음 표에는 시나리오에 필요한 역할 및 기능이 나와 있습니다.  
  
|역할\/기능|이 시나리오를 지원하는 방법|  
|---------|-----------------|  
|*원격 액세스 관리 역할*|이 역할은 서버 관리자 콘솔을 사용하여 설치 및 제거됩니다. 이 역할에는 모두 DirectAccess는 Windows Server 2008 R2 및 라우팅 및 원격 액세스 서비스 역할 서비스는 네트워크 정책 및 액세스 서비스의 기능 였습니다 \(NPAS\) 서버 역할입니다. 원격 액세스 역할은 다음의 두 가지 구성 요소로 구성됩니다.<br /><br />1.  DirectAccess 및 라우팅 및 원격 액세스 서비스 \(RRAS\) VPN-DirectAccess 및 VPN 원격 액세스 관리 콘솔에서 함께 관리 됩니다.<br />2.  RRAS 라우팅 RRAS 라우팅 기능은 레거시 라우팅 및 원격 액세스 콘솔에서 관리 됩니다.<br /><br />원격 액세스 역할은 다음과 같이 서버 기능에 종속됩니다.<br /><br />인터넷 정보 서비스 \(IIS\) 웹 서버-이 기능은 네트워크 위치 서버 구성, OTP 인증을 활용 하 고 기본 웹 프로브를 구성 해야 합니다.<br />Windows 로컬 계정에 원격 액세스 서버에 대 한 내부 Database-Used 합니다.|  
|원격 액세스 관리 도구 기능|이 기능은 다음과 같이 설치 됩니다.<br /><br />-이 값은 원격 액세스 역할이 설치 되어 있고 원격 관리 콘솔 사용자 인터페이스를 지 원하는 때 기본적으로 원격 액세스 서버에 설치 됩니다.<br />-앱는 하지 원격 액세스 서버 역할을 실행 하는 서버에 필요에 따라 설치 수 있습니다. 이 경우 이 기능은 DirectAccess 및 VPN을 실행하는 원격 액세스 컴퓨터를 원격으로 관리하는 데 사용됩니다.<br /><br />원격 액세스 관리 도구 기능의 구성 요소는 다음과 같습니다.<br /><br />-원격 액세스 GUI 및 명령줄 도구<br />-Windows PowerShell 용 원격 액세스 모듈<br /><br />이 기능은 다음 요소에 종속됩니다.<br /><br />그룹 정책 관리 콘솔<br />RAS 연결 관리자 관리 키트 \(CMAK\)<br />Windows PowerShell 3.0<br />-그래픽 관리 도구 및 인프라|  
  
## <a name="BKMK_HARD"></a>하드웨어 요구 사항  
이 시나리오의 하드웨어 요구 사항은 다음과 같습니다.  
  
-   Windows Server 2016 또는 Windows Server 2012에 대 한 하드웨어 요구 사항을 충족 하는 컴퓨터.  
  
-   시나리오를 테스트 하기 위해 하나 이상의 Windows 10, Windows 8 또는 Windows 7 DirectAccess 클라이언트로 구성 된 실행 컴퓨터가 필요 합니다.  
  
-   RADIUS를 통해 PAP를 지원하는 OTP 서버가 하나 필요합니다.  
  
-   OTP 하드웨어 또는 소프트웨어 토큰이 필요합니다.  
  
## <a name="BKMK_SOFT"></a>소프트웨어 요구 사항  
이 시나리오에 필요한 요구 사항은 다음과 같이 다양합니다.  
  
1.  단일 서버 배포에 필요한 소프트웨어 요구 사항. 자세한 내용은 [고급 설정을 사용 하 여 단일 DirectAccess 서버 배포](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)합니다.  
  
2.  단일 서버에 대 한 소프트웨어 요구 사항 외에 여러 가지 OTP\-특정 요구 사항:  
  
    1.  CA에서 인증에 대 한 IPsec을 사용 하 여 DirectAccess를 배포 해야 하는 OTP 배포 컴퓨터 CA에서 발급 한 인증서입니다. 원격 액세스 서버를 Kerberos 프록시로 사용하는 IPsec 인증은 OTP 배포에서 지원되지 않습니다. 내부 CA가 필요합니다.  
  
    2.  OTP 인증-Microsoft 엔터프라이즈 CA에 대 한 CA \(Windows Server 2003 이상을 실행 하 고\) OTP 클라이언트 인증서를 발급 해야 합니다. IPsec 인증을 위한 인증서 발급에 사용된 것과 같은 CA를 사용할 수도 있습니다. 첫 번째 인프라 터널을 통해 CA 서버를 사용할 수 있어야 합니다.  
  
    3.  보안 그룹을 제외 사용자 강력한 인증에서 이러한 사용자를 포함 하는 Active Directory 보안 그룹이 필요 합니다.  
  
    4.  클라이언트\-요구 사항-에 대 한 Windows 10 및 Windows 8 클라이언트 컴퓨터, 네트워크 연결 길잡이 \(NCA\) OTP 자격 증명이 필요한 지 여부를 검색할 서비스를 사용 합니다. 이러한 경우 DirectAccess 미디어 관리자 자격 증명을 묻습니다.  NCA는 운영 체제에 포함 하 고 설치 또는 배포 필요 하지 않습니다. Windows 7 클라이언트 컴퓨터, DirectAccess 연결 길잡이 \(DCA\) 는 2.0이 필요 합니다. 이 응용 프로그램은 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=29039)에서 다운로드할 수 있습니다.  
  
    5.  다음에 유의하세요.  
  
        1.  OTP 인증은 스마트 카드와 신뢰할 수 있는 플랫폼 모듈을 사용 하 여 동시에 사용할 수 있습니다 \(TPM\)\-기반 인증 합니다. 원격 액세스 관리 콘솔에서 OTP 인증을 사용하도록 설정하면 스마트 카드 인증도 사용할 수 있습니다.  
  
        2.  원격 액세스를 구성할 때 사용자 지정 된 보안에서 그룹에서 두 제외 될 수 있습니다\-단계 인증을 하 고 username을 사용 하 여 인증할\/암호만 합니다.  
  
        3.  OTP의 새 PIN 및 다음 토큰 코드 모드는 지원되지 않습니다.  
  
        4.  원격 액세스 멀티 사이트 배포 시, OTP 설정은 전역적이며 모든 진입점을 식별합니다. OTP용으로 구성된 RADIUS 또는 CA 서버가 여러 대인 경우 가용성 및 근접성에 따라 원격 액세스 서버별로 정렬됩니다.  
  
        5.  원격 액세스 다중에서 OTP를 구성 하는 경우\-포리스트 환경의 OTP Ca만 리소스 포리스트에서 있어야 하며 포리스트 트러스트 간에 인증서 등록이 구성 되어야 합니다. 자세한 내용은 참조 하세요. [AD CS: Windows Server 2008 R2로 포리스트 간 인증서 등록](https://technet.microsoft.com/library/ff955842.aspx)합니다.  
  
        6.  KEY FOB OTP 토큰을 사용 하는 사용자 토큰 뒤에 PIN을 삽입할지 \(구분 기호 없이\) DirectAccess OTP 대화 상자에서. PIN PAD OTP 토큰 사용자는 대화 상자에 토큰 코드만 삽입해야 합니다.  
  
        7.  WEBDAV를 사용하는 경우 OTP를 사용하도록 설정할 수 없습니다.  
  
## <a name="KnownIssues"></a>알려진된 문제  
OTP 시나리오를 구성할 때의 알려진 문제는 다음과 같습니다.  
  
-   원격 액세스는 프로브 메커니즘을 사용 하 여 RADIUS에 대 한 연결을 확인 하려면\-기반 OTP 서버. 이로 인해 OTP 서버에서 오류가 발생하는 경우가 있습니다. 이 문제를 방지하려면 OTP 서버에서 다음을 수행합니다.  
  
    -   프로브 메커니즘에 대한 원격 액세스 서버에서 구성된 사용자 이름 및 암호와 일치하는 사용자 계정을 만듭니다. 사용자 이름이 Active Directory 사용자를 정의하면 안 됩니다.  
  
        기본적으로 원격 액세스 서버의 사용자 이름은 DAProbeUser이고 암호는 DAProbePass입니다. 원격 액세스 서버의 레지스트리에서 다음 값을 사용하여 이러한 기본 설정을 수정할 수 있습니다.  
  
        -   HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\DirectAccess\\OTP\\RadiusProbeUser  
  
        -   HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\DirectAccess\\OTP\\ RadiusProbePass  
  
-   구성되어 실행 중인 DirectAccess 배포에서 IPsec 루트 인증서를 변경하면 OTP 작동이 중지됩니다. 각 DirectAccess 서버의 Windows PowerShell 프롬프트에서이 문제를 해결 하려면 명령을 실행 합니다. `iisreset`  
  
