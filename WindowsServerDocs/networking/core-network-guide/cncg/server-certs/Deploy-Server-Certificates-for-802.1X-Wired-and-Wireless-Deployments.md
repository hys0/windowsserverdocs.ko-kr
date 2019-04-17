---
title: 802.1 X 유무선 배포에 대 한 서버 인증서를 배포 합니다.
description: 이 항목은 802.1 X 유선 및 무선 배포에 대 한 배포 서버 인증서 가이드
manager: brianlic
ms.topic: article
ms.assetid: 0a39ecae-39cc-4f26-bd6f-b71ed02fc4ad
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fda9b2b53d088cc389e98cf96fecd748419bc6e2
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="deploy-server-certificates-for-8021x-wired-and-wireless-deployments"></a>802.1 X 유무선 배포에 대 한 서버 인증서를 배포 합니다.

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 가이드 서버 인증서에 대 한 원격 액세스 및 네트워크 NPS 정책 서버 () infrastructure 서버에 배포 하는 사용할 수 있습니다.   

이 가이드 다음 섹션에 포함 되어 있습니다.  

-   [이 가이드를 사용 하 여 사항](#bkmk_pre)  

-   [이 가이드 제공 하지 않는 항목](#bkmk_not)  

-   [기술 개요](#bkmk_tech)  

-   [서버 인증서 배포 개요](Server-Certificate-Deployment-Overview.md)  

-   [서버 인증서를 배포 계획](Server-Certificate-Deployment-Planning.md)  

-   [서버 인증서 배포](Server-Certificate-Deployment.md)  

### **<a name="digital-server-certificates"></a>디지털 서버 인증서**  
이 가이드 Active Directory 인증서 서비스 (AD CS) 인증서를 원격 액세스와 NPS 인프라 서버에 등록할 자동으로 사용 되는 지침을 제공 합니다. AD CS 공개 키 인프라 (PKI) 빌드하고 조직에 대 한 주요 공개 암호화, 디지털 인증서 및 디지털 서명이 기능을 제공 수 있습니다.  

네트워크에서 컴퓨터 간에 인증에 대 한 디지털 서버 인증서를 사용 하는 경우는 인증서를 제공 합니다.   

1. 암호화를 통해 기밀성 합니다.  
2. 디지털 서명 통해 무결성 합니다.  
3. 인증서 키 컴퓨터나, 사용자 장치 계정 컴퓨터가 네트워크에 연결 하 여 인증 합니다.  

### **<a name="server-types"></a>서버 유형**  
이 가이드를 사용 하 여 서버 인증서 다음과 같은 유형의 서버에 배포할 수 있습니다.  
- 실행 하는 서버 원격 액세스 서비스는 DirectAccess 또는 표준 가상 개인 네트워크 (VPN) 서버은 쉽고의 회원은 **RAS 및 서버 IAS** 그룹입니다.  
- 네트워크 NPS 정책 서버 () 서비스를 실행 하는 서버의 회원은는 **RAS 및 서버 IAS** 그룹입니다.  

### **<a name="advantages-of-certificate-autoenrollment"></a>자동 등록 인증서의 이점**  
자동 등록을 라고도 서버 인증서의 자동 등록 다음과 같은 이점을 제공 합니다.  

- AD CS 인증 기관 (캐나다)는 자동으로 서버 인증서 모든 NPS 원격 액세스 하 고 서버에 등록 합니다.  
- 모든 컴퓨터가 도메인에 있는 루트 신뢰할 수 있는 인증 기관에 설치 되어 있는 캘리포니아 인증서를 자동으로 받게 모든 도메인 회원 컴퓨터에 저장 합니다. 이 때문 도메인에 있는 모든 컴퓨터 기관에서 발급 된 인증서를 신뢰. 이 보안 해당 id를 서로 증명 보안 통신에 참여 하 여 인증 서버 수 있습니다.  
- 그룹 정책, 새로 고침 이외의 수동 모든 서버 재구성 필요 하지 않습니다.  
- 모든 서버 인증서 향상 키 EKU () 확장에 서버 인증 목적 및 클라이언트 인증 목적을 포함합니다.  
- 확장성 합니다. 이 가이드 엔터프라이즈 루트 기관을 배포한 후 공개 키 인프라 (PKI) Enterprise 하위 Ca 추가 하 여 확장할 수 있습니다.  
- 관리 합니다. AD CS AD CS 콘솔을 사용 하 여 또는 명령 Windows PowerShell 스크립트를 사용 하 여 관리할 수 있습니다.  
- 간편 하 게 됩니다. 그룹 계정과 그룹 구성원 Active Directory를 사용 하 여 서버 인증서를 등록 하는 서버를 지정 합니다.   
- 서버 인증서 배포할 때 인증서가 가이드에서 지침과 함께 구성 서식을 기반으로 합니다. 즉, 특정 서버 형식에 대 한 다양 한 인증서 템플릿 사용자 지정할 수 또는 발급 하고자 하는 모든 서버 인증서 같은 서식 파일을 사용할 수 있습니다.  

## <a name="bkmk_pre"></a>이 가이드를 사용 하 여 사항  

이 가이드 서버 인증서 AD CS 및 웹 서버 IIS () 서버 역할은 Windows Server 2016에 사용 하 여 배포 하는 방법에 대해 설명 합니다. 이 가이드는 절차를 수행 하기 위한 필수는 다음과가 같습니다.  

- Windows Server 2016 Core 네트워크 가이드를 사용 하는 핵심 네트워크 배포 해야 하거나 이미 설치 되어 있고 네트워크에서 제대로 작동 핵심 네트워크 가이드에 제공 되는 기술 있어야 합니다. 이러한 기술을 TCP/IP v4, DHCP, Active Directory Domain Services (AD DS), DNS 및 NPS 포함 됩니다.  
>[!NOTE]
>Windows Server 2016 기술 라이브러리 Windows Server 2016 Core 네트워크 가이드를 사용할 수 있습니다. 자세한 내용은 참조 [Core 네트워크 가이드](../../../core-network-guide/Core-Network-Guide.md)합니다.

- 이 가이드를 배포를 수행 하기 전에이 배포에 대 한 준비가 계획 섹션을 읽어야 합니다.  
- 이 가이드에 나와 있는 순서의 단계를 수행 해야 합니다. 앞으로 이동 하 고 실패 서버 또는 배포 배포 하는 단계를 수행 하지 않고 기관 배포 하지 않습니다.  
- 네트워크-있는 AD CS 엔터프라이즈 루트 캐나다도 설치 됩니다 하나 서버와 있는 설치 됩니다 인증 인증서 해지 목록 (CRL)의 웹 서버에 게시할 수 있도록 웹 IIS () 서버에 두 가지 새로운 서버 배포할 준비가 해야 합니다.   

>[!NOTE]  
>이 가이드를 배포 하는 웹 및 AD CS 서버에서 고정 IP 주소를 지정 하려면 뿐만 아니라 조직 용어가 따라 컴퓨터의 이름을 지정 준비 됩니다. 또한 컴퓨터 도메인에 가입 해야 합니다.  

## <a name="bkmk_not"></a>이 가이드 제공 하지 않는 항목  
이 가이드를 디자인 하 고 공개 키 인프라 (PKI) 배포 포괄적인 지침 AD CS을 사용 하 여 제공 하지 않습니다. AD CS 및 PKI 기술이이 가이드에 배포 하기 전에 디자인 설명서를 검토 하는 것이 좋습니다.   

## <a name="bkmk_tech"></a>기술 개요  
다음은 AD CS 및 웹 서버 (IIS)에 대 한 기술 개요입니다.  

### <a name="active-directory-certificate-services"></a>Active Directory 인증서 서비스  
Windows Server 2016에 AD CS 만들고 공개 키 기술을 사용 하는 소프트웨어의 보안 시스템에 사용 되는 X.509 인증서 관리 하기 위한 사용자 지정 가능한 서비스를 제공 합니다. 조직은 AD CS 해당 공개 키를 사람, 디바이스 또는 서비스의 id 하 여 보안 강화를 사용할 수 있습니다. AD CS 인증서 등록이 및 다양 한 확장 환경에서에서 해지 관리할 수 있는 기능이 포함 되어 있습니다.  

자세한 내용은 참조 [Active Directory 인증서 서비스 개요](https://technet.microsoft.com/library/hh831740.aspx) 및 [공개 키 Infrastructure 디자인 지침](https://social.technet.microsoft.com/wiki/contents/articles/2901.public-key-infrastructure-design-guidance.aspx)합니다.  

### <a name="web-server-iis"></a>웹 서버 IIS)  

Windows Server 2016에는 웹 서버 (IIS) 역할 안정적으로 웹 사이트, 서비스 및 응용 프로그램을 호스트할 안전 하 고 관리 하기 쉬운, 모듈식 있으며 extensible 플랫폼을 제공 합니다. Iis 인터넷, 인트라넷과 또는 엑스트라넷 정보 사용자와 공유할 수 있습니다. IIS는 IIS, ASP.NET, FTP 서비스, PHP, 및 Windows WCF () 통합 하는 웹 통합된 플랫폼입니다.  

자세한 내용은 참조 [웹 서버 (IIS) 개요](https://technet.microsoft.com/library/hh831725.aspx)합니다.  
