---
title: 전송 계층 보안 (TLS)를 관리 합니다.
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
author: justinha
ms.author: justinha
manager: brianlic-msft
ms.date: 05/16/2018
ms.openlocfilehash: 8053a14a74797cccce4c441d41f1f1623ba0ad6e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879444"
---
# <a name="manage-transport-layer-security-tls"></a>전송 계층 보안 (TLS)를 관리 합니다.

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10

## <a name="configuring-tls-cipher-suite-order"></a>TLS 암호화 그룹 순서 구성

다른 Windows 버전 다른 TLS 암호 그룹 및 우선 순위 순서를 지원합니다. 참조 [TLS/SSL (Schannel SSP)의 암호 그룹](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx) Microsoft Schannel 공급자가 다른 Windows 버전에서 지 원하는 기본 순서에 대 한 합니다.

> [!NOTE] 
> 목록 수정할 수도 있습니다 CNG 함수를 사용 하 여 암호 그룹을 참조 [우선 순위 지정 Schannel 암호 그룹](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx) 세부 정보에 대 한 합니다.

TLS 암호화 그룹 순서 변경 내용이 다음 부팅 시 적용 됩니다. 다시 시작 또는 종료 될 때까지 기존 순서에 적용 됩니다.

> [!WARNING] 
> 기본 우선 순위 순서에 대 한 레지스트리 설정을 업데이트 하는 지원 되지 않으며 서비스 업데이트를 다시 설정할 수 있습니다. 

### <a name="configuring-tls-cipher-suite-order-by-using-group-policy"></a>그룹 정책을 사용 하 여 TLS 암호화 그룹 순서를 구성 합니다.

기본 TLS 암호화 그룹 순서를 구성 하는 SSL 암호화 제품군 순서 그룹 정책 설정을 사용할 수 있습니다.

1.  그룹 정책 관리 콘솔에서 이동할 **컴퓨터 구성** > **관리 템플릿** > **네트워크**  >  **SSL 구성 설정을**합니다.
2.  두 번 클릭 **SSL 암호 도구 모음 순서**를 클릭 하 고는 **Enabled** 옵션.
3.  마우스 오른쪽 단추로 클릭 **SSL 암호 도구 모음** 선택한 상자 **모두 선택** 팝업 메뉴에서.

    ![그룹 정책 설정](../media/Transport-Layer-Security-protocol/ssl-cipher-suite-order-gp-setting.png)

4.  선택한 텍스트를 마우스 오른쪽 단추로 클릭 **복사** 팝업 메뉴에서.
5.  Notepad.exe와 새 암호화 제품군 순서 목록 사용 하 여 업데이트와 같은 텍스트 편집기에 텍스트를 붙여 넣습니다.

    > [!NOTE]
    > TLS 암호화 suite 순서 목록에서 엄격한 쉼표로 구분 된 형식 이어야 합니다. 각 암호화 suite 문자열의 오른쪽에 쉼표 (,)를 사용 하 여 종료 됩니다. 

    > 또한 암호화 그룹 목록은 1,023 자로 제한 됩니다.

6.  목록 대체는 **SSL 암호 그룹** 업데이트 된 정렬 된 목록을 사용 하 여 합니다.
7.  클릭 **확인** 또는 **적용**합니다.

### <a name="configuring-tls-cipher-suite-order-by-using-mdm"></a>MDM을 사용 하 여 TLS 암호화 그룹 순서를 구성

