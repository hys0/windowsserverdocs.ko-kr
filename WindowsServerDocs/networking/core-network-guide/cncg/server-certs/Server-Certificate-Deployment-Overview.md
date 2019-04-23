---
title: 서버 인증서 배포 개요
description: 이 항목은 서버 배포 인증서 802.1 X 유선 및 무선 배포 가이드의 일부
manager: brianlic
ms.topic: article
ms.assetid: ca5c3e04-ae25-4590-97f3-0376a9c2a9a2
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0cafa4bdeb80b22d6bac4ad09bcae9436cda97c8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877824"
---
# <a name="server-certificate-deployment-overview"></a>서버 인증서 배포 개요

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에는 다음 섹션이 수록되어 있습니다.  
  
-   [서버 인증서 배포 구성 요소](#bkmk_components)
  
-   [서버 인증서 배포 프로세스 개요](#bkmk_process)
  
## <a name="bkmk_components"></a>서버 인증서 배포 구성 요소
이 가이드를 사용 하 여 엔터프라이즈 루트 인증 기관 (CA)으로 Active Directory 인증서 서비스 (AD CS)를 설치 하 고 네트워크 정책 (NPS 서버), 라우팅 및 원격 액세스 서비스 (RRAS) 또는 둘 다 NPS 및 RRAS를 실행 하는 서버에 서버 인증서를 등록할 수 있습니다.


인증서 기반 인증 SDN을 배포 하는 경우 보안 통신을 달성할 수 있도록 다른 서버에 자신의 id를 증명 하는 서버 인증서를 사용 하 여 서버가 필요 합니다.
  
다음 그림에서는 SDN 인프라 서버에 서버 인증서를 배포 하는 데 필요한 구성 요소를 보여 줍니다.
  
![서버 인증서 배포 필수 인프라](../../../media/Nps-Certs/Nps-Certs.jpg)  
  
> [!NOTE]  
> 위의 그림에서는 여러 서버 표시 됩니다. DC1, c a 1, WEB1 및 많은 SDN 서버입니다. 이 가이드는 c a 1와 w e b 1을 배포 및 구성에 대 한 고 d c 1에서이 가이드에서는 네트워크에 이미 설치한 가정 구성 하기 위한 지침을 제공 합니다. Active Directory 도메인을 아직 설치 하지 않은 경우 해도 사용 하 여는 [핵심 네트워크 가이드](https://technet.microsoft.com/library/mt604042.aspx) Windows Server 2016 용입니다.  
  
위의 그림에 나와 있는 각 항목에 대 한 자세한 내용은 다음을 참조 합니다.  
  
-   [CA1](#bkmk_ca1)  
  
-   [WEB1](#bkmk_web1)  
  
-   [DC1](#bkmk_dc1)  
  
-   [NPS1](#bkmk_nps1)  
  
### <a name="bkmk_ca1"></a>CA1 AD CS 서버 역할을 실행  
이 시나리오에서는 엔터프라이즈 루트 인증 기관 (CA) 이기도 CA를 발급 합니다. CA는 인증서를 등록 하는 올바른 보안 권한이 있는 서버 컴퓨터에 인증서를 발급 합니다. Active Directory 인증서 서비스 (AD CS)는 c a 1에 설치 됩니다.  
  
대규모 네트워크 또는 보안 문제 사유를 제공 하는 위치에 대 한 루트 CA 및 발급 CA의 역할을 구분 하 고 발급 Ca는 하위 Ca를 배포할 수 있습니다.  
  
가장 안전한 배포에서 엔터프라이즈 루트 CA는 오프 라인으로 물리적으로 수행 됩니다.   
  
#### <a name="capolicyinf"></a>CAPolicy.inf  
AD CS를 설치 하기 전에 구성한 CAPolicy.inf 파일 특정 설정을 사용 하 여 배포 합니다.  
  
#### <a name="copy-of-the-ras-and-ias-servers-certificate-template"></a>복사본은 **RAS 및 IAS 서버** 인증서 템플릿  
복사본을 하나를 만들 때 서버 인증서를 배포 하면는 **RAS 및 IAS 서버** 인증서 템플릿을 선택한 다음이 가이드에서 요구 사항 및 지침에 따라 서식 파일을 구성 합니다.   
  
원본 템플릿의 구성 나중에 사용 하기 위해 유지 됩니다 있도록 원본 서식 파일 보다는 서식 파일의 복사본을 활용 합니다. 복사본을 구성는 **RAS 및 IAS 서버** 템플릿을 Active Directory 사용자 및 사용자가 지정한 컴퓨터의 그룹에 발급 CA를 만들 수 있는 서버 인증서입니다.  
  
#### <a name="additional-ca1-configuration"></a>추가 c a 1 구성  
CA는 컴퓨터 id 증명으로에 표시 되는 인증서에 유효한 인증서를 확인 하 고 해지 여부를 확인 해야 하는 인증서 해지 목록 (CRL)를 게시 합니다. 컴퓨터를 인증 프로세스 중에 CRL을 찾을 위치를 알 수 있도록 CRL의 올바른 위치와 CA를 구성 해야 합니다.  
  
### <a name="bkmk_web1"></a>W e b 1 웹 서비스 (IIS) 서버 역할을 실행  
W e b 1을 웹 서버 (IIS) 서버 역할을 실행 하는 컴퓨터에서 만들어야 폴더 Windows 탐색기에서 CRL 및 AIA 위치로 사용 하기 위해.  
  
#### <a name="virtual-directory-for-the-crl-and-aia"></a>CRL 및 AIA에 대 한 가상 디렉터리  
Windows 탐색기에서 폴더를 만든 후에 인터넷 정보 서비스 (IIS) 관리자와 같은 가상 디렉터리에 대 한 액세스 제어 목록 구성 컴퓨터 허용할 있습니다 게시 후 AIA 및 CRL에 액세스 하는 가상 디렉터리와 폴더를 구성 해야 합니다.  
  
### <a name="bkmk_dc1"></a>D c 1 AD DS 및 DNS 서버 역할을 실행  
D c 1에는 도메인 컨트롤러와 네트워크에 DNS 서버입니다.  
  
#### <a name="group-policy-default-domain-policy"></a>그룹 정책 기본 도메인 정책  
CA에서 인증서 템플릿을 구성한 후 인증서에 NPS 및 RAS 서버에 대 한 자동 등록 되도록 기본 도메인 정책 그룹 정책에서 구성할 수 있습니다. 그룹 정책 서버 d c 1에 AD DS에서 구성 됩니다.  
  
#### <a name="dns-alias-cname-resource-record"></a>DNS 별칭 (CNAME) 리소스 레코드입니다.  
다른 컴퓨터는 서버 뿐만 아니라 AIA 및 서버에 저장 된 CRL을 찾을 수 있도록 웹 서버에 대 한 별칭 (CNAME) 리소스 레코드를 만들어야 합니다. 또한 별칭 CNAME 리소스 레코드를 사용 하 여 웹 및 FTP 사이트를 호스트 하는 것과 같은 다른 용도 대 한 웹 서버를 사용할 수 있도록 유연성이 제공 됩니다.  
  
### <a name="bkmk_nps1"></a>NPS1 네트워크 정책 및 액세스 서비스 서버 역할의 네트워크 정책 서버 역할 서비스를 실행 합니다.  
Windows Server 2016 핵심 네트워크 가이드의 작업을 수행 하는 경우 NPS 설치 된, 하나 이상의 NPSs 네트워크에 설치 되어 있어야이 가이드의 작업을 수행 하기 전에 있도록 합니다.  
  
#### <a name="group-policy-applied-and-certificate-enrolled-to-servers"></a>그룹 정책을 적용 하 고 서버에 등록 된 인증서  
인증서 템플릿 및 자동 등록을 구성 하 고 나면 모든 대상 서버에서 그룹 정책을 새로 고칠 수 있습니다. 이 이번에는 서버 c a 1에서 서버 인증서를 등록합니다.  
  
### <a name="bkmk_process"></a>서버 인증서 배포 프로세스 개요  
  
> [!NOTE]  
> 이러한 단계를 수행 하는 방법에 대 한 세부 정보 섹션에 제공 됩니다 [서버 인증서 배포](../../../core-network-guide/cncg/server-certs/Server-Certificate-Deployment.md)합니다.  
  
서버 인증서 등록을 구성 하는 프로세스이 단계에서 발생 합니다.  
  
1.  W e b 1을 웹 서버 (IIS) 역할을 설치 합니다.  
  
2.  D c 1의 웹 서버에서 w e b 1에 대 한 별칭 (CNAME) 레코드를 만듭니다.  
  
3.  CA에서 CRL을 호스팅하고 CRL을 게시 한 후 엔터프라이즈 루트 CA 인증서를 새 가상 디렉터리에 복사 하도록 웹 서버를 구성 합니다.  
  
4.  AD CS를 설치 하려는 컴퓨터에서 컴퓨터에 고정 IP 주소를 할당, 컴퓨터 이름을 바꾸고, 컴퓨터를 도메인에 가입 및 다음 Domain Admins 및 Enterprise Admins 그룹의 구성원 인 사용자 계정으로 컴퓨터에 로그온 합니다.  
  
5.  AD CS를 설치 하려는 컴퓨터에서 배포에 관련 된 설정을 사용 하 여 CAPolicy.inf 파일을 구성 합니다.  
  
6.  AD CS 서버 역할을 설치 하 고 CA의 추가 구성을 수행 합니다.  
  
7.  공유 웹 서버 w e b 1에 c a 1에서 CRL 및 CA 인증서를 복사 합니다.  
  
8.  CA에서 RAS 및 IAS 서버 인증서 템플릿의 복사본을 구성 합니다. CA는 인증서 템플릿을 기반으로 하므로 CA 인증서를 발급 하기 전에 서버 인증서에 대 한 서식 파일을 구성 해야 하는 인증서를 발급 합니다.  
  
9.  그룹 정책에서 서버 인증서 자동 등록을 구성 합니다. 자동 등록을 구성 하는 경우 각 서버에 그룹 정책이 새로 고쳐질 때 자동으로 Active Directory 그룹 멤버와 지정 된 모든 서버에 서버 인증서를 받습니다. 나중에 더 많은 서버를 추가 하면 자동으로 받습니다 서버 인증서를 너무 합니다.  
  
10. 서버에서 그룹 정책 새로 고침. 그룹 정책이 새로 고쳐질 때 서버는 이전 단계에서 구성한 템플릿을 기반으로 하는 서버 인증서를 수신 합니다. 이 인증서는 인증 프로세스 중 클라이언트 컴퓨터에 해당 id를 증명 하기 위해 서버와 다른 서버에서 사용 됩니다.  
  
    > [!NOTE]  
    > 모든 도메인 구성원 컴퓨터는 엔터프라이즈 루트 CA의 인증서를 자동 등록의 구성 없이 자동으로 받습니다. 이 인증서는 자동 등록을 사용 하 여 배포 및 구성 하는 서버 인증서와 다릅니다. CA의 인증서가 자동으로 모든 도메인 구성원 컴퓨터에 대 한 신뢰할 수 있는 루트 인증 기관 인증서 저장소에 설치 되므로이 CA에서 발급 한 인증서를 신뢰 합니다.   
  
10. 모든 서버에 유효한 서버 인증서를 등록 한 것을 확인 합니다.  
  


