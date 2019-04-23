---
title: AD FS 2.0 페더레이션 서버 WID 팜 마이그레이션
description: Windows Server 2012로 AD FS 2.0 서버 WID 팜을 마이그레이션하는 방법에 정보를 제공 합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: dbef7d07041a1fd32656c95947d5202b566c068a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868324"
---
# <a name="migrate-an-ad-fs-20-wid-farm"></a>AD FS 2.0 WID 팜 마이그레이션  
이 문서는 AD 마이그레이션하는 방법에 자세한 정보를 제공 FS 2.0 Windows 내부 데이터베이스 WID () 팜을 Windows Server 2012.

## <a name="migrate-an-ad-fs-wid-farm"></a>AD FS WID 팜 마이그레이션
WID 팜 Windows Server 2012로 마이그레이션하려면 다음 절차를 수행 합니다.  
  
1.  모든 노드 (서버)에 대해 WID 팜의 검토 하 고의 절차를 수행 [WID 팜 마이그레이션 준비](prepare-to-migrate-a-wid-farm.md)합니다.  
  
2.  부하 분산 장치에서 기본이 아닌 노드를 모두 제거합니다.  
  
3.  Windows Server 2008 R2에서이 서버 또는 Windows Server 2012에 Windows Server 2008의 운영 체제를 업그레이드 합니다. 자세한 내용은 [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx)를 참조하세요.  
  
> [!IMPORTANT]
>  운영 체제 업그레이드로 인해 이 서버의 AD FS 구성이 손실되고 AD FS 2.0 서버 역할이 제거됩니다. Windows Server 2012 AD FS 서버 역할 대신 설치 되지만 구성 되지는 않습니다. 원래 AD FS 구성을 만들고 나머지 AD FS 설정을 복원하여 페더레이션 서버 마이그레이션을 완료해야 합니다.  
  
4.  이 서버에서 원래 AD FS 구성을 만듭니다.  
  
**AD FS 페더레이션 서버 구성 마법사** 를 사용하여 원래 AD FS 구성을 만들어 페더레이션 서버를 WID 팜에 추가할 수 있습니다. 자세한 내용은 [페더레이션 서버 팜에 페더레이션 서버 추가](add-a-federation-server-to-a-federation-server-farm.md)를 참조하세요.  
  
> [!NOTE]
> **AD FS 페더레이션 서버 구성 마법사** 의 **기본 페더레이션 서버 및 서비스 계정 지정**페이지가 나타나면 WID 팜의 기본 페더레이션 서버 이름을 입력하고, AD FS 마이그레이션을 준비하는 동안 기록한 서비스 계정 정보를 입력해야 합니다. 자세한 내용은 [Prepare to Migrate the AD FS 2.0 Federation Server](prepare-to-migrate-a-wid-farm.md)합니다. 
>  
> 도달 하면 합니다 **페더레이션 서비스 이름 지정** 페이지에 "준비" WID 팜 마이그레이션에 기록한 SSL 인증서를 선택 해야 합니다 [Prepare to Migrate the AD FS 2.0 Federation Server](prepare-to-migrate-a-wid-farm.md).  
  
5.  이 서버에서 AD FS 웹 페이지를 업데이트합니다. 마이그레이션을 준비 하는 동안 사용자 지정된 AD FS 웹 페이지를 백업한 경우 덮어쓰려면 기본 AD FS 웹 페이지에서 기본적으로 생성 된 백업 데이터를 사용 하도록 해야 합니다 **%systemdrive%\inetpub\adfs\ls** 으로 디렉터리 Windows Server 2012에서 AD FS 구성의 결과입니다.  
  
6.  방금 업그레이드 Windows Server 2012로 부하 분산 장치는 서버를 추가 합니다.  
  
7.  WID 팜의 나머지 보조 서버에 대해 1~6단계를 반복합니다.  
  
