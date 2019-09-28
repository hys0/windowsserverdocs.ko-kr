---
title: AD FS 2.0 페더레이션 서버 프록시 마이그레이션 준비
description: AD FS 서버 프록시를 Windows Server 2012로 마이그레이션할 준비에 대 한 정보를 제공 합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 20fbf3ea9231706635df2bd4c1d541fde0c1484b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408206"
---
# <a name="prepare-to-migrate-the-ad-fs-20-federation-server-proxy"></a>AD FS 2.0 페더레이션 서버 프록시 마이그레이션 준비

AD FS 2.0 페더레이션 서버 프록시를 Windows Server 2012로 마이그레이션하기 위해 준비 하려면이 서버 프록시에서 AD FS 구성 데이터를 내보내고 백업 해야 합니다.  이 항목의 단계는 프록시 페더레이션 서버가 하나 이상 포함된 시나리오에 적용됩니다.  
  
 AD FS 구성 데이터를 내보내려면 다음 작업을 수행합니다.  
  
-   [1단계: 프록시 서비스 설정 내보내기 @ no__t-0  
  
-   [2단계: 웹 페이지 사용자 지정 백업 @ no__t-0  
  
##  <a name="step-1-export-proxy-service-settings"></a>1단계: 프록시 서비스 설정 내보내기  
 페더레이션 서버 프록시 서비스 설정을 내보내려면 다음 절차를 수행합니다.  
  
### <a name="to-export-proxy-service-settings"></a>프록시 서비스 설정을 내보내려면  
  
1.  SSL(Secure Sockets Layer) 인증서와 해당 프라이빗 키를 .pfx 파일로 내보냅니다. 자세한 내용은 [서버 인증 인증서의 프라이빗 키 부분 내보내기](export-the-private-key-portion-of-a-server-authentication-certificate.md)를 참조하세요.  
  
> [!NOTE]
>  이 단계는 옵션입니다. 이 인증서는 운영 체제 업그레이드 중에 유지되기 때문입니다.  
  
2. AD FS 2.0 페더레이션 프록시 속성을 파일로 내보냅니다. Windows PowerShell을 사용하여 이 작업을 수행할 수 있습니다.  
  
Windows PowerShell을 열고 `PSH:>add-pssnapin “Microsoft.adfs.powershell”`명령을 실행하여 Windows PowerShell 세션에 AD FS cmdlet을 추가합니다. 그런 다음 `PSH:> Get-ADFSProxyProperties | out-file “.\proxyproperties.txt”`명령을 실행하여 페더레이션 프록시 속성을 파일로 내보냅니다.  
  
3. AD FS 페더레이션 서버의 관리자인 계정 또는 AD FS 페더레이션 서비스가 실행되는 서비스 계정의 자격 증명을 알고 있어야 합니다.  프록시 트러스트를 설정하려면 이 정보가 필요합니다.  
  
   이 단계를 완료하면 AD FS 페더레이션 서버 프록시를 구성하는 데 필요한 다음 정보가 수집됩니다.  
  
-   AD FS 페더레이션 서비스 이름  
  
-   프록시 트러스트 설정에 필요한 도메인 계정의 이름  
  
-   HTTP 프록시의 주소 및 포트(AD FS 페더레이션 서버 프록시와 AD FS 페더레이션 서버 사이에 HTTP 프록시가 있는 경우)  
  
##  <a name="step-2-back-up-webpage-customizations"></a>2단계: 웹 페이지 사용자 지정 백업  
 웹 페이지 사용자 지정 항목을 백업하려면 IIS의 가상 경로 **“/adfs/ls”** 에 매핑된 디렉터리에서 **web.config** 파일과 AD FS 프록시 웹 페이지를 복사합니다.  기본적으로 **%systemdrive%\inetpub\adfs\ls** 디렉터리에 있습니다.  
  
## <a name="next-steps"></a>다음 단계
 [AD FS 2.0 페더레이션 서버 마이그레이션 준비](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 페더레이션 서버 프록시 @no__t 마이그레이션 준비](prepare-to-migrate-ad-fs-fed-proxy.md)-1  
 [AD FS 2.0 페더레이션 서버 마이그레이션](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 페더레이션 서버 프록시](migrate-the-ad-fs-2-fed-server-proxy.md) 을 마이그레이션합니다.  
 [AD FS 1.1 웹 에이전트 마이그레이션](migrate-the-ad-fs-web-agent.md)