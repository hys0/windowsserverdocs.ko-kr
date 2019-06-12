---
title: Windows Server(버전 1709)에서 제거되었거나 교체될 예정인 기능
description: 릴리스에서 제거되었거나 제거될 예정인 기능
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 06/05/2018
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 37970f3bee2070cffc77bff855a8f28641196b24
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66452862"
---
# <a name="features-removed-or-planned-for-replacement-starting-with-windows-server-version-1709"></a>Windows Server, 버전 1709에서 제거되었거나 교체될 예정인 기능

>적용 대상: Windows Server, 버전 1709

다음은 이 릴리스에서 제거되었거나 다음 릴리스에서 교체될 가능성이 고려되기 시작한 Windows Server, 버전 1709 기능의 목록입니다. 상용 환경에서 운영 체제를 업데이트하는 IT 전문가가 참조하시면 유용합니다. **이 목록은 후속 릴리스에서 변경 될 수 있습니다 이며 모든 영향을 받는 기능 또는 기능을 포함 하지 않을 수 있습니다.** 

## <a name="features-removed-from-windows-server-version-1709"></a>Windows Server, 버전 1709에서 제거된 기능
Windows Server, 버전 1709에는 Windows Server 2016에 있는 동일한 기능이 포함되어 있습니다. 하지만 이 릴리스는 Windows Server 2016과는 다른 설치 옵션을 제공합니다.

- 반기 채널 릴리스로서 Windows Server, 버전 1709는 Server Core 설치 옵션만을 제공합니다. 자세한 내용은 참조 하세요 [채널 서비스 비교](../get-started-19/servicing-channels-19.md)합니다.
- 이 릴리스부터 Nano 서버를 설치 가능한 호스트 운영 체제로 사용할 수 없습니다. 대신 Nano 서버는 컨테이너 운영 체제로 이용 가능합니다. [Windows Server, 버전 1709의 Nano 서버 변경 사항](nano-in-semi-annual-channel.md)을 참조하세요.
- 이 릴리스부터 메시지 블록 (SMB (서버) 버전 1 더 이상 기본적으로 설치 됩니다. 자세한 내용은 참조 하세요 [SMBv1 Windows 10 Fall Creators Update 및 Windows Server, 버전 1709 이상 버전에서 기본적으로 설치 되지 않습니다](https://support.microsoft.com/help/4034314/smbv1-is-not-installed-by-default-in-windows)합니다.


## <a name="features-being-considered-for-replacement-starting-with-subsequent-releases"></a>다음 릴리스부터 교체를 고려 중인 기능

다음 기능은 Windows Server, 버전 1709 이후 릴리스부터 교체를 고려 중인 기능입니다. 결국에는 설치된 제품 이미지로부터 완전히 제거되고 다른 기능으로 교체(또는 다른 원본으로부터 설치 가능)되겠지만 이 릴리스에서는 여전히 사용 가능합니다. 단, 특정 기능이 제거된 경우도 있습니다. 이러한 기능에 종속된 응용 프로그램, 코드, 사용법을 계속 사용하기 위한 다른 방법 또는 향후 교체를 생각해야 합니다.

이러한 기능의 제안된 교체에 관해 공유할 피드백이 있는 경우 [피드백 허브 앱](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)을 사용할 수 있습니다. 이 앱은 Windows 10에서 실행되지만 이를 사용하여 Windows Server 제품(및 설명서)에 관한 피드백을 보낼 수 있습니다.

### <a name="iis-6-management-compatibility"></a>IIS 6 관리 호환성
교체를 고려 중인 특정 기능은 다음과 같습니다.

- IIS 6 메타베이스 호환성(Web-Metabase)
- IIS 6 관리 콘솔(Web-Lgcy-Mgmt-Console)
- IIS 6 스크립팅 도구(Web-Lgcy-Scripting)
- IIS 6 WMI 호환성(Web-WMI)

IIS 6 기반 메타베이스 스크립트 및 IIS 7 이상에서 사용되는 파일 기반 구성 사이의 에뮬레이션 계층 역할을 하는 IIS 6 메타베이스 호환성 대신 Microsoft.Web.Administration 네임스페이스와 같은 도구를 사용하여 관리 스크립트를 대상 IIS 파일 기반 구성에 직접 마이그레이션을 시작해야 합니다.

또한 IIS 6.0 이하 버전으로부터 마이그레이션을 시작하고, 가장 최신 Windows Server 릴리스에서 항상 사용 가능한 최신 IIS 버전으로 이동해야 합니다.


### <a name="iis-digest-authentication"></a>IIS 다이제스트 인증
이 인증 방법은 교체 계획 중입니다. 대신 클라이언트 인증서 매핑([일대일 클라이언트 인증서 매핑 구성](https://docs.microsoft.com/iis/manage/configuring-security/configuring-one-to-one-client-certificate-mappings) 참조) 또는 Windows 인증([응용 프로그램 설정](https://docs.microsoft.com/iis-administration/configuration/appsettings.json) 참조)과 같은 다른 인증 방법을 사용하기 시작해야 합니다.

### <a name="internet-storage-name-service-isns"></a>iSNS(Internet Storage Name Service)
iSNS는 교체 고려 중입니다. SMB(서버 메시지 블록) 기능은 기본적으로 추가 기능과 함께 동일한 기능을 제공합니다. 이 기능에 관한 배경 정보는 [서버 메시지 블록 개요](https://technet.microsoft.com/library/hh831795(v=ws.11).aspx)를 참조하세요.

### <a name="rsaaes-encryption-for-iis"></a>IIS용 RSA/AES 암호화 
때문에이 암호화 방법은 대체에 대 한 간주 되는 뛰어난 Cryptography API: 다음 세대 (CNG) 방법은 이미 사용할 수 있습니다. CNG 암호화에 대해 자세히 알아보려면 [CNG 정보](https://msdn.microsoft.com/library/windows/desktop/aa375276(v=vs.85).aspx)를 참조하세요.

### <a name="windows-powershell-20"></a>Windows PowerShell 2.0
이 Windows PowerShell 초기 버전은 최근의 여러 버전으로 대체되었습니다. 최적의 기능 및 성능을 위해 Windows PowerShell 5.0 이상으로 마이그레이션하세요. 자세한 내용은 [PowerShell 설명서](https://docs.microsoft.com/powershell/index?view=powershell-5.1)를 참조하세요.

