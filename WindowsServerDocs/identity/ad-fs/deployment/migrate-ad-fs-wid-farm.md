---
title: AD FS 2.0 페더레이션 서버 WID 팜 마이그레이션
description: AD FS 2.0 서버 WID 팜을 Windows Server 2012로 마이그레이션하는 방법에 대 한 정보를 제공 합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 89da3de4bc626e12a1fc34752841f2de1afb5322
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408249"
---
# <a name="migrate-an-ad-fs-20-wid-farm"></a>AD FS 2.0 WID 팜 마이그레이션  
이 문서에서는 AD FS 2.0 WID (Windows 내부 데이터베이스) 팜을 Windows Server 2012로 마이그레이션하는 방법에 대 한 자세한 정보를 제공 합니다.

## <a name="migrate-an-ad-fs-wid-farm"></a>AD FS WID 팜 마이그레이션
WID 팜을 Windows Server 2012로 마이그레이션하려면 다음 절차를 수행 합니다.  
  
1.  WID 팜의 모든 노드 (서버)에 대해 [wid 팜 마이그레이션 준비](prepare-to-migrate-a-wid-farm.md)의 절차를 검토 하 고 수행 합니다.  
  
2.  부하 분산 장치에서 기본이 아닌 노드를 모두 제거합니다.  
  
3.  이 서버의 운영 체제를 Windows Server 2008 R2 또는 Windows Server 2008에서 Windows server 2012로 업그레이드 합니다. 자세한 내용은 [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx)를 참조하세요.  
  
> [!IMPORTANT]
>  운영 체제 업그레이드로 인해 이 서버의 AD FS 구성이 손실되고 AD FS 2.0 서버 역할이 제거됩니다. Windows Server 2012 AD FS 서버 역할이 대신 설치 되지만 구성 되지 않습니다. 원래 AD FS 구성을 만들고 나머지 AD FS 설정을 복원하여 페더레이션 서버 마이그레이션을 완료해야 합니다.  
  
4. 이 서버에서 원래 AD FS 구성을 만듭니다.  
  
**AD FS 페더레이션 서버 구성 마법사** 를 사용하여 원래 AD FS 구성을 만들어 페더레이션 서버를 WID 팜에 추가할 수 있습니다. 자세한 내용은 [페더레이션 서버 팜에 페더레이션 서버 추가](add-a-federation-server-to-a-federation-server-farm.md)를 참조하세요.  
  
> [!NOTE]
> **AD FS 페더레이션 서버 구성 마법사** 의 **기본 페더레이션 서버 및 서비스 계정 지정**페이지가 나타나면 WID 팜의 기본 페더레이션 서버 이름을 입력하고, AD FS 마이그레이션을 준비하는 동안 기록한 서비스 계정 정보를 입력해야 합니다. 자세한 내용은 [AD FS 2.0 WID 팜 마이그레이션 준비](prepare-to-migrate-a-wid-farm.md)합니다. 
>  
> 도달 하면 합니다 **페더레이션 서비스 이름 지정** 페이지에 "준비" WID 팜 마이그레이션에 기록한 SSL 인증서를 선택 해야 합니다 [AD FS 2.0 WID 팜 마이그레이션 준비](prepare-to-migrate-a-wid-farm.md).  
  
5. 이 서버에서 AD FS 웹 페이지를 업데이트합니다. 마이그레이션을 준비 하는 동안 사용자 지정 된 AD FS 웹 페이지를 백업한 경우 Windows Server 2012의 AD FS 구성으로 인해 기본적으로 **%systemdrive%\inetpub\adfs\ls** 디렉터리에 생성 된 기본 AD FS 웹 페이지를 덮어쓰도록 백업 데이터를 사용 해야 합니다.  
  
6. 방금 Windows Server 2012로 업그레이드 한 서버를 부하 분산 장치에 추가 합니다.  
  
7. WID 팜의 나머지 보조 서버에 대해 1~6단계를 반복합니다.  
  
8. 업그레이드된 보조 서버 중 하나를 WID 팜의 기본 서버로 수준을 올립니다. 이렇게 하려면 Windows PowerShell을 열고 `PSH:> Set-AdfsSyncProperties –Role PrimaryComputer`명령을 실행합니다.  
  
