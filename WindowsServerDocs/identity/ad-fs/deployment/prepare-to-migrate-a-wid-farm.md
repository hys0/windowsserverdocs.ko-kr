---
title: "AD 2.0 FS WID 농장 마이그레이션을 준비합니다"
description: "Windows Server 2012 ADFS 2.0 서버 WID 농장 마이그레이션을 준비 중에 대해 설명 합니다."
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4985a8d16614bd12bce991e196d105464d37634d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="prepare-to-migrate-an-ad-fs-20-wid-farm"></a>AD 2.0 FS WID 농장 마이그레이션을 준비합니다  
 Windows Server 2012를 Windows 내부 데이터베이스 (WID) 그룹에 속해 있는 ADFS 2.0 federation 서버 마이그레이션하기 준비 내보내기 고 이러한 서버에서 ADFS 구성 데이터를 백업 해야 합니다.  
  
 ADFS 구성 데이터를 내보내려면 다음 작업을 수행 합니다.  
  
-   [1 단계:-서비스 설정](#step-1-export-service-settings)  
  
-   [2 단계: 특성 사용자 지정 상점 백업](#step-2-back-up-custom-attribute-stores)  
  
-   [3 단계: 사용자 지정 웹 페이지를 백업](#step-3-back-up-webpage-customizations)  
  
## <a name="step-1-export-service-settings"></a>1 단계: 내보내기 서비스 설정  
 서비스 설정이 내보낼 다음 절차를 수행 합니다.  
  
### <a name="to-export-service-settings"></a>서비스 설정이 내보내려면  
  
1.  SSL 인증서 federation 서비스에서 사용 되는 인증서 주제 이름과 지문 값을 기록 합니다. SSL 인증서를 찾으려면 정보 IIS (인터넷 서비스) management console을 엽니다, 선택 **기본 웹 사이트** 왼쪽된 창에서 클릭 **바인딩을...** 에 **알림** 창, 찾기 및 선택 https 구속력 클릭 **편집**, 클릭 한 다음 **보기**합니다.  
  
> [!NOTE]
>  필요에 따라 ssl와 개인 키.pfx 파일에 내보낼 수 있습니다. 자세한 내용은 참조 [내보내려면 서버 인증 인증서의 개인 키 부분](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md)합니다.  
>   
>  이 단계는 선택적 때문에이 인증서 개인 인증서 스토어 로컬 컴퓨터에에서 저장 되 고 운영 체제로 업그레이드에 유지 됩니다.  
  
2.  토큰 서명, 토큰 암호화 또는 서비스 통신 인증서 및 생성 되지 않으면 내부적으로 자체 서명된 인증서 뿐 아니라 키를 내보냅니다.  
  
Windows PowerShell를 사용 하 여 서버에 사용 중인 모든 인증서를 볼 수 있습니다. Windows PowerShell 열고 ADFS cmdlet Windows PowerShell 세션에 추가 하려면 다음 명령을 실행: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`합니다. 서버에서 사용 중인 모든 인증서를 보려면 다음 명령을 실행 `PSH:>Get-ADFSCertificate`합니다. 이 명령을 출력 각 인증서의 스토어 위치를 지정 하는 StoreLocation 및 StoreName 값을 포함 합니다.  에 대 한 지침을 사용할 수 있습니다 [내보내려면 서버 인증 인증서의 개인 키 부분](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md) .pfx 파일을 각 인증서 및 개인 키를 내보내려면 합니다.  
  
> [!NOTE]
>  이 단계는 선택적 모든 외부 인증서 운영 체제로 업그레이드 하는 동안 그대로 유지 됩니다.  
  
3.  ADFS 2.0 federation 서비스 계정의 id 및이 계정의 암호를 기록 합니다.  
  
Id 값을 찾으려면 검사는 **사용자로 로그온** 열 **광고 FS 2.0 Windows 서비스** 에 **서비스** 콘솔 하 고 수동으로 값을 기록 합니다.  
  
## <a name="step-2-back-up-custom-attribute-stores"></a>2 단계: 특성 사용자 지정 상점 백업  
 Adfs에서 사용 중인 Windows PowerShell를 사용 하 여 사용자 지정 된 특성 스토어에 대 한 정보를 찾을 수 있습니다. Windows PowerShell 열고 ADFS cmdlet Windows PowerShell 세션에 추가 하려면 다음 명령을 실행: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`합니다. 사용자 지정 된 특성 스토어에 대 한 정보를 찾으려면 다음 명령을 실행: `PSH:>Get-ADFSAttributeStore`합니다. 업그레이드 또는 사용자 지정 된 특성 스토어 마이그레이션할 단계 다릅니다.  
  
## <a name="step-3-back-up-webpage-customizations"></a>3 단계: 사용자 지정 웹 페이지를 백업  
 모든 웹 페이지 사용자 지정을 백업 하려면 ADFS 웹 페이지를 복사 및 **web.config** 가상 경로 매핑됩니다 디렉터리의 파일 **"/ adfs/1!"** iis에서 합니다. 기본적으로에는 **%systemdrive%\inetpub\adfs\ls** 디렉터리 합니다.  

## <a name="next-steps"></a>다음 단계
 [광고 FS 2.0 Federation 서버 마이그레이션을 준비합니다](prepare-to-migrate-ad-fs-fed-server.md)   
 [광고 FS 2.0 Federation 서버 프록시 마이그레이션을 준비합니다](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [광고 FS 2.0 Federation Server를 마이그레이션해야](migrate-the-ad-fs-fed-server.md)   
 [광고 FS 2.0 Federation 서버 프록시 마이그레이션](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [광고 FS 1.1 웹 에이전트 마이그레이션](migrate-the-ad-fs-web-agent.md)