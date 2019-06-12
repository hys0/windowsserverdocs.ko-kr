---
title: 802.1 X 유선 및 무선 배포용 서버 인증서 배포
description: 이 항목은 서버 배포 인증서 802.1 X 유선 및 무선 배포 가이드의 일부
manager: brianlic
ms.topic: article
ms.assetid: 0a39ecae-39cc-4f26-bd6f-b71ed02fc4ad
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2d4cdcd11e0eb334064ddefec0eda775ffccff2c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446474"
---
# <a name="deploy-server-certificates-for-8021x-wired-and-wireless-deployments"></a>802.1 X 유선 및 무선 배포용 서버 인증서 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2016

원격 액세스 및 네트워크 정책 (NPS 서버) 인프라 서버에 서버 인증서를 배포 하려면이 가이드를 사용할 수 있습니다.   

이 가이드에는 다음 섹션이 수록되어 있습니다.  

-   [이 가이드를 사용 하기 위한 필수 구성 요소](#bkmk_pre)  

-   [이 가이드에서 설명하지 않는 정보](#bkmk_not)  

-   [기술 개요](#bkmk_tech)  

-   [서버 인증서 배포 개요](Server-Certificate-Deployment-Overview.md)  

-   [서버 인증서 배포 계획](Server-Certificate-Deployment-Planning.md)  

-   [서버 인증서 배포](Server-Certificate-Deployment.md)  

### <a name="digital-server-certificates"></a>**디지털 서버 인증서**  
이 가이드는 Active Directory 인증서 서비스 (AD CS)를 사용 하 여 원격 액세스 및 NPS 인프라 서버에 인증서를 자동으로 등록에 대 한 지침을 제공 합니다. AD CS를 사용 하면 공개 키 인프라 (PKI)를 빌드 및 조직에 대 한 공개 키 암호화, 디지털 인증서 및 디지털 서명 기능을 제공할 수 있습니다.  

네트워크에 있는 컴퓨터 간의 인증을 위해 디지털 서버 인증서를 사용 하는 경우 인증서를 제공 합니다.   

1. 암호화를 통해 기밀을 유지 합니다.  
2. 디지털 서명 통한 무결성입니다.  
3. 컴퓨터 네트워크의 컴퓨터, 사용자 또는 장치 계정에 인증서 키를 연결 하 여 인증 합니다.  

### <a name="server-types"></a>**서버 유형**  
이 가이드를 사용 하 여 다음 유형의 서버를 서버 인증서를 배포할 수 있습니다.  
- 서버 원격 액세스 서비스를 실행 하는 DirectAccess 또는 표준 VPN(가상 사설망) 서버 및 멤버는 **RAS 및 IAS Servers** 그룹입니다.  
- 네트워크 정책 (NPS 서버) 서비스를 실행 하는 서버는의 멤버는 **RAS and IAS Servers** 그룹입니다.  

### <a name="advantages-of-certificate-autoenrollment"></a>**인증서 자동 등록의 장점**  
자동 등록을 라고도 하는 서버 인증서의 자동 등록은 다음과 같은 이점을 제공 합니다.  

- AD CS 인증 기관 (CA)에 모든 NPS 및 원격 액세스 서버에 서버 인증서를 자동으로 등록 됩니다.  
- 도메인의 모든 컴퓨터에 신뢰할 수 있는 루트 인증 기관에 설치 된 CA 인증서를 자동으로 수신 모든 도메인 구성원 컴퓨터에 저장 합니다. 이 인해 도메인의 모든 컴퓨터는 CA에서 발급 한 인증서를 신뢰 합니다. 이 트러스트를 서로 자신의 id를 증명 및 보안 통신에 참여 하 여 인증 서버 수 있습니다.  
- 그룹 정책 새로 고침을 이외의 모든 서버 수동 재구성 필요 하지 않습니다.  
- 확장 키 사용 현황 EKU (향상)에서 서버 인증 용도로 및 클라이언트 인증 용도의 모두를 포함 하는 모든 서버 인증서입니다.  
- 확장성입니다. 이 가이드에 엔터프라이즈 루트 CA를 배포한 후 엔터프라이즈 하위 Ca를 추가 하 여 공개 키 인프라 (PKI)를 확장할 수 있습니다.  
- 관리 효율성입니다. AD CS 콘솔을 사용 하거나 Windows PowerShell 명령 및 스크립트를 사용 하 여 AD CS를 관리할 수 있습니다.  
- 단순성입니다. Active Directory 그룹 계정 및 그룹 멤버 자격을 사용 하 여 서버 인증서를 등록 하는 서버를 지정 합니다.   
- 서버 인증서를 배포할 때 인증서는이 가이드의 지침을 구성 하는 서식 파일을 기반으로 합니다. 즉, 특정 서버 유형에 대 한 다른 인증서 템플릿을 사용자 지정할 수 있습니다 하거나 발급 하고자 하는 모든 서버 인증서에 대 한 같은 서식 파일을 사용할 수 있습니다.  

## <a name="bkmk_pre"></a>이 가이드를 사용 하기 위한 필수 구성 요소  

이 가이드에서는 Windows Server 2016의 AD CS 및 웹 서버 (IIS) 서버 역할을 사용 하 여 서버 인증서를 배포 하는 방법을 설명 합니다. 이 가이드의 절차를 수행 하기 위한 필수 구성 요소는 다음과가 같습니다.  

- Windows Server 2016 핵심 네트워크 가이드를 사용 하 여 핵심 네트워크를 배포 해야 하거나 설치 하 고 네트워크에서 제대로 작동 하는 핵심 네트워크 가이드에서 제공 하는 기술을 이미 있어야 합니다. 이러한 기술은 다음과 TCP/IP v4, DHCP, Active Directory 도메인 서비스 (AD DS), DNS 및 NPS 합니다.  
  >[!NOTE]
  >Windows Server 2016 핵심 네트워크 가이드는 Windows Server 2016 기술 라이브러리에서 사용할 수 있습니다. 자세한 내용은 참조 [핵심 네트워크 가이드](../../../core-network-guide/Core-Network-Guide.md)합니다.

- 배포를 수행 하기 전에이 배포에 대 한 준비가 되도록이 가이드의 계획 섹션을 참조 해야 합니다.  
- 이 가이드에 소개 된 순서에 단계를 수행 해야 합니다. 실패 하는 서버 또는 배포를 배포 하는 단계를 수행 하지 않고 CA 배포을 이동 하지 않고 있습니다.  
- 두 명의 새 서버 네트워크에서 한 서버는를 엔터프라이즈 루트 CA로 AD CS를 설치 합니다 및는 설치는 CA 웹 서버에 인증서 해지 목록 (CRL)을 게시할 수 있도록 웹 서버 (IIS) 서버를 배포 하는 대비해 야 합니다.   

>[!NOTE]  
>이 가이드에도 사용자 조직 명명 규칙에 따라 컴퓨터 이름에 대 한 배포 하는 웹 및 AD CS 서버에 고정 IP 주소를 할당할 준비가 됩니다. 또한 사용자의 도메인에 컴퓨터를 조인 해야 합니다.  

## <a name="bkmk_not"></a>새로운이 가이드에서는  
이 가이드는 설계 및 AD CS를 사용 하 여 공개 키 인프라 (PKI)를 배포 하기 위한 포괄적인 지침을 제공 하지 않습니다. AD CS 및 PKI 디자인 설명서가이 가이드에 포함 된 기술을 배포 하기 전에 검토 하는 것이 좋습니다.   

## <a name="bkmk_tech"></a>기술 개요  
다음은 AD CS 및 웹 서버 (IIS)에 대 한 기술 개요입니다.  

### <a name="active-directory-certificate-services"></a>Active Directory 인증서 서비스  
Windows Server 2016의 AD CS 만들고 공개 키 기술을 사용 하는 소프트웨어 보안 시스템에서 사용 되는 X.509 인증서를 관리 하기 위한 사용자 지정 가능한 서비스를 제공 합니다. 조직에서는 사람, 장치 또는 서비스의 id는 해당 공개 키에 바인딩하여 보안을 강화 하기 위해 AD CS를 사용할 수 있습니다. AD CS에는 인증서 등록 및 해지 다양 한 확장 가능한 환경에서에서 관리할 수 있는 기능이 포함 되어 있습니다.  

자세한 내용은 참조 [Active Directory 인증서 서비스 개요](https://technet.microsoft.com/library/hh831740.aspx) 및 [공개 키 인프라 디자인 지침](https://social.technet.microsoft.com/wiki/contents/articles/2901.public-key-infrastructure-design-guidance.aspx)합니다.  

### <a name="web-server-iis"></a>웹 서버(IIS)  

Windows Server 2016에서 웹 서버 (IIS) 역할 웹 사이트, 서비스 및 응용 프로그램을 안정적으로 호스팅하기 위한 안전, 관리 하기 쉬운, 모듈식 하 고 확장 가능한 플랫폼을 제공 합니다. Iis에서 인터넷, 인트라넷 또는 엑스트라넷 사용자와 정보를 공유할 수 있습니다. IIS는 IIS, ASP.NET, FTP 서비스, PHP 및 Windows Communication Foundation (WCF)를 통합 하는 통합형된 웹 플랫폼.  

자세한 내용은 참조 [웹 서버 (IIS) 개요](https://technet.microsoft.com/library/hh831725.aspx)합니다.  
