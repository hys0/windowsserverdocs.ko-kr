---
ms.assetid: 638c89bd-87e6-484b-9d2e-8ae2a74227e5
title: 서비스 통신 인증서 설정
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: d0464853c73f88ed76545921ffc8a4bf8551c800
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408328"
---
# <a name="set-a-service-communications-certificate"></a>서비스 통신 인증서 설정


Active Directory Federation Services \(AD FS 페더레이션 서버는 서비스 통신 인증서를 사용 하 여 웹 클라이언트 또는 페더레이션 서버 프록시와의 SSL(Secure Sockets Layer) \(SSL\) 웹 서비스 트래픽을 보호\).

> [!NOTE]  
> 서비스 통신 인증서가 SSL 인증서와 동일 하지 않습니다. AD FS SSL 인증서를 변경 하려면 Powershell을 사용 해야 합니다. 이 [문서의](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/manage-ssl-certificates-ad-fs-wap)지침을 따르세요.


다음 절차를 사용 하 여의 AD FS 관리 스냅인\-서비스 통신 인증서를 변경할 수 있습니다.  

> [!NOTE]  
> 의 AD FS Management snap\-는 페더레이션 서버에 대 한 서버 인증 인증서를 서비스 통신 인증서로 참조 합니다.  

로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) 에서 적절 한 계정 및 그룹 구성원 자격 사용에 대 한 세부 정보를 검토 \(http:\/\/go.microsoft.com\/fwlink\/? LinkId\=83477\).   

### <a name="to-set-a-service-communications-certificate"></a>서비스 통신 인증서를 설정 하려면  

1.  **시작** 화면에서**AD FS 관리**를 입력 한 다음 enter 키를 누릅니다.  

2.  콘솔 트리에서 **서비스**를 두 번 클릭 한 다음 **인증서**를 클릭\-합니다.  

3.  **작업** 창에서 **서비스 통신 인증서 설정** 링크를 클릭 합니다.  

4.  **서비스 통신 인증서 선택** 대화 상자에서 서비스 통신 인증서로 설정할 인증서 파일로 이동 하 고 인증서 파일을 선택한 다음 **열기**를 클릭 합니다.  

## <a name="additional-references"></a>추가 참조  
[검사 목록: 페더레이션 서버 설정](Checklist--Setting-Up-a-Federation-Server.md)  

[페더레이션 서버에 대한 인증서 요구 사항](https://technet.microsoft.com/library/dd807040.aspx)  
