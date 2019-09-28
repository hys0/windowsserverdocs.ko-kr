---
title: AD FS 문제 해결-Idp-시작 된 로그온
description: 이 문서에서는 AD FS 로그온 페이지의 문제를 해결 하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 89ee45bd0387cf728bc126529169b6b1ca045d6f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366193"
---
# <a name="ad-fs-troubleshooting---idp-initiated-sign-on"></a>AD FS 문제 해결-Idp-시작 된 로그온
AD FS sign-on 페이지를 사용 하 여 인증이 작동 하는지 여부를 테스트할 수 있습니다.  이렇게 하려면 페이지로 이동 하 여 로그인 합니다.  또한 로그인 페이지를 사용 하 여 모든 SAML 2.0 신뢰 당사자가 나열 되어 있는지 확인할 수 있습니다.

## <a name="enable-the-idp-initiated-sign-on-page"></a>Idp 시작 로그온 페이지를 사용 하도록 설정
기본적으로 Windows 2016의 AD FS에는 로그온 페이지가 사용 하도록 설정 되어 있지 않습니다.  PowerShell 명령 Set-adfsproperties을 사용 하 여 사용 하도록 설정할 수 있습니다.  페이지를 사용 하도록 설정 하려면 다음 절차를 따르십시오.

1.  Windows PowerShell 열기
2.  @No__t-0을 입력 하 고 enter 키를 누릅니다.
3.  **EnableIdpInitiatedSignonPage** 이 false @no__t로 설정 되었는지 확인 합니다.-1false @ no__t-2
4.  PowerShell에서 다음을 입력 합니다. `Set-AdfsProperties -EnableIdpInitiatedSignonPage $true`
5.  확인이 표시 되지 않으므로 Set-adfsproperties를 다시 입력 하 고 **Enableidpinitatedsignonpage** 가 true로 설정 되어 있는지 확인 합니다.
![True](media/ad-fs-tshoot-initiatedsignon/idp4.png)

## <a name="test-authentication"></a>인증 테스트
Idp 시작 로그온 페이지를 사용 하 여 AD FS 인증을 테스트 하려면 다음 절차를 따르십시오.

1.  웹 브라우저를 열고 Idp sign on 페이지로 이동 합니다.  예 들어 https://sts.contoso.com/adfs/ls/idpinitiatedsignon.htm
2.  로그인 하 라는 메시지가 표시 됩니다.  자격 증명을 입력 합니다.
![Sign @ no__t-1
3.  성공적으로 완료 되 면 로그인 해야 합니다.


## <a name="test-authentication-using-a-seamless-logon-experience"></a>원활한 로그온 환경을 사용 하 여 인증 테스트
AD FS 서버에 대 한 URL이 인터넷 옵션의 로컬 인트라넷 영역에 추가 되도록 하 여 원활한 로그온 환경을 테스트할 수 있습니다.  다음 절차를 따르십시오.

1.  Windows 10 클라이언트에서 시작을 클릭 하 고 인터넷 옵션을 입력 한 다음 인터넷 옵션을 선택 합니다.
2.   보안 탭을 클릭 하 고 로컬 인트라넷을 클릭 한 다음 사이트 단추를 클릭 합니다.
![ 원활한 @ no__t-1
1.  고급을 클릭합니다.
2.  Url을 입력 하 고 추가를 클릭 합니다.  닫기를 클릭 합니다.
![ url 추가 @ no__t-1
1.  확인을 클릭 합니다.  확인을 클릭 합니다.  그러면 인터넷 옵션이 닫힙니다.
2.  웹 브라우저를 열고 Idp sign on 페이지로 이동 합니다.  예 들어 https://sts.contoso.com/adfs/ls/idpinitiatedsignon.htm
3.  로그인 단추를 클릭 합니다.  자격 증명을 묻는 메시지를 표시 하지 않고 자동으로 로그인 해야 합니다.
![ 원활한 @ no__t-1

## <a name="next-steps"></a>다음 단계

- [AD FS 문제 해결](ad-fs-tshoot-overview.md)
