---
title: 3 단계 계획 OTP 인증서 배포
description: 이 항목은 Windows Server 2016에서 OTP 인증을 사용 하 여 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eca02eeb-d92d-463e-aae0-1f7038ba26fe
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4102fc4f7eacf0b407446717caa83e4e5f70ae57
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282365"
---
# <a name="step-3-plan-otp-certificate-deployment"></a>3 단계 계획 OTP 인증서 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2016

RADIUS 서버를 계획 한 후에 OTP (일회용 암호) 인증서, OTP 인증서 템플릿 및 원격에서 사용 된 등록 기관 인증서를 발급 하는 CA를 포함 하 여 인증 기관 (CA) 요구 사항에 대 한 계획 해야 합니다. 모든 DirectAccess 클라이언트 OTP 인증서 요청을 서명 하는 액세스 서버입니다. 이러한 인증서는 다음과 같이 사용 됩니다.  
  
1.  OTP 인증서를 요청 하는 DirectAccess 클라이언트 및 원격 액세스 서버가 요청을 수신 합니다.  
  
2.  원격 액세스 서버의 OTP 자격 증명을 확인 하 고 유효한 경우 서버 등록 기관으로 역할 단기 서명 인증서를 사용 하 여 OTP 인증서 등록 요청에 서명 합니다.  
  
3.  원격 액세스 서버를 DirectAccess 클라이언트에 다시 서명 된 인증서 등록 요청을 보냅니다.  
  
4.  그런 다음 클라이언트 OTP 서버에서 서명 된 인증서 등록 요청을 사용 하 여 CA에서 인증서를 등록 합니다.  
  
5.  CA 확인 자격 증명을 요청 합니다.  
  
|태스크|설명|  
|----|--------|  
|[3.1 OTP CA 계획](#bkmk_3_1_CA)|OTP 인증을 위해 DirectAccess 클라이언트에 인증서를 발급 하는 데 인증 기관 (CA)를 계획 합니다.|  
|[3.2 OTP 인증서 템플릿 계획](#bkmk_3_2_OTP_Cert)|OTP 인증서 템플릿을 계획 합니다.|
|[3.3 등록 기관 인증서 계획](#bkmk_33RACert)|모든 OTP 인증 인증서 요청을 서명 등록 기관 인증서를 계획 합니다.|

## <a name="bkmk_3_1_CA"></a>3.1 OTP CA 계획  
일회용 암호 인증 (OTP)를 사용 하 여 DirectAccess를 배포 하려면 DirectAccess 클라이언트 컴퓨터에 OTP 인증 인증서를 발급 하려면 내부 CA가 필요 합니다. 이 작업을 위해 일반 IPsec 컴퓨터 인증에 사용 되는 인증서를 발급 하는 데 사용 하는 것과 같은 내부 CA를 사용할 수 있습니다.  
  
## <a name="bkmk_3_2_OTP_Cert"></a>3.2 OTP 인증서 템플릿 계획  
각 DirectAccess 클라이언트가 내부 네트워크에 대 한 액세스 권한을 얻으려면 OTP 인증 인증서가 필요 합니다. OTP 인증서에 대 한 내부 CA에서 템플릿을 구성 해야 합니다. OTP 인증서 템플릿을 구성할 때 다음 note:  
  
-   OTP 인증을 수행 해야 하는 모든 사용자에 게 있어야 읽기 및 등록 권한을이 템플릿에 대 한 합니다.  
  
-   주체 이름 OTP 사용자 이름 및 인증서 요청을 수행 하는 원격 액세스 서버의 이름이 아니라 주체 이름 일치 하는지 확인 하려면 Active Directory 정보에서 구축 되어야 합니다. 주체 이름 정식 고유 이름 형식에서 이어야 합니다 하 고 주체 대체 이름을 UPN 형식 이어야 합니다. 이렇게 하면 등록된 된 OTP 인증서 스마트 카드 Kerberos 인증에 유효 합니다.  
  
-   인증서의 용도 스마트 카드 로그온 해야 합니다.  
  
-   발급 한 인증 된 서명을 해야 합니다. 서명은 등록 기관 서명 인증서 템플릿에 설정 된 미리 정의 된 DirectAccess OTP 응용 프로그램 정책을 사용 하 여 구성 되어야 합니다.  
  
-   유효 기간은 1 시간으로 설정 되어야 합니다.  
  
    > [!NOTE]  
    > 경우 여기서 CA 서버는 Windows Server 2003 컴퓨터를 다른 컴퓨터에서 템플릿을 구성 해야 합니다. 이것이 때문에 설정 합니다 **유효 기간** 시간 수 없는 2008/Vista 이전의 Windows 버전을 실행 하는 경우. 인증 서비스 역할이 설치 된 템플릿을 구성 하는 데 사용 하는 컴퓨터에 없는 경우는 클라이언트 컴퓨터 인증서 템플릿 스냅인을 설치 해야 할 수 있습니다. 이 주제에 대 한 자세한 내용은 [여기](https://technet.microsoft.com/library/cc732445.aspx)합니다.  
  
-   갱신 기간을 0으로 설정 되어야 합니다.  
  
-   (선택 사항) 인증서 및 요청 CA 데이터베이스에 저장 되어야 합니다.  
  
-   올바르게, 다음과 같이 인증서 확장 된 키 사용 매개 변수를 설정 해야 합니다.  
  
    -   DirectAccess에 대 한 서명 인증서 템플릿의 등록 1.3.6.1.4.1.311.81.1.1 키를 사용 합니다.  
  
    -   OTP 인증 인증서 템플릿에 대 한 키 1.3.6.1.4.1.311.20.2.2 키를 사용 합니다.  
  
## <a name="bkmk_33RACert"></a>3.3 등록 기관 인증서 계획  
DirectAccess 클라이언트는 OTP 인증서를 요청 하는 경우 원격 액세스 서버는 클라이언트로부터 요청을 받습니다. 원격 액세스 서버를 등록 기관 인증서를 사용 하 여 클라이언트에서 모든 OTP 인증서 요청을 서명 합니다. 요청 원격 액세스 서버에서 등록 기관 인증서로 서명 하는 경우에 CA 인증서를 발급 합니다. 내부 CA에서 인증서를 발급 해야, 인증서는 자체 서명 된 일 수 없습니다. OTP 인증서를 발급 한 CA에서 발급 하지 않아도 되지만 OTP 인증서를 발급 하는 CA는 등록 기관 서명 인증서를 발급 하는 CA를 신뢰 해야 합니다.  
  
## <a name="BKMK_Links"></a>참고 항목  
  
-   [4단계: 원격 액세스 서버의 OTP 계획](Step-4-Plan-for-OTP-on-the-Remote-Access-Server.md)  
  