8.  업그레이드된 보조 서버 중 하나를 WID 팜의 기본 서버로 수준을 올립니다. 이렇게 하려면 Windows PowerShell을 열고 `PSH:> Set-AdfsSyncProperties –Role PrimaryComputer`명령을 실행합니다.  
  
9. 부하 분산 장치에서 WID 팜의 원래 기본 서버를 제거합니다.  
  
10. Windows PowerShell을 사용하여 WID 팜의 원래 기본 서버를 보조 서버로 수준을 내립니다. Windows PowerShell을 열고 `PSH:>add-pssnapin “Microsoft.adfs.powershell”`명령을 실행하여 Windows PowerShell 세션에 AD FS cmdlet을 추가합니다. 그런 다음 원래 기본 서버 수준을 보조 서버로 내리려면 다음 명령을 실행합니다. `PSH:> Set-AdfsSyncProperties – Role SecondaryComputer –PrimaryComputerName <FQDN of the Primary Federation Server>`.  
  
11. Windows Server 2012에 Windows Server 2008 R2 또는 Windows Server 2008에서 WID 팜의이 마지막 노드 (서버)의 운영 체제를 업그레이드 합니다. 자세한 내용은 [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx)를 참조하세요.  
  
> [!IMPORTANT]
>  운영 체제 업그레이드로 인해 이 서버의 AD FS 구성이 손실되고 AD FS 2.0 서버 역할이 제거됩니다. Windows Server 2012 AD FS 서버 역할 대신 설치 되지만 구성 되지는 않습니다. 수동으로 원래 AD FS 구성을 만들고 나머지 AD FS 설정을 복원하여 페더레이션 서버 마이그레이션을 완료해야 합니다.  
  
12. WID 팜의 이 마지막 노드(서버)에서 원래 AD FS 구성을 만듭니다.  
  
**AD FS 페더레이션 서버 구성 마법사** 를 사용하여 원래 AD FS 구성을 만들어 페더레이션 서버를 WID 팜에 추가할 수 있습니다. 자세한 내용은 [페더레이션 서버 팜에 페더레이션 서버 추가](add-a-federation-server-to-a-federation-server-farm.md)를 참조하세요.  
  
> [!NOTE]
> **AD FS 페더레이션 서버 구성 마법사** 의 **기본 페더레이션 서버 및 서비스 계정 지정**페이지가 나타나면 AD FS 마이그레이션을 준비하는 동안 기록한 서비스 계정 정보를 입력합니다. 자세한 내용은 [Prepare to Migrate the AD FS 2.0 Federation Server](prepare-to-migrate-a-wid-farm.md)합니다. 
>  
> 도달 하면 합니다 **페더레이션 서비스 이름 지정** 페이지에서 기록한 SSL 인증서를 선택 해야 합니다 [Prepare to Migrate the AD FS 2.0 Federation Server](prepare-to-migrate-a-wid-farm.md)합니다.  
  
13. WID 팜의 이 마지막 서버에서 AD FS 웹 페이지를 업데이트합니다. 마이그레이션을 준비 하는 동안 사용자 지정된 AD FS 웹 페이지를 백업한 경우 덮어쓰려면 기본 AD FS 웹 페이지에서 기본적으로 생성 된 백업 데이터를 사용 합니다 **%systemdrive%\inetpub\adfs\ls** 의 결과로 디렉터리 Windows Server 2012에서 AD FS 구성 합니다.  
  
14. 방금 업그레이드 Windows Server 2012로 부하 분산 장치를 WID 팜의이 마지막 서버를 추가 합니다.  
  
15. 사용자 지정 특성 저장소와 같은 나머지 AD FS 사용자 지정 항목을 복원합니다.  
  
## <a name="next-steps"></a>다음 단계
 [AD FS 2.0 페더레이션 서버 마이그레이션 준비](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 페더레이션 서버 프록시 마이그레이션 준비](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 페더레이션 서버 마이그레이션](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 페더레이션 서버 프록시 마이그레이션](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [AD FS 1.1 웹 에이전트 마이그레이션](migrate-the-ad-fs-web-agent.md)