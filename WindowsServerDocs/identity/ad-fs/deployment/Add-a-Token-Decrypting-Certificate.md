---
ms.assetid: 27e1e299-0beb-4e86-8143-1ba031dc3502
title: 토큰 암호 해독 인증서 추가
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 388414fff97705901bf52ee844b90508d62f8c83
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408455"
---
# <a name="add-a-token-decrypting-certificate"></a>토큰 암호 해독 인증서 추가

페더레이션 서버는 새 인증서가 기본 암호 해독 인증서로 설정 된 후 신뢰 당사자 페더레이션 서버에서 이전 인증서를 사용 하 여 발급 된 토큰의 암호를 해독 해야 하는 경우 토큰\-암호 해독 인증서를 사용 합니다. Active Directory Federation Services \(AD FS\) SSL(Secure Sockets Layer) \(\) SSL 인터넷 정보 서비스 인증서를 기본 암호 해독 인증서로 사용 합니다.\(\)  
  
> [!CAUTION]  
> 토큰\-암호 해독에 사용 되는 인증서는 페더레이션 서비스 안정성에 매우 중요 합니다. 이 용도로 구성 된 인증서의 손실 또는 계획 되지 않은 제거는 서비스를 방해할 수 있으므로이 목적을 위해 구성 된 모든 인증서를 백업 해야 합니다.  
  
다음 절차를 사용 하 여 사용자가 내보낸 파일에서의 AD FS 관리 스냅인\-인증서를 암호 해독\-토큰을 추가할 수 있습니다.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) 에서 적절 한 계정 및 그룹 구성원 자격 사용에 대 한 세부 정보를 검토 \(http:\/\/go.microsoft.com\/fwlink\/? LinkId\=83477\).   
  
### <a name="to-add-a-token-decrypting-certificate"></a>인증서를 암호 해독\-토큰을 추가 하려면  
  
1.  **시작** 화면에서**AD FS 관리**를 입력 한 다음 enter 키를 누릅니다.  
  
2.  콘솔 트리에서 **서비스**를 두 번 클릭 한 다음 **인증서**를 클릭\-합니다.  
  
3.  **작업** 창에서 **토큰 추가\-인증서 암호 해독** 링크를 클릭 합니다.  
  
4.  **인증서 파일 찾아보기** 대화 상자에서 추가 하려는 인증서 파일로 이동 하 여 인증서 파일을 선택한 다음 **열기**를 클릭 합니다.  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: 페더레이션 서버 설정](Checklist--Setting-Up-a-Federation-Server.md)  
  
[페더레이션 서버에 대한 인증서 요구 사항](https://technet.microsoft.com/library/dd807040.aspx)  
  

