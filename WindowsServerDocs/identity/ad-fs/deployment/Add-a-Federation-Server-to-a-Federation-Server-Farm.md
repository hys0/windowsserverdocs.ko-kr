---
ms.assetid: 6ecf8d85-cd61-4c87-add8-00a679a6e3ff
title: 페더레이션 서버 팜에 페더레이션 서버 추가
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 57c59241c36ba4ed657b83e7c691931f57978a7c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408521"
---
# <a name="add-a-federation-server-to-a-federation-server-farm"></a>페더레이션 서버 팜에 페더레이션 서버 추가


페더레이션 서비스 역할 서비스를 설치 하 고 컴퓨터에 필요한 인증서를 구성 하 고 나면 컴퓨터가 페더레이션 서버가 되도록 구성할 준비가 된 것입니다. 다음 절차를 사용하여 새 페더레이션 서버 팜에 컴퓨터를 가입시킬 수 있습니다.  
  
AD FS 페더레이션 서버 구성 마법사를 사용 하 여 컴퓨터를 팜에 가입 시킬 수 있습니다. 이 마법사를 사용 하 여 컴퓨터를 기존 팜에 연결 하는 경우 컴퓨터는 AD FS 구성 데이터베이스의 읽기\-만 복사본으로 구성 되며 기본 페더레이션 서버에서 업데이트를 받아야 합니다.  
  
> [!NOTE]  
> \(SSO\) 디자인에서 페더레이션된 웹 Single\-Sign\-의 경우 계정 파트너 조직에 하나 이상의 페더레이션 서버가 있어야 하 고 리소스 파트너 조직의 페더레이션 서버는 하나 이상 있어야 합니다. 자세한 내용은 [Where to Place a Federation Server](https://technet.microsoft.com/library/dd807127.aspx)를 참조하세요.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) 에서 적절 한 계정 및 그룹 구성원 자격 사용에 대 한 세부 정보를 검토 \(http:\/\/go.microsoft.com\/fwlink\/? LinkId\=83477\).   
  
### <a name="to-add-a-federation-server-to-a-federation-server-farm"></a>페더레이션 서버 팜에 페더레이션 서버를 추가 하려면  
  
1.  AD FS 페더레이션 서버 구성 마법사를 시작 하는 방법에는 두 가지가 있습니다. 마법사를 시작하려면 다음 중 하나를 수행합니다.  
  
    -   페더레이션 서비스 역할 서비스 설치가 완료 되 면에서 AD FS 관리 스냅인\-열고 **개요** 페이지 또는 **작업** 창에서 **페더레이션 서버 구성 마법사 AD FS** 링크를 클릭 합니다.  
  
    -   설치 마법사가 완료 되 면 언제 든 지 Windows 탐색기를 열고 **C:\\windows\\ADFS** 폴더로 이동한 다음 **fsconfigwizard .exe**를 두 번 클릭\-합니다.  
  
2.  **시작** 페이지에서 **Add a federation server to an existing Federation Service(기존 페더레이션 서비스에 페더레이션 서버 추가)** 가 선택되어 있는지 확인하고 **다음**을 클릭합니다.  
  
3.  선택한 AD FS 데이터베이스가 이미 있는 경우 **기존 AD FS 구성 데이터베이스 검색 됨** 페이지가 나타납니다. 이 경우 **데이터베이스 삭제**를 클릭한 후 **다음**을 클릭합니다.  
  
    > [!CAUTION]  
    > 이 AD FS 데이터베이스의 데이터가 중요 하지 않거나 프로덕션 페더레이션 서버 팜에서 사용 되지 않는 경우에만이 옵션을 선택 하십시오.  
  
4.  **Specify the Primary Federation Server and Service Account(기본 페더레이션 서버 및 서비스 계정 지정)** 페이지의 **Primary federation server name(기본 페더레이션 서버 이름)** 에서 팜에 있는 기본 페더레이션 서버의 컴퓨터 이름을 입력하고 **찾아보기**를 클릭합니다. **찾아보기** 대화 상자에서 기존 페더레이션 서버 팜의 다른 모든 페더레이션 서버에서 서비스 계정으로 사용하는 도메인 계정을 찾은 다음 **확인**을 클릭합니다. 암호를 입력 하 고 확인 한 후 **다음**을 클릭 합니다.  
  
    > [!NOTE]  
    > 페더레이션 서버 팜의 서비스 계정을 지정 하는 방법에 대 한 자세한 내용은 [수동으로 페더레이션 서버 팜에 대 한 서비스 계정 구성](Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md)을 참조 하세요. 페더레이션 서버 팜의 각 페더레이션 서버는 작동 하는 팜에 대해 동일한 서비스 계정을 지정 해야 합니다. 예를 들어 만든 서비스 계정이 contoso\\ADFS2SVC 일 경우 페더레이션 서버 구성 마법사의이 단계에서 페더레이션 서버 역할에 대해 구성 하 고 동일한 팜에 참여 하는 각 컴퓨터는 팜을 작동 하기 위해 페더레이션 서버 구성 마법사의이 단계에서 contoso\\ADFS2SVC를 지정 해야 합니다.  
  
5.  **설정 적용 준비 완료** 페이지에서 세부 정보를 검토합니다. 설정이 올바르면 **다음** 을 클릭 하 여 이러한 설정으로 AD FS 구성을 시작 합니다.  
  
6.  **구성 결과** 페이지에서 결과를 검토합니다. 모든 구성 단계가 완료되면 **닫기**  를 클릭하여 마법사를 종료합니다.  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: 페더레이션 서버 설정](Checklist--Setting-Up-a-Federation-Server.md)  
  