9. 부하 분산 장치에서 WID 팜의 원래 기본 서버를 제거합니다.  
  
10. Windows PowerShell을 사용하여 WID 팜의 원래 기본 서버를 보조 서버로 수준을 내립니다. Windows PowerShell을 열고 `PSH:>add-pssnapin “Microsoft.adfs.powershell”`명령을 실행하여 Windows PowerShell 세션에 AD FS cmdlet을 추가합니다. 그런 다음 원래 기본 서버 수준을 보조 서버로 내리려면 다음 명령을 실행합니다. `PSH:> Set-AdfsSyncProperties – Role SecondaryComputer –PrimaryComputerName <FQDN of the Primary Federation Server>`.  
  
11. WID 팜의이 마지막 노드 (서버)에 있는 운영 체제를 Windows Server 2008 R2 또는 Windows server 2008에서 Windows server 2012로 업그레이드 합니다. 자세한 내용은 [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx)를 참조하세요.  
  
> [!IMPORTANT]
>  운영 체제 업그레이드로 인해 이 서버의 AD FS 구성이 손실되고 AD FS 2.0 서버 역할이 제거됩니다. Windows Server 2012 AD FS 서버 역할이 대신 설치 되지만 구성 되지 않습니다. 수동으로 원래 AD FS 구성을 만들고 나머지 AD FS 설정을 복원하여 페더레이션 서버 마이그레이션을 완료해야 합니다.  
  
12. WID 팜의 이 마지막 노드(서버)에서 원래 AD FS 구성을 만듭니다.  
  
**AD FS 페더레이션 서버 구성 마법사** 를 사용하여 원래 AD FS 구성을 만들어 페더레이션 서버를 WID 팜에 추가할 수 있습니다. 자세한 내용은 [페더레이션 서버 팜에 페더레이션 서버 추가](add-a-federation-server-to-a-federation-server-farm.md)를 참조하세요.  
  
> [!NOTE]
> **AD FS 페더레이션 서버 구성 마법사** 의 **기본 페더레이션 서버 및 서비스 계정 지정**페이지가 나타나면 AD FS 마이그레이션을 준비하는 동안 기록한 서비스 계정 정보를 입력합니다. 자세한 내용은 [AD FS 2.0 WID 팜 마이그레이션 준비](prepare-to-migrate-a-wid-farm.md)합니다. 
>  
> 도달 하면 합니다 **페더레이션 서비스 이름 지정** 페이지에서 기록한 SSL 인증서를 선택 해야 합니다 [AD FS 2.0 WID 팜 마이그레이션 준비](prepare-to-migrate-a-wid-farm.md)합니다.  
  
13. WID 팜의 이 마지막 서버에서 AD FS 웹 페이지를 업데이트합니다. 마이그레이션을 준비 하는 동안 사용자 지정 된 AD FS 웹 페이지를 백업한 경우 Windows Server 2012에 대 한 AD FS 구성의 결과로, 기본적으로 **%systemdrive%\inetpub\adfs\ls** 디렉터리에 생성 된 기본 AD FS 웹 페이지를 백업 데이터를 사용 하 여 덮어씁니다.  
  
14. 방금 Windows Server 2012로 업그레이드 한 WID 팜의이 마지막 서버를 부하 분산 장치에 추가 합니다.  
  
15. 사용자 지정 특성 저장소와 같은 나머지 AD FS 사용자 지정 항목을 복원합니다.  
  
## <a name="next-steps"></a>다음 단계
 [AD FS 2.0 페더레이션 서버 마이그레이션 준비](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 페더레이션 서버 프록시  마이그레이션 준비](prepare-to-migrate-ad-fs-fed-proxy.md)  
 [AD FS 2.0 페더레이션 서버 마이그레이션](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 페더레이션 서버 프록시  마이그레이션](migrate-the-ad-fs-2-fed-server-proxy.md)  
 [AD FS 1.1 웹 에이전트 마이그레이션](migrate-the-ad-fs-web-agent.md)