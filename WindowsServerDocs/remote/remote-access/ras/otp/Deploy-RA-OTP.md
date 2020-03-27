---
title: OTP 인증을 통한 원격 액세스 배포
description: 이 항목은 Windows Server 2016에서 OTP 인증을 사용 하 여 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b1b2fe70-7956-46e8-a3e3-43848868df09
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 5b86cbe970c60f0684f3f6e5198fa91bbb9745b1
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80313681"
---
# <a name="deploy-remote-access-with-otp-authentication"></a>OTP 인증을 통한 원격 액세스 배포

>적용 대상: Windows Server(반기 채널), Windows Server 2016

 Windows Server 2016 및 Windows Server 2012에서는 DirectAccess와 라우팅 및 원격 액세스 서비스 \(RRAS\) VPN을 단일 원격 액세스 역할로 결합 합니다.   

## <a name="scenario-description"></a><a name="BKMK_OVER"></a>시나리오 설명  
이 시나리오에서 DirectAccess를 사용 하는 원격 액세스 서버는 표준 Active Directory 자격 증명 외에도 두 개의\-요소 \(OTP\) 인증을 사용 하 여 DirectAccess 클라이언트 사용자를 인증 하도록 구성 됩니다.  
  
## <a name="prerequisites"></a>필수 조건  
이 시나리오의 배포를 시작하기 전에 다음 목록에서 중요한 요구 사항을 검토하세요.  
  
-   OTP를 배포 하기 전에 [고급 설정을 사용 하 여 단일 DirectAccess 서버 배포](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md) 를 배포 해야 합니다.  
  
-   Windows 7 클라이언트는 DCA 2.0를 사용 하 여 OTP를 지원 해야 합니다.  
  
-   OTP는 PIN 변경을 지원하지 않습니다.  
  
