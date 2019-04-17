---
title: "광고 FS 2.0 Federation 서버 프록시 마이그레이션을 준비합니다"
description: "Windows Server 2012 ADFS 서버 프록시 마이그레이션을 준비 중에 대해 설명 합니다."
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f207993580e6fd06c9ff185e58e5b7e81af60252
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="prepare-to-migrate-the-ad-fs-20-federation-server-proxy"></a>광고 FS 2.0 Federation 서버 프록시 마이그레이션을 준비합니다

Windows Server 2012 ADFS 2.0 federation 서버 프록시 마이그레이션하 준비 내보내기 고이 서버 프록시에서 ADFS 구성 데이터를 백업 해야 합니다.  이 항목의 단계 한 프록시 federation 서버를 시나리오를 또는 여러 프록시 federation 서버에 적용 됩니다.  
  
 ADFS 구성 데이터를 내보내려면 다음 작업을 수행 합니다.  
  
-   [1 단계: 내보내기 프록시 서비스 설정](#step-1-export-proxy-service-settings)  
  
-   [2 단계: 사용자 지정 웹 페이지를 백업](#step-2-back-up-webpage-customizations)  
  
##  <a name="step-1-export-proxy-service-settings"></a>1 단계: 내보내기 프록시 서비스 설정  
 Federation 서버 프록시 서비스 설정 내보낼 다음 절차를 수행 합니다.  
  
### <a name="to-export-proxy-service-settings"></a>서비스 설정이 프록시를 내보내려면  
  
1.  .Pfx 파일로 Layer SSL (Secure Sockets) 인증서와 개인 키 내보냅니다. 자세한 내용은 참조 [내보내려면 서버 인증 인증서의 개인 키 부분](export-the-private-key-portion-of-a-server-authentication-certificate.md)합니다.  
  
> [!NOTE]
>  이 단계는 선택적 되므로이 인증서 운영 체제로 업그레이드 하는 동안 그대로 유지 됩니다.  
  
2.  파일을 ADFS 2.0 federation 프록시 속성 내보냅니다. Windows PowerShell를 사용 하 여 하는 작업을 수행할 수 있습니다.  
  
Windows PowerShell 열고 ADFS cmdlet Windows PowerShell 세션에 추가 하려면 다음 명령을 실행: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`합니다. 파일을 federation 프록시 속성 내보낼 다음 명령을 실행: `PSH:> Get-ADFSProxyProperties | out-file “.\proxyproperties.txt”`합니다.  
  
3.  ADFS federation 서버 관리자 계정 또는 ADFS federation 서비스가 실행 되는 서비스 계정 자격 증명을 알 수 있는지 확인 합니다.  이 정보는 프록시 보안 설정에 대 한 필요 합니다.  
  
 다음 ADFS federation 프록시 서버를 구성 하는 데 필요한 정보를 수집 결과이 단계를 완료 다음과 같습니다.  
  
-   광고 FS federation 서비스 이름  
  
-   프록시 보안 설정에 대 한 해야 하는 도메인 계정 이름  
  
-   주소 (HTTP 프록시 ADFS federation 서버 프록시와 ADFS federation 서버 있는 경우) HTTP 프록시 포트 하 고  
  
##  <a name="step-2-back-up-webpage-customizations"></a>2 단계: 사용자 지정 웹 페이지를 백업  
 사용자 지정 웹 페이지를 백업 하려면 ADFS 프록시 웹 페이지를 복사 및 **web.config** 가상 경로 매핑됩니다 디렉터리의 파일 **"/ adfs/1!"** iis에서 합니다.  기본적으로에는 **%systemdrive%\inetpub\adfs\ls** 디렉터리 합니다.  
  
## <a name="next-steps"></a>다음 단계
 [광고 FS 2.0 Federation 서버 마이그레이션을 준비합니다](prepare-to-migrate-ad-fs-fed-server.md)   
 [광고 FS 2.0 Federation 서버 프록시 마이그레이션을 준비합니다](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [광고 FS 2.0 Federation Server를 마이그레이션해야](migrate-the-ad-fs-fed-server.md)   
 [광고 FS 2.0 Federation 서버 프록시 마이그레이션](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [광고 FS 1.1 웹 에이전트 마이그레이션](migrate-the-ad-fs-web-agent.md)