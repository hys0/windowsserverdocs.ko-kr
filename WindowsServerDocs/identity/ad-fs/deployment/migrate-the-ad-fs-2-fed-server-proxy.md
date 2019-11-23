---
title: AD FS 2.0 페더레이션 서버 프록시 마이그레이션
description: AD FS 페더레이션 서버 프록시를 Windows Server 2012로 마이그레이션하는 방법에 대 한 정보를 제공 합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: e97a1b3b66d7c12c96570022b7e69caaf0e92f65
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408223"
---
# <a name="migrate-the-ad-fs-20-federation-server-proxy"></a>AD FS 2.0 페더레이션 서버 프록시 마이그레이션
이 문서에서는 AD FS 2.0 페더레이션 프록시 서버를 Windows Server 2012로 마이그레이션하는 방법에 대 한 자세한 정보를 제공 합니다.

## <a name="migrate-the-proxy"></a>프록시 마이그레이션

AD FS 2.0 페더레이션 서버 프록시를 Windows Server 2012로 마이그레이션하려면 다음 절차를 수행 합니다.  
  
1.  Windows Server 2012로 마이그레이션하려는 모든 페더레이션 서버 프록시에 대해 [AD FS 2.0 페더레이션 서버 프록시 마이그레이션 준비](prepare-to-migrate-ad-fs-fed-proxy.md)의 절차를 검토 하 고 수행 합니다.  
  
2.  부하 분산 장치에서 페더레이션 서버 프록시를 제거합니다.  
  
3.  Windows Server 2008 R2 또는 Windows server 2008에서 Windows Server 2012로이 서버의 운영 체제에 대 한 전체 업그레이드를 수행 합니다. 자세한 내용은 [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx)를 참조하세요.  
  
> [!IMPORTANT]
>  운영 체제 업그레이드로 인해 이 서버의 AD FS 프록시 구성이 손실되고 AD FS 2.0 서버 역할이 제거됩니다. Windows Server 2012 AD FS 서버 역할이 대신 설치 되지만 구성 되지 않습니다. 수동으로 원래 AD FS 프록시 구성을 만들고 나머지 AD FS 프록시 설정을 복원하여 페더레이션 서버 프록시 마이그레이션을 완료해야 합니다.  
  
4. **AD FS 페더레이션 서버 프록시 구성 마법사**를 사용하여 원래 AD FS 프록시 구성을 만듭니다. 자세한 내용은 [컴퓨터 페더레이션 서버 프록시 역할에 대 한 구성](configure-a-computer-for-the-federation-server-proxy-role.md)합니다. 다음과 같이 마법사를 실행하면서 AD FS 2.0 페더레이션 서버 프록시 마이그레이션 준비에서 수집한 정보를 사용합니다.  
  
 
|**페더레이션 서버 프록시 마법사 입력 옵션**|**다음 값을 사용 합니다.**|
|-----|-----|  
|**페더레이션 서비스 이름**|proxyproperties.txt 파일의 BaseHostName 값을 입력합니다.|  
|**이 페더레이션 서비스에 요청을 보낼 때 HTTP 프록시 서버 사용** 확인란|proxyproperties.txt 파일에 ForwardProxyUrl 속성 값이 포함되어 있는 경우 이 확인란을 선택합니다.|  
|**HTTP 프록시 서버 주소**|proxyproperties.txt 파일의 ForwardProxyUrl 값을 입력합니다.|  
|자격 증명 프롬프트|AD FS 페더레이션 서버의 관리자 계정 또는 AD FS 페더레이션 서비스를 실행하는 서비스 계정의 자격 증명을 입력합니다.|  
  
5. 이 서버에서 AD FS 웹 페이지를 업데이트합니다. 마이그레이션을 위해 페더레이션 서버 프록시를 준비 하는 동안 사용자 지정 된 AD FS 프록시 웹 페이지를 백업한 경우 Windows Server 2012에 AD FS 프록시 구성의 결과로 백업 데이터를 사용 하 여 기본적으로 **%systemdrive%\inetpub\adfs\ls** 디렉터리에 생성 된 기본 AD FS 웹 페이지를 덮어씁니다.  
  
6. 이 서버를 부하 분산 장치에 다시 추가합니다.  
  
7. 마이그레이션할 다른 AD FS 2.0 페더레이션 서버 프록시가 있는 경우 나머지 페더레이션 서버 프록시 컴퓨터에 대해 2-6단계를 반복합니다.  
  
  
## <a name="next-steps"></a>다음 단계
 [AD FS 2.0 페더레이션 서버 마이그레이션 준비](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 페더레이션 서버 프록시  마이그레이션 준비](prepare-to-migrate-ad-fs-fed-proxy.md)  
 [AD FS 2.0 페더레이션 서버 마이그레이션](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 페더레이션 서버 프록시  마이그레이션](migrate-the-ad-fs-2-fed-server-proxy.md)  
 [AD FS 1.1 웹 에이전트 마이그레이션](migrate-the-ad-fs-web-agent.md)