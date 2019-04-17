---
title: 서버 인증서 배포 개요
description: 이 항목은 802.1 X 유선 및 무선 배포에 대 한 배포 서버 인증서 가이드
manager: brianlic
ms.topic: article
ms.assetid: ca5c3e04-ae25-4590-97f3-0376a9c2a9a2
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4650c99325def63fd0df25989c661230fada3dac
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="server-certificate-deployment-overview"></a>서버 인증서 배포 개요

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 다음 섹션에 포함 되어 있습니다.  
  
-   [서버 인증서 배포 구성 요소](#bkmk_components)
  
-   [서버 인증서 배포 프로세스 개요](#bkmk_process)
  
## <a name="bkmk_components"></a>서버 인증서 배포 구성 요소
이 가이드를 사용 하 여 Active Directory 인증서 서비스 (AD CS)는 엔터프라이즈 루트 인증 기관 (캐나다)를 설치 하 고 서버 인증서 네트워크 NPS 정책 서버 (), 라우팅과 원격 액세스 서비스 (RRAS) 또는 둘 다 NPS RRAS 및 실행 하는 서버에 등록할 수 수 있습니다.


SDN 인증서 기반 인증을 배포 하는 경우 보안 통신을 이룰 수 있도록 해당 id 다른 서버 증명 서버 인증서를 사용 하 여 서버 필요 합니다.
  
다음은 서버 인증서 SDN 인프라의 서버에 배포 하는 데 필요한 구성 요소입니다.
  
![서버 인증서 배포 필요한 인프라](../../../media/Nps-Certs/Nps-Certs.jpg)  
  
> [!NOTE]  
> 위의 그림 여러 서버 나와: d c 1, CA1, WEB1, 및 많은 SDN 서버 합니다. 이 가이드 구성 d c 1,이 가이드에서는 사용자의 네트워크에 이미 설치 되어 가정 및 배포 및 CA1 및, WEB1 구성에 대 한 지침을 제공 합니다. 아직 Active Directory 도메인 설치 하지 않은 경우 할 수 있는 하도록를 사용 하 여는 [Core 네트워크 가이드](https://technet.microsoft.com/library/mt604042.aspx) Windows Server 2016 용 합니다.  
  
위의 그림 표시 각 항목에 대 한 자세한 내용은 다음을 참조 하십시오.  
  
-   [CA1](#bkmk_ca1)  
  
-   [WEB1](#bkmk_web1)  
  
-   [D C 1](#bkmk_dc1)  
  
-   [NPS1](#bkmk_nps1)  
  
### <a name="bkmk_ca1"></a>CA1 AD CS 서버 역할을 실행  
이 경우 (캐나다)에서 루트 Enterprise 인증 기관 이기도 발급 캘리포니아 합니다. 캘리포니아는 인증서를 등록 올바른 보안 권한 있는 서버 컴퓨터에 인증서 문제입니다. Active Directory 인증서 서비스 (AD CS) CA1에 설치 됩니다.  
  
큰 네트워크 또는 보안상의 이유로 맞춤을 제공 개별 루트 캘리포니아 및 발급 캘리포니아 역할 수 있으며 발급는 Ca 하위 Ca 배포할 수 있습니다.  
  
가장 안전한 배포 엔터프라이즈 루트 캘리포니아 오프 라인으로 물리적으로 수행 됩니다.   
  
#### <a name="capolicyinf"></a>CAPolicy.inf  
AD CS 설치 하기 전에 파일을 구성 하기 CAPolicy.inf 특정 설정을 사용 하 여 배포 합니다.  
  
#### <a name="copy-of-the-ras-and-ias-servers-certificate-template"></a>복사는 **RAS 및 IAS 서버** 인증서 템플릿을  
한 복사본을 만들 때 서버의 인증서를 배포 하기는 **RAS 및 IAS 서버** 인증서 템플릿 한 다음이 가이드의 요구 사항 및 지침에 따라 서식 구성 합니다.   
  
원본 템플릿 구성은 나중에 사용에 대 한 유지 되도록 원래 템플릿 보다 서식 파일의 복사본을 활용 합니다. 복사본을 구성는 **RAS 및 IAS 서버** 템플릿을 Active Directory 사용자 및 컴퓨터 사용자 지정 하는 그룹 문제는 캘리포니아 만들 수 있도록 서버 인증서를 합니다.  
  
#### <a name="additional-ca1-configuration"></a>추가 CA1 구성  
캐나다의 컴퓨터 id 증명으로에 제공 하는 인증서 유효 인증서 지 확인 하 고 해지 된를 확인 해야 하는 인증서 해지 목록 CRL ()를 게시 합니다. 컴퓨터를 인증 과정 CRL 찾을 위치를 알 수 있도록 기관 crl 정확한 위치를 구성 해야 합니다.  
  
### <a name="bkmk_web1"></a>WEB1 웹 IIS (서비스) 서버 역할을 실행  
웹 IIS () 서버 역할 WEB1를 실행 하는 컴퓨터에서 만들어야 폴더 Windows 탐색기에서로 CRL 및 AIA의 위치를 사용 하기 위해 합니다.  
  
#### <a name="virtual-directory-for-the-crl-and-aia"></a>가상 CRL와 AIA 디렉터리  
Windows 탐색기의 폴더를 만든 후 가상 디렉터리 서비스 IIS (인터넷 정보) 관리자도 가상 디렉터리에 대 한 액세스를 제어 목록 구성 컴퓨터 수 있도록 여기 게시 다음 AIA 및 CRL 액세스 하는 폴더를 구성할 해야 합니다.  
  
### <a name="bkmk_dc1"></a>D c 1 AD DS 및 DNS 서버 역할 실행  
D c 1 도메인 컨트롤러 및 네트워크에서 DNS 서버를입니다.  
  
#### <a name="group-policy-default-domain-policy"></a>그룹 정책 기본 도메인 정책  
기본 도메인 정책 인증서가 서버 NPS 및 RAS에 자동 하 고 캐나다의 인증서 템플릿을 구성 하 고 나면 그룹 정책에서 구성할 수 있습니다. 그룹 정책은 d c 1 서버의 AD DS에서 구성 됩니다.  
  
#### <a name="dns-alias-cname-resource-record"></a>DNS (CNAME) 리소스 기록 별칭  
서버를 AIA 및 CRL 서버에 저장 되어 있는 다른 컴퓨터를 찾을 수 있도록 하는 웹 서버에 대 한 (CNAME) 별칭 리소스 레코드를 만들어야 합니다. 또한 CNAME 리소스 레코드 별칭을 사용 하 여 FTP 및 웹 사이트와 같은 다른 목적을 위해 웹 서버를 사용할 수 있도록 유연 하 게를 제공 합니다.  
  
### <a name="bkmk_nps1"></a>NPS1 액세스 서비스 및 네트워크 정책 서버 역할의 네트워크 정책 서버 역할 서비스 실행  
이 가이드의 작업을 수행 하기 전에 해야 이미 하나 또는 네트워크에 더 많은 NPS 서버가 설치 되어 있으므로, Windows Server 2016 Core 네트워크 가이드의 작업을 수행할 때 NPS 서버가 설치 되어 있습니다.  
  
#### <a name="group-policy-applied-and-certificate-enrolled-to-servers"></a>그룹 정책을 적용 되며 인증서가 서버에 등록 한  
인증서 템플릿 및 자동 등록을 구성 하 고 나면 모든 대상 서버에서 그룹 정책의 복구할 수 있습니다. 지금은 서버에서 CA1 서버 인증서를 등록합니다.  
  
### <a name="bkmk_process"></a>서버 인증서 배포 프로세스 개요  
  
> [!NOTE]  
> 이러한 단계를 수행 하는 방법의 세부 정보 섹션에 제공 [서버 인증서 배포](../../../core-network-guide/cncg/server-certs/Server-Certificate-Deployment.md)합니다.  
  
이러한 단계에서 서버 인증서 등록이 구성 과정 발생 합니다.  
  
1.  WEB1, 웹 IIS () 역할을 설치 합니다.  
  
2.  D c 1 WEB1 웹 서버에 대 한 별칭 (CNAME) 레코드가 만듭니다.  
  
3.  캐나다에서 CRL 개최 된 다음 CRL 게시 하 고 새 가상 디렉터리에 엔터프라이즈 루트 인증서 복사 웹 서버를 구성 합니다.  
  
4.  AD CS 설치 하려는 컴퓨터의 컴퓨터에서 고정 IP 주소를 지정 컴퓨터, 컴퓨터에서 도메인에 가입 바꾸고 도메인 관리자 및 Enterprise 관리자 그룹에 포함 되어 있는 사용자 계정으로 컴퓨터에 로그온 합니다.  
  
5.  AD CS 설치 하려는 컴퓨터에서 배포 관련 된 설정을 사용 하 여 CAPolicy.inf 파일을 구성 합니다.  
  
6.  AD CS 서버 역할을 설치 하 고 있는 캘리포니아 추가 구성 수행 합니다.  
  
7.  CA1에서 CRL 및 캐나다 인증서 WEB1 웹 서버에서 공유를 복사 합니다.  
  
8.  캐나다, RAS 및 IAS 서버의 인증서 템플릿의 복사본을 구성 합니다. 발급 인증서 인증서 서식 기반으로 하므로 캘리포니아 인증서 드릴 수 전에 서식 서버 인증서에 대 한 구성 해야 합니다.  
  
9.  자동 서버 인증서 등록이 그룹 정책에서 구성 합니다. 자동 등록을 구성 그룹 구성원 Active Directory를 자동으로 지정 된 모든 서버 각 서버에서 그룹 정책을 고치면 서버 인증서를 수신 합니다. 더 많은 서버, 나중에 추가 하는 경우 자동으로 받게 됩니다 서버 인증서도 있습니다.  
  
10. 서버에서 그룹 정책을 새로 고칩니다. 그룹 정책, 새로 고침 서버 이전 단계에서 구성 서식 바탕으로 하는 서버 인증서를 수신 합니다. 이 인증서 인증 과정에서 id 클라이언트 컴퓨터를 증명 서버와 다른 서버에서 사용 됩니다.  
  
    > [!NOTE]  
    > 자동으로 모든 도메인 구성원 컴퓨터 구성 자동 등록 없이 엔터프라이즈 루트 캘리포니아 인증서를 받습니다. 이 인증서가 서버 인증서를 구성 하 고 자동 등록을 사용 하 여 배포 다릅니다. 캐나다의 인증서가이 캘리포니아 하 여 발급 된 인증서를 신뢰 하 않도록 도메인 회원 컴퓨터의 모든 신뢰할 수 있는 인증 기관 인증서 스토어에 자동으로 설치 됩니다.   
  
10. 모든 서버 유효한 서버 인증서가 등록 되어 있는지 확인 합니다.  
  


