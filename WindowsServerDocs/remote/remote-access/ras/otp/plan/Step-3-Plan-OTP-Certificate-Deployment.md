---
title: 3 단계 OTP 인증서 배포 계획
description: 이 항목은 Windows Server 2016에서 OTP 인증을 사용 하 여 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eca02eeb-d92d-463e-aae0-1f7038ba26fe
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d34630b4faa8012eee73967a99bc0541f1305a09
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80313527"
---
# <a name="step-3-plan-otp-certificate-deployment"></a>3 단계 OTP 인증서 배포 계획

>적용 대상: Windows Server(반기 채널), Windows Server 2016

RADIUS 서버를 계획 한 후에는 OTP (일회용 암호) 인증서, OTP 인증서 템플릿 및 원격에서 사용 하는 등록 기관 인증서를 발급 하는 CA를 포함 하 여 CA (인증 기관) 요구 사항에 대 한 계획을 세워야 합니다. 모든 DirectAccess 클라이언트 OTP 인증서 요청을 서명할 서버에 액세스 합니다. 이러한 인증서는 다음과 같이 사용 됩니다.  
  
1.  DirectAccess 클라이언트는 OTP 인증서를 요청 하 고, 원격 액세스 서버는 요청을 수신 합니다.  
  
2.  원격 액세스 서버는 OTP 자격 증명을 확인 하 고, 유효한 경우 서버는 등록 기관 역할을 하며 단기 서명 인증서를 사용 하 여 OTP 인증서 등록 요청에 서명 합니다.  
  
3.  원격 액세스 서버는 서명 된 인증서 등록 요청을 DirectAccess 클라이언트로 다시 보냅니다.  
  
4.  그런 다음 클라이언트는 서버에서 서명한 인증서 등록 요청을 사용 하 여 CA에서 OTP 인증서를 등록 합니다.  
  
5.  CA는 자격 증명과 요청을 확인 합니다.  
  
|작업|설명|  
|----|--------|  
|[3.1 OTP CA 계획](#bkmk_3_1_CA)|OTP 인증을 위해 DirectAccess 클라이언트에 인증서를 발급 하는 데 사용할 CA (인증 기관)를 계획 합니다.|  
|[3.2 OTP 인증서 템플릿 계획](#bkmk_3_2_OTP_Cert)|OTP 인증서 템플릿을 계획 합니다.|
|[3.3 등록 기관 인증서 계획](#bkmk_33RACert)|모든 OTP 인증 인증서 요청을 서명 하도록 등록 기관 인증서를 계획 합니다.|

## <a name="31-plan-the-otp-ca"></a><a name="bkmk_3_1_CA"></a>3.1 OTP CA 계획  
OTP (일회성 암호 인증)를 사용 하 여 DirectAccess를 배포 하려면 DirectAccess 클라이언트 컴퓨터에 OTP 인증 인증서를 발급 하기 위한 내부 CA가 필요 합니다. 이러한 목적을 위해 일반 IPsec 컴퓨터 인증에 사용 되는 인증서를 발급 하는 데 사용 하는 것과 동일한 내부 CA를 사용할 수 있습니다.  
  
## <a name="32-plan-the-otp-certificate-template"></a><a name="bkmk_3_2_OTP_Cert"></a>3.2 OTP 인증서 템플릿 계획  
각 DirectAccess 클라이언트는 내부 네트워크에 대 한 액세스 권한을 얻기 위해 OTP 인증 인증서가 필요 합니다. OTP 인증서에 대 한 내부 CA에서 템플릿을 구성 해야 합니다. OTP 인증서 템플릿을 구성할 때 다음 사항에 유의 하세요.  
  
-   OTP 인증을 수행 해야 하는 모든 사용자에 게는이 템플릿에 대 한 읽기 및 등록 권한이 있어야 합니다.  
  
-   주체 이름은 인증서 요청을 수행 하는 원격 액세스 서버의 이름이 아니라 OTP 사용자 이름과 일치 하는지 확인 하기 위해 Active Directory 정보에서 작성 해야 합니다. 주체 이름은 정규화 된 이름 형식 이어야 하 고 주체 대체 이름은 UPN 형식 이어야 합니다. 이렇게 하면 등록 된 OTP 인증서가 스마트 카드 Kerberos 인증에 유효 합니다.  
  
-   인증서의 용도는 스마트 카드 로그온 이어야 합니다.  
  
-   발급 하려면 인증 된 서명이 하나 필요 합니다. 등록 기관 서명 인증서 템플릿에 설정 된 미리 정의 된 DirectAccess OTP 응용 프로그램 정책을 사용 하 여 서명을 구성 해야 합니다.  
  
-   유효 기간은 1 시간으로 설정 해야 합니다.  
  
    > [!NOTE]  
    > CA 서버가 Windows Server 2003 컴퓨터인 경우에는 다른 컴퓨터에 템플릿을 구성 해야 합니다. 이는 2008/Vista 이전 Windows 버전을 실행 하는 경우에는 **유효 기간** 을 시간으로 설정 하지 못할 수 있기 때문입니다. 템플릿을 구성 하는 데 사용 하는 컴퓨터에 인증 서비스 역할이 설치 되어 있지 않거나 클라이언트 컴퓨터인 경우 인증서 템플릿 스냅인을 설치 해야 할 수 있습니다. 이 주제에 대 한 자세한 내용을 보려면 [여기](https://technet.microsoft.com/library/cc732445.aspx)를 클릭 하세요.  
  
-   갱신 기간은 0으로 설정 해야 합니다.  
  
-   필드 인증서와 요청은 CA 데이터베이스에 저장 하면 안 됩니다.  
  
-   다음과 같이 certificate 확장 키 사용 매개 변수를 올바르게 설정 해야 합니다.  
  
    -   DirectAccess 등록 서명 인증서 템플릿의 경우 1.3.6.1.4.1.311.81.1.1 키를 사용 합니다.  
  
    -   OTP 인증 인증서 템플릿의 경우 key 1.3.6.1.4.1.311.20.2.2 키를 사용 합니다.  
  
## <a name="33-plan-the-registration-authority-certificate"></a><a name="bkmk_33RACert"></a>3.3 등록 기관 인증서 계획  
DirectAccess 클라이언트가 OTP 인증서를 요청 하면 원격 액세스 서버에서 클라이언트의 요청을 수신 합니다. 원격 액세스 서버는 등록 기관 인증서를 사용 하 여 클라이언트의 모든 OTP 인증서 요청에 서명 합니다. CA는 원격 액세스 서버의 등록 기관 인증서에 의해 요청이 서명 된 경우에만 인증서를 발급 합니다. 인증서는 내부 CA에서 발급 해야 하며 인증서는 자체 서명 될 수 없습니다. OTP 인증서를 발급 한 ca는이를 발급 하지 않아도 되지만 OTP 인증서를 발급 하는 CA는 등록 기관 서명 인증서를 발급 하는 CA를 신뢰 해야 합니다.  
  
## <a name="see-also"></a><a name="BKMK_Links"></a>참고 항목  
  
-   [4 단계: 원격 액세스 서버에 대 한 OTP 계획](Step-4-Plan-for-OTP-on-the-Remote-Access-Server.md)  
  


