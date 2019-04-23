---
ms.assetid: 10d6723e-c857-43da-9d2d-acb5641d3da8
title: 컴퓨터를 도메인에 가입
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 811f5296143637974cf82e59d57665f8a96f1c8c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884114"
---
# <a name="join-a-computer-to-a-domain"></a>컴퓨터를 도메인에 가입

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Federation Services에 대 한 \(AD FS\) 페더레이션 서버를 도메인에 가입 되어 있어야 하는 대로 작동 하는 각 컴퓨터 작동 합니다. 페더레이션 서버 프록시를 도메인에 조인할 수 있지만 이것이 요구 사항은 없습니다.  
  
웹 서버는 클레임을 호스팅하는 경우 웹 서버를 도메인에 가입 시킬 필요가 없습니다\-인식 응용 프로그램입니다.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="to-join-a-computer-to-a-domain"></a>컴퓨터를 도메인에 가입 하려면  
  
1.  에 **시작** 화면에서 입력 **제어판**, 한 다음 ENTER를 누릅니다.  
  
2.  이동할 **시스템 및 보안**를 클릭 하 고 **시스템**입니다.  
  
3.  **컴퓨터 이름, 도메인 및 작업 그룹 설정**에서 **설정 변경**을 클릭합니다.  
  
4.  **컴퓨터 이름** 탭에서 **변경**을 클릭합니다.  
  
5.  아래 **소속**, 클릭 **도메인**에이 컴퓨터에 가입 하 고 클릭 하려는 도메인의 이름을 입력 **확인**합니다.  
  
6.  **확인**을 클릭한 다음 컴퓨터를 다시 시작합니다.  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: 페더레이션 서버 설정](Checklist--Setting-Up-a-Federation-Server.md)  
  
[검사 목록: 페더레이션 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

