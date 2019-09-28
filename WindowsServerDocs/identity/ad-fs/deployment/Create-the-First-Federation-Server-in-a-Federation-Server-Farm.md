---
ms.assetid: 5e334c4e-75a7-453c-83e8-5ab4243cc685
title: 페더레이션 서버 팜의 첫 번째 페더레이션 서버 만들기
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 09b577ddcf722c6eac17ea145f29f9583d1cdb00
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408424"
---
# <a name="create-the-first-federation-server-in-a-federation-server-farm"></a>페더레이션 서버 팜의 첫 번째 페더레이션 서버 만들기

페더레이션 서비스 역할 서비스를 설치 하 고 컴퓨터에 필요한 인증서를 구성 하 고 나면 컴퓨터가 페더레이션 서버가 되도록 구성할 준비가 된 것입니다. 다음 절차에 따라 AD FS 페더레이션 서버 구성 마법사를 사용 하 여 새 페더레이션 서버 팜의 첫 번째 페더레이션 서버로 사용할 컴퓨터를 설정할 수 있습니다.  
  
팜의 첫 번째 페더레이션 서버를 만들면 새 페더레이션 서비스도 만들어지며 이 컴퓨터가 기본 페더레이션 서버로 설정됩니다. 즉,이 컴퓨터는 AD FS 구성 데이터베이스의 읽기 @ no__t-0write 복사본으로 구성 됩니다. 이 팜의 다른 모든 페더레이션 서버는 기본 페더레이션 서버에 적용 된 모든 변경 내용을 로컬로 저장 되는 AD FS 구성 데이터베이스의 읽기 전용 복사본에 복제 해야 합니다. 이 복제 프로세스에 대한 자세한 내용은 [AD FS 구성 데이터베이스의 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)을 참조하세요.  
  
