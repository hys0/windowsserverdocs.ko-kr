---
ms.assetid: 4b71b212-7e5b-4fad-81ee-75b3d1f27869
title: "Adfs는 인증서를 인증에 대 한 암호 확인용 호스트 구속력에 대 한 지원"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 553ff059693c7b0c0e6f0364d82c1adbca661097
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication"></a>Adfs는 인증서를 인증에 대 한 암호 확인용 호스트 구속력에 대 한 지원

>Windows Server 2016 적용 됩니다.

대부분의 네트워크에 로컬 방화벽 정책 49443 같은 포트를 사용할 수 없는 통해 교통을 허용 하지 될 수 있습니다. Windows Server 2016에 ADFS 전에 ADFS 된 인증서를 인증을 수행 하려고 할 때 문제가 알게 되었습니다. 동일한 호스트에 인증 디바이스 및 사용자 인증 인증서에 대 한 다른 바인딩이 없을 수 하기 때문입니다. 기본 포트 443 받도록 디바이스 연결와 같은 채널의 여러 구속력 지원 하기 위해 변경할 수 없습니다. 결과는 스마트 카드 인증이 작동 하지 않았던 및 사용자가 무슨 일이 정말 무슨 일 표시 되지 않으므로 모르는 했습니다.  
  
Windows Server 2016에 Adfs와이 수행할 수 있습니다.
  
Windows Server 2016에 Adfs이 변경 되었습니다. 이제 두 가지 모드를 지원 첫 번째 다른 포트 (443, 49443)와 동일한 호스트 (즉, adfs.contoso.com)를 사용 합니다. 두 번째 같은 포트 (443)와 다른 호스트 (adfs.contoso.com 및 certauth.adfs.contoso.com)를 사용 합니다. "Certauth. < adfs 서비스 이름 >" 대체 제목 이름으로 지원 하기 위해 SSL 인증서가 필요 합니다. 농장 생성 하거나 PowerShell 통해 나중에이 수행할 수 있습니다.  
  
## <a name="how-to-configure-alternate-host-name-binding-for-certificate-authentication"></a>대체 호스트 이름 구속력 인증서를 인증에 대 한 구성 하는 방법  
두 가지 방법으로 대체 호스트 이름 구속력 인증서를 인증에 대 한를 추가할 수 있습니다. 첫 번째 인증서 위에서 언급 한 두 번째 방법은 사용 하 여 설치 프로그램이 자동으로 됩니다 다음 제목을 대체 이름 (산)에 포함 된 경우 Windows server 2016 년 Adfs와 새 ADFS 농장을 설정할 때입니다. 두 가지 다른 호스트 (sts.contoso.com와 동일한 포트 certauth.sts.contoso.com 설치 프로그램 자동으로. 인증서를 SAN 포함 되어 있지 않으면 인증서 주제 대체 이름 certauth.*를 지원 하지 않는 알리는 경고를 표시 됩니다. 화면 캡처 아래를 참조 하십시오. 첫 번째 표시 되는 인증서 SAN 및 두 번째 표시 되는 인증서 되지 않았습니다를 설치 합니다.  
  
![암호 확인용 호스트 구속력](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_1.png)  
  
![암호 확인용 호스트 구속력](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_2.png)  
  
마찬가지로, Windows Server 2016에 ADFS 배포한 PowerShell cmdlet 사용할 수 있습니다: AdfsAlternateTlsClientBinding 설정 합니다.
  
```powershell
Set-AdfsAlternateTlsClientBinding -Member DC1.contoso.com -Thumbprint '<thumbprint of cert>'
```

메시지가 표시 되 면 예를 클릭 합니다.  고 수 있을 것입니다.

![암호 확인용 호스트 구속력](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_3.png)

## <a name="additional-references"></a>추가 참조

* [Adfs의 인증서를 SSL 및 Windows Server 2016에에서 WAP 관리](../operations/Manage-SSL-Certificates-AD-FS-WAP-2016.md)