Windows 10 정책 CSP는 TLS 암호 그룹 구성을 지원합니다. 참조 [암호화/TLSCipherSuites](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/policy-configuration-service-provider#cryptography-tlsciphersuites) 자세한 내용은 합니다.

### <a name="configuring-tls-cipher-suite-order-by-using-tls-powershell-cmdlets"></a>TLS PowerShell Cmdlet을 사용 하 여 TLS 암호화 그룹 순서를 구성 합니다.

TLS PowerShell 모듈에는 TLS 암호 그룹의 정렬 된 목록 가져오기, 암호 그룹을 사용 하지 않도록 설정 및 암호 그룹을 사용 하도록 설정 하면 지원 합니다. 참조 [TLS 모듈](https://technet.microsoft.com/itpro/powershell/windows/tls/tls) 자세한 내용은 합니다.

## <a name="configuring-tls-ecc-curve-order"></a>TLS ECC 곡선이 순서를 구성합니다. 

Windows 10 및 Windows Server 2016 부터는 ECC 곡선이 순서 구성할 수 있습니다 암호화 제품군 순서와 무관 합니다. TLS 암호화 suite 순서 목록에는 타원 곡선 접미사를 하는 경우 이러한 재정의 됩니다 새 타원 곡선 우선 순위 순서에 따라 사용 하도록 설정 하는 경우. 이 통해 조직에서 암호 도구 모음 순서를 사용 하 여 서로 다른 버전의 Windows 구성 하려면 그룹 정책 개체를 사용할 수 있습니다.

> [!NOTE]
> Windows 10 이전 암호화 suite 문자열 곡선 우선 순위를 결정 하는 타원 곡선을 사용 하 여 추가 되었습니다.

### <a name="managing-windows-ecc-curves-using-certutil"></a>CertUtil을 사용 하 여 Windows ECC 곡선이 관리

Windows 10 및 Windows Server 2016 부터는 Windows는 명령줄 유틸리티 certutil.exe 통해 타원 곡선 매개 변수 관리를 제공 합니다. 타원 곡선 매개 변수는 bcryptprimitives.dll에 저장 됩니다. Certutil.exe를 사용 하 여, 관리자 추가 및 제거할 수 곡선 매개 변수에서 Windows, 각각. Certutil.exe는 곡선 매개 변수를 레지스트리에 안전 하 게 저장 합니다. Windows는 곡선을 사용 하 여 연결 된 이름으로 곡선 매개 변수를 사용할 수 있습니다.    

#### <a name="displaying-registered-curves"></a>등록 된 곡선을 표시합니다.

곡선의 목록을 표시 하려면 다음 certutil.exe 명령을 사용 하 여 현재 컴퓨터에 등록 합니다.

```powershell
certutil.exe –displayEccCurve
```

![Certutil 표시 곡선](../media/Transport-Layer-Security-protocol/certutil-display-curves.png)

*그림 1 Certutil.exe 출력을 등록 된 곡선의 목록을 표시 합니다.*

#### <a name="adding-a-new-curve"></a>새 곡선을 추가합니다.

조직에서는 만들고 신뢰할 수 있는 다른 엔터티에서 연구 곡선 매개 변수를 사용할 수 있습니다.  
Windows에서 이러한 새 곡선을 사용 하려는 관리자는 곡선을 추가 해야 합니다.  
곡선을 현재 컴퓨터에 추가할 명령을 certutil.exe를 사용 합니다.

```powershell
Certutil —addEccCurue curveName curveParameters [curveOID] [curveType]
```

- 합니다 **curveName** 인수 추가 된 곡선 매개 변수는 곡선의 이름을 나타냅니다.
- 합니다 **curveParameters** 인수 추가 하려는 곡선의 매개 변수를 포함 하는 인증서의 파일 이름을 나타냅니다.
- 합니다 **curveOid** 인수 곡선 매개 변수를 추가 하려면 (선택 사항)의 OID를 포함 하는 인증서의 파일 이름을 나타냅니다.
- 합니다 **curveType** 인수에서 명명 된 곡선을 10 진수 값을 나타내며 합니다 [EC 명명 된 곡선 레지스트리](http://www.iana.org/assignments/tls-parameters/tls-parameters.xhtml#tls-parameters-8) (선택 사항).

![Certutil 추가 곡선](../media/Transport-Layer-Security-protocol/certutil-add-curves.png)

*그림 2 certutil.exe를 사용 하 여 곡선을 추가 합니다.*

#### <a name="removing-a-previously-added-curve"></a>이전에 추가한 곡선을 제거합니다.

관리자는 명령을 certutil.exe를 사용 하 여 이전에 추가한 곡선을 제거할 수 있습니다.

```powershell
Certutil.exe –deleteEccCurve curveName
```

관리자 컴퓨터에서 곡선 제거 후 Windows 명명된 된 곡선을 사용할 수 없습니다.

## <a name="managing-windows-ecc-curves-using-group-policy"></a>그룹 정책을 사용 하 여 Windows ECC 곡선이 관리

조직에는 곡선 매개 변수 enterprise, 도메인 가입, 그룹 정책과 그룹 정책 기본 설정 레지스트리 확장을 사용 하 여 컴퓨터를 배포할 수 있습니다.  
곡선을 배포 하기 위한 프로세스 다음과 같습니다.

1.  Windows 10 및 Windows Server 2016에서 사용 하 여 **certutil.exe** Windows에 새 등록 된 명명 된 곡선을 추가 합니다.
2.  동일한 컴퓨터에서 그룹 정책 관리 콘솔 (GPMC)를 열고 새 그룹 정책 개체를 만들고 편집 합니다.
3.  이동할 **컴퓨터 구성 | 기본 설정 | Windows 설정 | 레지스트리**합니다.  마우스 오른쪽 단추로 클릭 **레지스트리**합니다. 마우스로 **새로 만들기** 선택한 **컬렉션 항목**합니다. 곡선의 이름과 일치 하도록 컬렉션 항목을 이름을 바꿉니다. 아래에 각 레지스트리 키에 대 한 하나의 레지스트리 컬렉션 항목을 만든 *HKEY_LOCAL_MACHINE\CurrentControlSet\Control\Cryptography\ECCParameters*합니다.
4.  새로 추가 하 여 새로 만든된 그룹 정책 기본 설정 레지스트리 수집 구성 **레지스트리 항목** 아래에서 나열 된 각 레지스트리 값에 대해 *HKEY_LOCAL_MACHINE\CurrentControlSet\Control\Cryptography\ ECCParameters\[curveName]* 합니다.
5.  새 명명 된 곡선을 수신 해야 하는 Windows 10 및 Windows Server 2016 컴퓨터 그룹 정책 레지스트리 컬렉션 항목을 포함 하는 그룹 정책 개체를 배포 합니다.

    ![GPP 곡선 배포](../media/Transport-Layer-Security-protocol/gpp-distribute-curves.png)

    *그림 3 Group Policy Preferences 곡선을 배포 하려면*

## <a name="managing-tls-ecc-order"></a>관리 TLS ECC 순서

ECC 곡선이 순서 그룹 정책 설정을 사용할 수 있습니다 Windows 10 및 Windows Server 2016 부터는 기본 TLS ECC 곡선이 순서를 구성 합니다. 자신의 신뢰할 수 있는 명명 된 곡선 (즉 TLS 사용 하 여 사용 하도록 승인 된) 운영 체제에 추가 하 고 향후 TLS에서 사용할 수 있도록 곡선 우선 순위 그룹 정책 설정을 추가할 해당 명명 된 곡선 수 제네릭 ECC이 설정, 조직에서는 사용 하 여 핸드셰이크입니다. 새 곡선 우선 순위는 정책 설정을 받은 후 다시 부팅 하면 활성화 됩니다.     

![GPP 곡선 배포](../media/Transport-Layer-Security-protocol/gp-managing-tls-curve-priority-order.png)

*그림 4 관리 TLS 곡선 그룹 정책을 사용 하 여 우선 순위*


