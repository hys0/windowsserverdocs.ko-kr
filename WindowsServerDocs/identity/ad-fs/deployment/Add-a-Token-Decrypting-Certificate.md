---
ms.assetid: 27e1e299-0beb-4e86-8143-1ba031dc3502
title: 토큰 암호 해독 인증서 추가
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 0eba51521e7ef88542bccf93d92d2e783d800b5e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842214"
---
# <a name="add-a-token-decrypting-certificate"></a>토큰 암호 해독 인증서 추가

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

토큰을 사용 하는 페더레이션 서버\-암호 해독 인증서 신뢰 당사자 페더레이션 서버를 새 인증서를 기본 암호 해독 인증서로 설정 되 면 이전 인증서를 사용 하 여 발급 된 토큰의 암호를 해독 해야 합니다. Active Directory Federation Services \(AD FS\) Secure Sockets Layer를 사용 하 여 \(SSL\) 인터넷 정보 서비스에 대 한 인증서 \(IIS\) 기본 암호 해독을 인증서입니다.  
  
> [!CAUTION]  
> 토큰에 사용 되는 인증서\-암호를 해독 하는 것은 페더레이션 서비스의 안정성에 중요 합니다. 손실 되거나 의도치 않게 제거가이 목적을 위해 구성 된 모든 인증서는 서비스 중단 될 수 있습니다, 때문에이 목적을 위해 구성 된 모든 인증서를 백업 해야 합니다.  
  
다음 절차를 사용 하 여 토큰을 추가할\-AD FS 관리 스냅인에는 인증서를 암호 해독\-에서 내보낸 된 파일에서입니다.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.microsoft.com\/fwlink\/? LinkId\=83477\)합니다.   
  
### <a name="to-add-a-token-decrypting-certificate"></a>토큰을 추가 하려면\-인증서를 암호 해독  
  
1.  에 **시작** 화면에서 입력**AD FS 관리**, 한 다음 ENTER를 누릅니다.  
  
2.  콘솔 트리에서 두 번\-클릭 **Service**를 클릭 하 고 **인증서**합니다.  
  
3.  에 **동작** 창 클릭 합니다 **토큰 추가\-암호 해독 인증서** 링크.  
  
4.  에 **인증서 파일을 찾습니다** 대화 상자에서 추가 인증서 파일을 선택한 다음 클릭 하려는 인증서 파일을 이동 **오픈**합니다.  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: 페더레이션 서버 설정](Checklist--Setting-Up-a-Federation-Server.md)  
  
[페더레이션 서버에 대 한 인증서 요구 사항](https://technet.microsoft.com/library/dd807040.aspx)  
  

