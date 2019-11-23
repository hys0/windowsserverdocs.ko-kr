---
ms.assetid: bbb84ea6-7e31-4442-85ab-a9447e7c19e8
title: 토큰 서명 인증서 추가
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: c8b2246842dd70c06442faed995f6b883dbaf70a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71360090"
---
# <a name="add-a-token-signing-certificate"></a>토큰 서명 인증서 추가


Active Directory Federation Services \(\) AD FS의 페더레이션 서버는 페더레이션 리소스에 대 한 무단 액세스를 얻기 위해 공격자가 보안 토큰을 변경 하거나 위조 하지 못하도록 토큰\-서명 인증서를 요구 합니다. 모든 토큰\-암호화 프라이빗 키와 디지털 서명하는 데 사용되는 공개 키 포함 서명 인증서 \(프라이빗 키를 사용하여\) 보안 토큰입니다. 나중에 파트너 페더레이션 서버에서 이러한 키를 받은 후 암호화 된 보안 토큰의 공개 키\)를 통해 \(신뢰성의 유효성을 검사 합니다.  
  
> [!CAUTION]  
> 토큰\-서명에 사용 되는 인증서는 페더레이션 서비스 안정성에 매우 중요 합니다. 이 용도로 구성 된 인증서의 손실 또는 계획 되지 않은 제거는 서비스를 방해할 수 있으므로이 목적을 위해 구성 된 모든 인증서를 백업 해야 합니다.  
  
토큰\-서명 인증서가 페더레이션 서비스의 신뢰할 수 있는 루트에 연결 되어야 합니다. 다음 절차를 사용 하 여 서명 인증서\-토큰을에서 내보낸 파일의 AD FS 관리 스냅인\-에 추가할 수 있습니다.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) 에서 적절 한 계정 및 그룹 구성원 자격 사용에 대 한 세부 정보를 검토 \(http:\/\/go.microsoft.com\/fwlink\/? LinkId\=83477\).   
  
### <a name="to-add-a-token-signing-certificate"></a>서명 인증서\-토큰을 추가 하려면  
  
1.  **시작** 화면에서**AD FS 관리**를 입력 한 다음 enter 키를 누릅니다.  
  
2.  콘솔 트리에서 **서비스**를 두 번 클릭 한 다음 **인증서**를 클릭\-합니다.  
  
3.  **작업** 창에서 **토큰\-서명 인증서 추가** 링크를 클릭 합니다.  
  
4.  **인증서 파일 찾아보기** 대화 상자에서 추가 하려는 인증서 파일로 이동 하 여 인증서 파일을 선택한 다음 **열기**를 클릭 합니다.  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: 페더레이션 서버 설정](Checklist--Setting-Up-a-Federation-Server.md)  
  
[페더레이션 서버에 대한 인증서 요구 사항](https://technet.microsoft.com/library/dd807040.aspx)  
  

