---
ms.assetid: bbb84ea6-7e31-4442-85ab-a9447e7c19e8
title: "토큰 서명 인증서를 추가 합니다."
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 8a94e0724d6fd2a04e2fbfc22b3054b49d87f440
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="add-a-token-signing-certificate"></a>토큰 서명 인증서를 추가 합니다.

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Federation 서버 Active Directory Federation Services \(AD FS\)에 변경 하거나 보안 토큰 연합된 리소스에는 무단 액세스 하기 위해에서 위조 악의적인 token\ 서명 인증서 필요 합니다. 모든 token\ 서명 인증서 개인 암호화 키와에 디지털 서명 하는 데 사용 되는 공개 키를 포함 \ (개인 key\)을 통해 보안 토큰 합니다. 나중에 이러한 키 파트너 federation 서버를 받은 후 자녀가 신뢰성을 확인 \ (공개 key\)를 통해 암호화 보안 토큰 합니다.  
  
> [!CAUTION]  
> Token\ 로그인에 사용 되는 인증서를 중요 하며, Federation 서비스의 안정성을 개선 합니다. 손실이 나이 위해 구성 된 인증서를 예상치 못한 제거 서비스가 중단 될 수 있습니다을 하기 때문에이 위해 구성 된 인증서를 백업 해야 합니다.  
  
Token\ 서명 인증서가 신뢰할 수 있는 루트 Federation 서비스에 연결 해야 합니다. 내보낸 하는 파일에서 token\ 서명 인증서 snap\에서 AD FS 관리를 추가 하려면 다음 절차에 사용할 수 있습니다.  
  
회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) \ (http:///\/ go.microsoft.com\/fwlink\/있나요? LinkId\ 83477\ =).   
  
### <a name="to-add-a-token-signing-certificate"></a>Token\ 서명 인증서를 추가 하려면  
  
1.  에 **시작** 화면에서 입력**AD FS 관리**, ENTER 키를 누릅니다.  
  
2.  콘솔 트리에서 double\ 클릭 **서비스**을 차례로 클릭 하 고 **인증서**합니다.  
  
3.  에 **작업** 창 클릭는 **추가 Token\ 서명 인증서** 링크입니다.  
  
4.  에 **인증서 파일 찾아보기** 대화 상자에 추가 인증서 파일을 선택한 다음 원하는 인증서 파일을 찾아 **열기**합니다.  
  
## <a name="additional-references"></a>추가 참조  
[Federation 서버 설정 검사:](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Federation 서버의 인증서 요구 사항](https://technet.microsoft.com/library/dd807040.aspx)  
  

