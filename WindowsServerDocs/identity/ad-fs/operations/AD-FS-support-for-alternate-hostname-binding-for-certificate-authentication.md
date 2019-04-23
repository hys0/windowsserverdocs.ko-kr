---
ms.assetid: 4b71b212-7e5b-4fad-81ee-75b3d1f27869
title: 인증서 인증을 위한 대체 호스트 이름 바인딩에 대한 AD FS 지원
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 553ff059693c7b0c0e6f0364d82c1adbca661097
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887254"
---
# <a name="ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication"></a>인증서 인증을 위한 대체 호스트 이름 바인딩에 대한 AD FS 지원

>적용 대상: Windows Server 2016

대부분의 네트워크에는 로컬 방화벽 정책 못할 수 있습니다 트래픽 49443 같은 비표준 포트를 통해. Windows Server 2016에서 AD FS 전에 AD FS 사용 하 여 인증서 인증을 수행 하려고 할 때이 큰 문제가 됩니다. 즉, 동일한 호스트에 장치 인증 및 사용자 인증서 인증에 대 한 서로 다른 바인딩을 같을 수 없었습니다. 기본 포트 443 장치 인증서를 받이 바인딩되고 동일한 채널에서 여러 바인딩을 지원 하기 위해 변경할 수 없습니다. 결과적으로 스마트 카드 인증이 작동 하지 않습니다 하 고 사용자가 실제로 변경 된 내용에 대 한 표시가 없습니다 이후 발생 한 일 수 있었습니다.  
  
Windows Server 2016에서 AD FS와 함께이 수행할 수 있습니다.
  
이 Windows Server 2016에서 AD FS에서 변경 되었습니다. 두 가지 모드, 지원 이제 첫 번째는 동일한 호스트 (예: adfs.contoso.com)를 사용 하 여 서로 다른 포트 (443, 49443). 두 번째 동일한 포트 (443)와 서로 다른 호스트 (예: adfs.contoso.com 및 certauth.adfs.contoso.com)를 사용 합니다. 이 기능을 지원 하도록 "certauth < adfs 서비스 이름 >" 대체 주체 이름으로 SSL 인증서를 해야 합니다. 팜 만들 때나 나중에 PowerShell을 통해이 수행할 수 있습니다.  
  
## <a name="how-to-configure-alternate-host-name-binding-for-certificate-authentication"></a>인증서 인증에 대 한 대체 호스트 이름 바인딩을 구성 하는 방법  
두 가지 방법으로 인증서 인증에 대 한 대체 호스트 이름 바인딩을 추가할 수 있습니다. 첫째는 위에서 언급 한 두 번째 방법을 사용 하 여 설치 프로그램이 자동으로 됩니다 인증서 주체 대체 이름 (SAN) 포함 되어 있으면 Windows server 2016 년까지 AD FS와 함께 새 AD FS 팜을 설정할 때입니다. 즉, 두 명의 서로 다른 호스트 (예: sts.contoso.com 및 동일한 포트와 certauth.sts.contoso.com를 설정이 자동으로 됩니다. 인증서에 SAN을 찾을 수 없는 경우 인증서 주체 대체 이름 certauth. *를 지원 하지 않음을 알리는 경고가 표시 됩니다. 아래 스크린 샷을 참조 하십시오. 첫 번째 인증서가 SAN 열리고 두 번째 그렇지 않은 인증서를 보여 줍니다. 설치를 보여줍니다.  
  
![대체 호스트 이름 바인딩](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_1.png)  
  
![대체 호스트 이름 바인딩](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_2.png)  
  
마찬가지로, Windows Server 2016에서 AD FS 배포 되 면 PowerShell cmdlet을 사용할 수 있습니다. Set-AdfsAlternateTlsClientBinding.
  
```powershell
Set-AdfsAlternateTlsClientBinding -Member DC1.contoso.com -Thumbprint '<thumbprint of cert>'
```

예를 클릭 합니다.  고 수 있을 것입니다.

![대체 호스트 이름 바인딩](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_3.png)

## <a name="additional-references"></a>추가 참조

* [AD FS 및 Windows Server 2016의에서 WAP에서 SSL 인증서 관리](../operations/Manage-SSL-Certificates-AD-FS-WAP-2016.md)