-   공개 키 인프라를 배포해야 합니다.  
  
    자세한 내용은 다음을 참조하십시오. [테스트 랩 가이드 미니 모듈: Windows Server 2012에 대한 기본 PKI](https://social.technet.microsoft.com/wiki/contents/articles/7862.test-lab-guide-mini-module-basic-pki-for-windows-server-2012.aspx)  
  
-   DirectAccess 관리 콘솔 또는 Windows PowerShell cmdlet 외부에서 정책을 변경 하는 것은 지원 되지 않습니다.  
  
## <a name="in-this-scenario"></a>이 시나리오의 내용  
OTP 인증 시나리오는 다음과 같은 단계로 구성됩니다.  
  
1.  [고급 설정을 사용 하 여 단일 DirectAccess 서버를 배포](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)합니다. OTP를 구성 하기 전에 단일 원격 액세스 서버를 배포 해야 합니다. 단일 서버를 계획하고 배포하는 과정에는 네트워크 토폴로지 설계 및 구성, 인증서 계획 및 배포, DNS와 Active Directory 설정, 원격 액세스 서버 설정 구성, DirectAccess 클라이언트 배포 및 인트라넷 서버 준비가 포함됩니다.  
  
2.  [OTP 인증을 사용 하 여 원격 액세스를 계획](https://docs.microsoft.com/windows-server/remote/remote-access/ras/otp/plan/plan-remote-access-with-otp-authentication)합니다. OTP는 단일 서버에 필요한 계획 외에도 Microsoft 인증 기관 \(CA\) 및 OTP 용 인증서 템플릿을 계획 해야 합니다. 그리고 RADIUS\-OTP 서버를 사용 하도록 설정 합니다. 계획에는 강력한 \(OTP 또는 스마트 카드\) 인증의 특정 사용자를 제외 하는 보안 그룹 요구 사항이 포함 될 수도 있습니다. 다중\-포리스트 환경에서 OTP를 구성 하는 방법에 대 한 자세한 내용은 [다중 포리스트 배포 구성](../../ras/multi-forest/Configure-a-Multi-Forest-Deployment.md)을 참조 하세요.  
  
3.  [OTP 인증을 사용 하 여 DirectAccess를 구성](/configure/Configure-RA-with-OTP-Authentication.md)합니다. Otp 배포는 OTP 인증을 위한 인프라 준비, OTP 서버 구성, 원격 액세스 서버에서 OTP 설정 구성 및 DirectAccess 클라이언트 설정 업데이트를 포함 하 여 다양 한 구성 단계로 구성 됩니다.  
  
4.  [OTP 배포 문제 해결] ((/troubleshoot/Troubleshoot-an-OTP-Deployment.md). 이 문제 해결 섹션에서는 OTP 인증을 사용 하 여 원격 액세스를 배포할 때 발생할 수 있는 가장 일반적인 몇 가지 오류에 대해 설명 합니다.  
  
## <a name="practical-applications"></a><a name="BKMK_APP"></a>실용적인 응용 프로그램  
보안 강화-OTP를 사용 하면 DirectAccess 배포의 보안이 강화 됩니다. 사용자가 내부 네트워크에 대한 액세스 권한을 얻으려면 OTP 자격 증명이 있어야 합니다. 사용자는 Windows 10 또는 Windows 8 클라이언트 컴퓨터의 네트워크 연결에서 사용할 수 있는 작업 공간 연결을 통해 또는 Windows 7을 실행 하는 클라이언트 컴퓨터에서\) \(DCA 연결 길잡이를 사용 하 여 OTP 자격 증명을 제공 합니다. OTP 인증 프로세스는 다음과 같습니다.  
  
1.  DirectAccess 클라이언트는 인프라 터널\)를 통해 \(DirectAccess 인프라 서버에 액세스 하기 위해 도메인 자격 증명을 입력 합니다.  특정 IKE 오류로 인해 내부 네트워크에 대한 연결을 사용할 수 없는 경우, 클라이언트 컴퓨터의 작업 공간 연결에서 자격 증명이 필요함을 사용자에게 알립니다. Windows 7을 실행 하는 클라이언트 컴퓨터에서는 스마트 카드 자격 증명을 요청 하는 pop\-표시 됩니다.  
  
2.  OTP 자격 증명을 입력 한 후에는 SSL을 통해 원격 액세스 서버로 전송 되며 단기\-용어 스마트 카드 로그온 인증서에 대 한 요청과 함께 전송 됩니다.  
  
3.  원격 액세스 서버는 RADIUS\-기반 OTP 서버를 사용 하 여 OTP 자격 증명의 유효성 검사를 시작 합니다.  
  
4.  성공하면 원격 액세스 서버가 해당 등록 기관 인증서를 사용하여 인증서 요청에 서명하고 다시 DirectAccess 클라이언트 컴퓨터로 보냅니다.  
  
5.  DirectAccess 클라이언트 컴퓨터는 서명 된 인증서 요청을 CA에 전달 하 고 Kerberos SSP\/AP에서 사용할 수 있도록 등록 된 인증서를 저장 합니다.  
  
6.  클라이언트 컴퓨터는 이 인증서를 사용하여 표준 스마트 카드 Kerberos 인증을 투명하게 수행합니다.  
  
## <a name="roles-and-features-included-in-this-scenario"></a><a name="BKMK_NEW"></a>이 시나리오에 포함 된 역할 및 기능  
다음 표에는 시나리오에 필요한 역할 및 기능이 나와 있습니다.  
  
|역할\/기능|이 시나리오를 지원하는 방법|  
|---------|-----------------|  
|*원격 액세스 관리 역할*|이 역할은 서버 관리자 콘솔을 사용하여 설치 및 제거됩니다. 이 역할은 이전에 Windows Server 2008 r 2의 기능 이었던 DirectAccess 및 라우팅 및 원격 액세스 서비스를 모두 포함 하며, 이전에는 네트워크 정책 및 액세스 서비스 \(NPAS\) 서버 역할의 역할 서비스입니다. 원격 액세스 역할은 다음의 두 가지 구성 요소로 구성됩니다.<br /><br />1. DirectAccess 및 라우팅 및 원격 액세스 서비스 \(RRAS\) VPN-DirectAccess와 VPN은 원격 액세스 관리 콘솔에서 함께 관리 됩니다.<br />2. RRAS 라우팅-RRAS 라우팅 기능은 레거시 라우팅 및 원격 액세스 콘솔에서 관리 됩니다.<br /><br />원격 액세스 역할은 다음과 같이 서버 기능에 종속됩니다.<br /><br />-인터넷 정보 서비스 \(IIS\) 웹 서버-네트워크 위치 서버를 구성 하 고, OTP 인증을 활용 하 고, 기본 웹 프로브를 구성 하는 데이 기능이 필요 합니다.<br />Windows 로컬 계정에 원격 액세스 서버에 대 한 내부 Database-Used 합니다.|  
|원격 액세스 관리 도구 기능|이 기능은 다음과 같이 설치됩니다.<br /><br />-이 값은 원격 액세스 역할이 설치 되어 있고 원격 관리 콘솔 사용자 인터페이스를 지 원하는 때 기본적으로 원격 액세스 서버에 설치 됩니다.<br />-앱는 하지 원격 액세스 서버 역할을 실행 하는 서버에 필요에 따라 설치 수 있습니다. 이 경우 이 기능은 DirectAccess 및 VPN을 실행하는 원격 액세스 컴퓨터를 원격으로 관리하는 데 사용됩니다.<br /><br />원격 액세스 관리 도구 기능의 구성 요소는 다음과 같습니다.<br /><br />-원격 액세스 GUI 및 명령줄 도구<br />-Windows PowerShell 용 원격 액세스 모듈<br /><br />이 기능은 다음 요소에 종속됩니다.<br /><br />그룹 정책 관리 콘솔<br />-RAS 연결 관리자 관리 키트 \(CMAK\)<br />Windows PowerShell 3.0<br />-그래픽 관리 도구 및 인프라|  
  
## <a name="hardware-requirements"></a><a name="BKMK_HARD"></a>하드웨어 요구 사항  
이 시나리오의 하드웨어 요구 사항은 다음과 같습니다.  
  
-   Windows Server 2016 또는 Windows Server 2012의 하드웨어 요구 사항을 충족 하는 컴퓨터입니다.  
  
-   시나리오를 테스트 하려면 DirectAccess 클라이언트로 구성 된 windows 10, Windows 8 또는 Windows 7을 실행 하는 컴퓨터가 하나 이상 필요 합니다.  
  
-   RADIUS를 통해 PAP를 지원하는 OTP 서버가 하나 필요합니다.  
  
-   OTP 하드웨어 또는 소프트웨어 토큰이 필요합니다.  
  
## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>소프트웨어 요구 사항  
이 시나리오에 필요한 요구 사항은 다음과 같이 다양합니다.  
  
1.  단일 서버 배포에 필요한 소프트웨어 요구 사항. 자세한 내용은 [고급 설정을 사용 하 여 단일 DirectAccess 서버 배포](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)를 참조 하세요.  
  
2.  단일 서버에 대 한 소프트웨어 요구 사항 외에도 몇 가지 OTP\-특정 요구 사항이 있습니다.  
  
    1.  IPsec 인증용 CA-OTP 배포 DirectAccess는 CA에서 발급 한 IPsec 컴퓨터 인증서를 사용 하 여 배포 해야 합니다. 원격 액세스 서버를 Kerberos 프록시로 사용하는 IPsec 인증은 OTP 배포에서 지원되지 않습니다. 내부 CA가 필요합니다.  
  
    2.  OTP 인증용 CA-OTP 클라이언트 인증서를 발급 하려면 Windows 2003 서버\) 이상에서 실행 되는 Microsoft 엔터프라이즈 CA \(필요 합니다. IPsec 인증을 위한 인증서 발급에 사용된 것과 같은 CA를 사용할 수도 있습니다. 첫 번째 인프라 터널을 통해 CA 서버를 사용할 수 있어야 합니다.  
  
    3.  보안 그룹-강력한 인증에서 사용자를 제외 하려면 이러한 사용자를 포함 하는 Active Directory 보안 그룹이 필요 합니다.  
  
    4.  클라이언트\-쪽 요구 사항-Windows 10 및 Windows 8 클라이언트 컴퓨터에 대 한 네트워크 연결 길잡이 \(NCA\) 서비스는 OTP 자격 증명이 필요한 지 여부를 검색 하는 데 사용 됩니다. 인증서가 있으면 DirectAccess 미디어 관리자가 자격 증명을 묻는 메시지를 표시 합니다.  NCA는 운영 체제에 포함 되어 있으며 설치 또는 배포가 필요 하지 않습니다. Windows 7 클라이언트 컴퓨터의 경우에는 DirectAccess 연결 길잡이 \(DCA\) 2.0가 필요 합니다. 이 응용 프로그램은 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=29039)에서 다운로드할 수 있습니다.  
  
    5.  유의 사항은 다음과 같습니다.  
  
        1.  OTP 인증은 스마트 카드 및 신뢰할 수 있는 플랫폼 모듈 \(TPM\)\-기반 인증을 사용 하 여 병렬로 사용할 수 있습니다. 원격 액세스 관리 콘솔에서 OTP 인증을 사용하도록 설정하면 스마트 카드 인증도 사용할 수 있습니다.  
  
        2.  원격 액세스를 구성 하는 동안 지정 된 보안 그룹의 사용자는 두 개의\-단계 인증에서 제외 될 수 있으므로 사용자 이름\/암호만 사용 하 여 인증 합니다.  
  
        3.  OTP의 새 PIN 및 다음 토큰 코드 모드는 지원되지 않습니다.  
  
        4.  원격 액세스 멀티 사이트 배포 시, OTP 설정은 전역적이며 모든 진입점을 식별합니다. OTP용으로 구성된 RADIUS 또는 CA 서버가 여러 대인 경우 가용성 및 근접성에 따라 원격 액세스 서버별로 정렬됩니다.  
  
        5.  원격 액세스 다중\-포리스트 환경에서 OTP를 구성 하는 경우 OTP Ca는 리소스 포리스트에만 있어야 하 고, 포리스트 트러스트 간에 인증서 등록을 구성 해야 합니다. 자세한 내용은 [AD CS: Windows Server 2008 R2로 포리스트 간 인증서 등록](https://technet.microsoft.com/library/ff955842.aspx)을 참조하십시오.  
  
        6.  키 FOB OTP 토큰을 사용 하는 사용자는\) DirectAccess OTP 대화 상자에서 구분 기호를 사용 하지 않고 \(토큰을 삽입 해야 합니다. PIN PAD OTP 토큰 사용자는 대화 상자에 토큰 코드만 삽입해야 합니다.  
  
        7.  WEBDAV를 사용하는 경우 OTP를 사용하도록 설정할 수 없습니다.  
  
## <a name="known-issues"></a><a name="KnownIssues"></a>알려진 문제  
OTP 시나리오를 구성할 때의 알려진 문제는 다음과 같습니다.  
  
-   원격 액세스는 프로브 메커니즘을 사용 하 여 RADIUS\-기반 OTP 서버에 대 한 연결을 확인 합니다. 이로 인해 OTP 서버에서 오류가 발생하는 경우가 있습니다. 이 문제를 방지하려면 OTP 서버에서 다음을 수행합니다.  
  
    -   프로브 메커니즘에 대한 원격 액세스 서버에서 구성된 사용자 이름 및 암호와 일치하는 사용자 계정을 만듭니다. 사용자 이름이 Active Directory 사용자를 정의하면 안 됩니다.  
  
        기본적으로 원격 액세스 서버의 사용자 이름은 DAProbeUser이고 암호는 DAProbePass입니다. 원격 액세스 서버의 레지스트리에서 다음 값을 사용하여 이러한 기본 설정을 수정할 수 있습니다.  
  
        -   HKEY\_로컬\_MACHINE\\소프트웨어\\Microsoft\\DirectAccess\\OTP\\RadiusProbeUser  
  
        -   HKEY\_로컬\_MACHINE\\소프트웨어\\Microsoft\\DirectAccess\\OTP\\ RadiusProbePass  
  
-   구성되어 실행 중인 DirectAccess 배포에서 IPsec 루트 인증서를 변경하면 OTP 작동이 중지됩니다. 이 문제를 해결 하려면 각 DirectAccess 서버의 Windows PowerShell 프롬프트에서 다음 명령을 실행 합니다. `iisreset`  
  
