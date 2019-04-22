---
ms.assetid: bbb84ea6-7e31-4442-85ab-a9447e7c19e8
title: 토큰 서명 인증서 추가
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 8a94e0724d6fd2a04e2fbfc22b3054b49d87f440
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826154"
---
# <a name="add-a-token-signing-certificate"></a>토큰 서명 인증서 추가

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Federation Services에서 페더레이션 서버 \(AD FS\) 토큰이 필요한\-공격자가 변경 하거나 무단으로 액세스 하기 위해 보안 토큰을 위조를 방지 하기 위해 인증서를 서명 합니다. 에 연결된 된 리소스입니다. 모든 토큰\-암호화 개인 키와 디지털 서명 하는 데 사용 되는 공개 키 포함 서명 인증서 \(개인 키를 사용 하 여\) 보안 토큰입니다. 나중에 이러한 키 파트너 페더레이션 서버에서 받으면 유효성을 검사 신뢰성 \(공개 키를 사용 하 여\) 암호화 된 보안 토큰입니다.  
  
> [!CAUTION]  
> 토큰에 사용 되는 인증서\-서명 하는 것은 페더레이션 서비스의 안정성에 중요 합니다. 손실 되거나 의도치 않게 제거가이 목적을 위해 구성 된 모든 인증서는 서비스 중단 될 수 있습니다, 때문에이 목적을 위해 구성 된 모든 인증서를 백업 해야 합니다.  
  
토큰\-서명 인증서가 페더레이션 서비스에서 신뢰할 수 있는 루트에 연결 해야 합니다. 다음 절차를 사용 하 여 토큰을 추가할\-AD FS 관리 스냅인에 서명 인증서\-에서 내보낸 된 파일에서입니다.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.microsoft.com\/fwlink\/? LinkId\=83477\)합니다.   
  
### <a name="to-add-a-token-signing-certificate"></a>토큰을 추가 하려면\-서명 인증서  
  
1.  에 **시작** 화면에서 입력**AD FS 관리**, 한 다음 ENTER를 누릅니다.  
  
2.  콘솔 트리에서 두 번\-클릭 **Service**를 클릭 하 고 **인증서**합니다.  
  
3.  에 **동작** 창 클릭 합니다 **토큰 추가\-서명 인증서** 링크.  
  
4.  에 **인증서 파일을 찾습니다** 대화 상자에서 추가 인증서 파일을 선택한 다음 클릭 하려는 인증서 파일을 이동 **오픈**합니다.  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: 페더레이션 서버 설정](Checklist--Setting-Up-a-Federation-Server.md)  
  
[페더레이션 서버에 대 한 인증서 요구 사항](https://technet.microsoft.com/library/dd807040.aspx)  
  