> [!NOTE]  
> 페더레이션된 웹 Single @ no__t-0Sign @ no__t On \(SSO @ no__t 디자인의 경우 계정 파트너 조직에 하나 이상의 페더레이션 서버가 있어야 하 고 리소스 파트너 조직의 페더레이션 서버는 하나 이상 있어야 합니다. 자세한 내용은 [Where to Place a Federation Server](https://technet.microsoft.com/library/dd807127.aspx)를 참조하세요.  
  
이 절차를 완료하기 위해서는 최소한 Domain Admins의 구성원 자격이 있거나 Active Directory의 프로그램 데이터 컨테이너에 대한 쓰기 권한이 부여된 위임된 도메인 계정이 있어야 합니다.  
  
### <a name="to-create-the-first-federation-server-in-a-federation-server-farm"></a>페더레이션 서버 팜의 첫 번째 페더레이션 서버를 만들려면  
  
1.  AD FS 페더레이션 서버 구성 마법사를 시작 하는 방법에는 두 가지가 있습니다. 마법사를 시작하려면 다음 중 하나를 수행합니다.  
  
    -   페더레이션 서비스 역할 서비스 설치가 완료 되 면 AD FS Management snap @ no__t-0in을 열고 **개요** 페이지 또는 **작업** 창에서 **AD FS 페더레이션 서버 구성 마법사** 링크를 클릭 합니다.  
  
    -   설치 마법사가 완료 된 후 언제 든 지 Windows 탐색기를 열고 **C: \\Windows @ no__t-2ADFS** 폴더로 이동한 다음 두 번째 @ no__t를 클릭 하 여 **fsconfigwizard**를 클릭 합니다.  
  
2.  **시작** 페이지에서 **새 페더레이션 서비스 만들기** 가 선택되어 있는지 확인하고 **다음**을 클릭합니다.  
  
3.  **Select 독립형 @ no__t-1alone 팜 배포** 페이지에서 **새 페더레이션 서버 팜**을 클릭 한 후 **다음**을 클릭 합니다.  
  
4.  **페더레이션 서비스 이름 지정** 페이지에서 표시된 **SSL 인증서**가 올바른지 확인합니다. 올바른 인증서가 아닌 경우 **SSL 인증서** 목록에서 적절한 인증서를 선택합니다.  
  
    이 인증서는 기본 웹 사이트에 대 한 SSL(Secure Sockets Layer) \(SSL @ no__t-1 설정에서 생성 됩니다. 기본 웹 사이트에 SSL 인증서가 하나만 구성되어 있는 경우 해당 인증서가 표시되고 사용하도록 자동으로 선택됩니다. 기본 웹 사이트에 대해 구성된 SSL 인증서가 여러 개인 경우 해당 인증서가 여기에 모두 나열되므로 그 중에서 선택해야 합니다. 기본 웹 사이트에 대해 구성된 SSL 설정이 없는 경우 로컬 컴퓨터의 개인 인증서 저장소에서 사용할 수 있는 인증서에서 목록이 생성됩니다.  
  
    > [!NOTE]  
    > IIS에 대해 SSL 인증서가 구성된 경우 마법사에서는 인증서를 재정의할 수 없습니다. 따라서 SSL 인증서에 대한 이전의 의도된 모든 IIS 구성이 유지됩니다. 이 제한을 해결하려면 IIS 관리 콘솔을 사용하여 인증서를 제거하거나 수동으로 다시 구성하면 됩니다.  
  
5.  선택한 AD FS 데이터베이스가 이미 있는 경우 **기존 AD FS 구성 데이터베이스 검색 됨** 페이지가 나타납니다. 이 페이지가 표시되면 **데이터베이스 삭제**를 클릭한 후 **다음**을 클릭합니다.  
  
    > [!CAUTION]  
    > 이 AD FS 데이터베이스의 데이터가 중요 하지 않거나 프로덕션 페더레이션 서버 팜에서 사용 되지 않는 경우에만이 옵션을 선택 하십시오.  
  
6.  **서비스 계정을 지정** 페이지에서 **찾아보기**를 클릭합니다. **찾아보기** 대화 상자에서 이 새 페더레이션 서버 팜에서 서비스 계정으로 사용할 도메인 계정을 찾은 후 **확인**을 클릭합니다. 이 계정의 암호를 입력하고 확인한 후 **다음**을 클릭합니다.  
  
    > [!NOTE]  
    > 페더레이션 서버 팜의 서비스 계정을 지정 하는 방법에 대 한 자세한 내용은 [수동으로 페더레이션 서버 팜에 대 한 서비스 계정 구성](Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md) 을 참조 하세요. 페더레이션 서버 팜의 각 페더레이션 서버는 작동 하는 팜에 대해 동일한 서비스 계정을 지정 해야 합니다. 예를 들어 만든 서비스 계정이 contoso @ no__t-0ADFS2SVC 인 경우 페더레이션 서버 역할에 대해 구성 하 고 동일한 팜에 참여 하는 각 컴퓨터는 페더레이션 서버에서이 단계에서 contoso @ no__t-1ADFS2SVC를 지정 해야 합니다. 팜을 운영할 구성 마법사입니다.  
  
7.  **설정 적용 준비 완료** 페이지에서 세부 정보를 검토합니다. 설정이 올바르면 **다음** 을 클릭 하 여 이러한 설정으로 AD FS 구성을 시작 합니다.  
  
8.  **구성 결과** 페이지에서 결과를 검토합니다. 모든 구성 단계가 완료되면 **닫기**  를 클릭하여 마법사를 종료합니다.  
  
    > [!IMPORTANT]  
    > 안전한 배포를 위해 AD FS 페더레이션 서버 구성 마법사를 사용하여 페더레이션 서버 팜을 구성할 때는 아티팩트 확인 및 회신 검색을 사용할 수 없습니다. 이 마법사는 서비스 구성 데이터를 저장하는 Windows 내부 데이터베이스를 자동으로 구성합니다. 그러나 AD FS Management snap @ no__t-1in의 **끝점** 노드 또는 Windows PowerShell의 Enable @ No__t-2ADFSEndpoint cmdlet을 사용 하 여 아티팩트 확인 끝점을 사용 하도록 설정 하 여이 변경 내용을 실수로 취소할 수도 있습니다. 따라서 페더레이션 서버 팜과 Windows 내부 데이터베이스를 함께 사용할 때는 이 끝점이 사용되지 않는 상태로 유지되도록 기본 설정을 다시 구성하지 않아야 합니다.  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: 페더레이션 서버 설정](Checklist--Setting-Up-a-Federation-Server.md)  
  

