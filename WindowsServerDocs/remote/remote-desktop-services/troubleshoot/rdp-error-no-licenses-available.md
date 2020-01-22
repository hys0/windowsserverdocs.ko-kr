---
title: 클라이언트에서 연결할 수 없고 "사용 가능한 라이선스 없음" 오류가 표시됨
description: 원격 데스크톱 연결과 관련된 "사용 가능한 라이선스 없음" 오류를 해결합니다.
audience: itpro
ms.custom: na
ms.reviewer: rklemen
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: troubleshooting
ms.assetid: ''
author: kaushika-msft
manager: dcscontentpm
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 74b4656216d5568f546d1a13722eeec748f1f9b5
ms.sourcegitcommit: c5709021aa98abd075d7a8f912d4fd2263db8803
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2020
ms.locfileid: "76265895"
---
# <a name="clients-cant-connect-and-see-no-licenses-available-error"></a>클라이언트에서 연결할 수 없고 "사용 가능한 라이선스 없음" 오류가 표시됨

이 상황은 RDSH 서버 및 원격 데스크톱 라이선스 서버가 포함된 배포에 적용됩니다.

먼저 사용자가 보고 있는 다음과 같은 동작을 확인합니다.

- 사용할 수 있는 라이선스 또는 라이선스 서버가 없어 세션 연결이 끊어졌습니다.
- 보안 오류로 인해 액세스가 거부되었습니다.

RD 세션 호스트에 도메인 관리자 권한으로 로그인하고, RD 라이선스 진단 도구를 엽니다. 다음과 같은 메시지를 찾습니다.

  - 원격 데스크톱 세션 호스트 서버의 유예 기간이 만료되었지만 RD 세션 호스트 서버가 라이선스 서버로 구성되지 않았습니다. RD 세션 호스트 서버에 라이선스 서버가 구성되어 있지 않으면 RD 세션 호스트 서버로의 연결이 거부됩니다.
  - \<컴퓨터 이름\> 라이선스 서버를 사용할 수 없습니다. 네트워크 연결 문제가 있거나,원격 데스크톱 라이선싱 서비스가 라이선스 서버에서 중지되었거나, RD 라이선싱을 사용할 수 없기 때문일 수 있습니다.

이러한 문제는 다음과 같은 사용자 메시지와 관련이 있는 경우가 많습니다.

  - 이 컴퓨터에 사용할 수 있는 원격 데스크톱 클라이언트 액세스 라이선스가 없어서 원격 세션이 끊겼습니다.
  - 라이선스를 제공하는 데 사용할 수 있는 원격 데스크톱 라이선스 서버가 없어서 원격 세션이 끊겼습니다.

이 경우 [RD 라이선스 서비스를 구성](#configure-the-rd-licensing-service)합니다.

RD 라이선스 진단 도구가 "RDP 프로토콜 구성 요소 X.224가 프로토콜 스트림에서 오류를 발견하여 클라이언트 연결을 끊겼습니다"와 비슷한 다른 문제를 나열하는 경우 라이선스 인증서에 영향을 주는 문제일 수 있습니다. 이와 같은 문제는 다음과 같은 사용자 메시지와 관련이 있는 경우가 많습니다.

보안 오류로 인해 클라이언트가 터미널 서버에 연결할 수 없습니다. 네트워크에 로그인되었는지 확인한 후 서버에 다시 연결해 보세요.

이 경우 [X509 인증서 레지스트리 키를 새로 고칩니다](#refresh-the-x509-certificate-registry-keys).

## <a name="configure-the-rd-licensing-service"></a>RD 라이선스 서비스 구성

다음 절차에서는 서버 관리자를 사용하여 구성을 변경합니다. 서버 관리자를 구성하고 사용하는 방법에 대한 내용은 [서버 관리자](../../../administration/server-manager/server-manager.md)를 참조하세요.

1. **서버 관리자**를 열고, **원격 데스크톱 서비스**로 이동합니다.
2. **배포 개요**에서 **작업**을 선택한 다음, **배포 속성 편집**을 선택합니다.
3. **RD 라이선싱**을 선택한 다음, 배포에 적합한 라이선싱 모드(**디바이스 단위** 또는 **사용자 단위**)를 선택합니다.
4. RD 라이선스 서버의 FQDN(정규화된 도메인 이름)을 입력한 다음, **추가**를 선택합니다.
5. RD 라이선스 서버가 둘 이상인 경우 서버마다 4단계를 반복합니다. 
    ![서버 관리자의 RD 라이선스 서버 구성 옵션.](../media/troubleshoot-remote-desktop-connections/RDLicensing_Configure.png)

## <a name="refresh-the-x509-certificate-registry-keys"></a>X509 인증서 레지스트리 키 새로 고침

> [!IMPORTANT]  
> 이 섹션의 지침은 주의 깊게 수행해야 합니다. 레지스트리를 잘못 수정하면 심각한 문제가 발생할 수 있습니다. 문제가 발생하는 경우에 대비하여 복원할 수 있도록 레지스트리 수정을 시작하기 전에 해당 [레지스트리를 백업](https://support.microsoft.com/help/322756)하세요.

이 문제를 해결하려면 X509 인증서 레지스트리 키를 백업한 후 제거하고, 컴퓨터를 다시 시작하고, RD 라이선스 서버를 다시 활성화합니다. 다음 단계를 수행합니다.

> [!NOTE]
> 각 RDSH 서버에서 다음 절차를 수행합니다.

RD 라이선싱 서버를 다시 활성화하는 방법은 다음과 같습니다.

1. 레지스트리 편집기를 열고, **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\RCM**으로 이동합니다.
2. [레지스트리] 메뉴에서 **레지스트리 파일 내보내기**를 선택합니다.
3. **파일 이름** 상자에 **exported-Certificate**를 입력한 다음, **저장**을 선택합니다.
4. 다음 값을 각각 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택한 다음, **예**를 선택하여 삭제를 확인합니다.  
      - **인증서**
      - **X509 인증서**
      - **X509 인증서 ID**
      - **X509 인증서2**
5. 레지스트리 편집기를 종료하고, RDSH 서버를 다시 시작합니다.