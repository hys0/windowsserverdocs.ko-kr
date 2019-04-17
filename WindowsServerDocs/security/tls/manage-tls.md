---
title: "Transport Layer Security (TLS) 관리"
description: "Windows Server 보안"
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
ms.date: 06/05/2017
ms.openlocfilehash: e26d1f833dbb7219251947f1cb3cb09def958aea
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="manage-transport-layer-security-tls"></a>Transport Layer Security (TLS) 관리

## <a name="configuring-tls-cipher-suite-order"></a>구성 TLS 암호화 제품군 주문

다른 Windows 버전 다른 TLS 암호 그룹 및 우선 순위를 지원합니다. 참조 [TLS/SSL (Schannel SSP)에서 암호 그룹](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx) Microsoft Schannel 공급자의 서로 다른 Windows 버전에서 지원 되는 기본 주문에 대 한 합니다.

> [!NOTE] 
> 목록 수정할 수 있습니다 CNG 기능을 사용 하 여 암호 그룹의 참조 [Schannel 암호 그룹 우선 순위를 지정](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx) 대 한 자세한 내용은 합니다.

TLS 암호 그룹 순서를 변경 다음 부팅에 적용 됩니다. 다시 시작 또는 종료 될 때까지 기존 순서 적용 될 예정입니다.

> [!WARNING] 
> 레지스트리 설정이 기본 우선 순위 주문에 대 한 업데이트는 지원 되지 않으며 서비스 업데이트를 다시 설정할 수 있습니다. 

### <a name="configuring-tls-cipher-suite-order-by-using-group-policy"></a>그룹 정책을 사용 하 여 TLS 암호 그룹 순서를 구성 합니다.

기본 TLS 암호화 suite 순서를 구성 하는 SSL 암호화 Suite 주문 그룹 정책 설정을 사용할 수 있습니다.

1.  그룹 정책 관리 콘솔에서로 이동 **컴퓨터 구성** > **관리 템플릿** > **네트워크** > **SSL 구성 설정을**합니다.
2.  두 번 클릭 **SSL 암호 그룹 순서**을 차례로 클릭 하 고는 **사용** 옵션 합니다.
3.  마우스 오른쪽 단추로 클릭 **SSL 암호 그룹** 선택한 상자 **모두 선택** 팝업 메뉴에서 합니다.

    ![그룹 정책 설정](../media/Transport-Layer-Security-protocol/ssl-cipher-suite-order-gp-setting.png)

4.  선택한 텍스트를 마우스 오른쪽 단추로 클릭 하 고 선택 **복사** 팝업 메뉴에서 합니다.
5.  텍스트를 notepad.exe, 새 암호 제품군 주문 목록을 업데이트 등의 텍스트 편집기에 붙여 넣습니다.

    > [!NOTE]
    > TLS 암호화 suite 순서 목록 무과실 쉼표로 구분 형식에 있어야 합니다. 각 암호화 제품군 문자열의 왼쪽에서 오른쪽으로 쉼표로 (,)에 종료 됩니다. 

    > 또한 암호 그룹 목록이 1,023 자로 제한 됩니다.

6.  교체 목록에는 **SSL 암호 그룹** 주문한 목록을 업데이트 합니다.
7.  클릭 **확인** 또는 **적용**합니다.

### <a name="configuring-tls-cipher-suite-order-by-using-mdm"></a>MDM를 사용 하 여 TLS 암호 그룹 순서를 구성

Windows 10 정책 CSP TLS 암호 그룹의 구성을 지원합니다. 참조 [암호화/TLSCipherSuites](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/policy-configuration-service-provider#cryptography-tlsciphersuites) 에 대 한 자세한 내용은 합니다.

### <a name="configuring-tls-cipher-suite-order-by-using-tls-powershell-cmdlets"></a>PowerShell Cmdlet TLS 사용 하 여 TLS 암호 그룹 순서를 구성

TLS PowerShell 모듈 주문한 TLS 암호 그룹 목록이 다운로드 암호화 제품군을 사용 하지 않도록 설정 하 고 암호화 제품군 사용을 지원 합니다. 참조 [TLS 모듈](https://technet.microsoft.com/itpro/powershell/windows/tls/tls) 에 대 한 자세한 내용은 합니다.

## <a name="configuring-tls-ecc-curve-order"></a>TLS ECC 곡선 순서를 구성합니다. 

Windows 10 및 Windows Server 2016부터, ECC 곡선 주문 구성할 수 있습니다 암호 그룹 순서 독립적인. TLS 목록에 타원 곡선 접미사 제품군 순서를 암호화 된 경우 자녀가 보다 우선 합니다 새로운 타원 곡선 우선 순위를 사용 하도록 설정 하면 됩니다. 이 통해 조직에서 다른 버전의 Windows는 동일한 암호 제품군 순서를 구성 하는 그룹 정책 개체를 사용할 수 있습니다.

> [!NOTE]
> Windows 10 이전 암호화 제품군 문자열이 곡선 우선 순위를 확인 하려면 타원 곡선으로 추가 되었습니다.

### <a name="managing-windows-ecc-curves-using-certutil"></a>CertUtil를 사용 하 여 Windows ECC 곡선 관리

Windows 10 및 Windows Server 2016부터, Windows 타원 곡선 매개 관리 제공 하지만 명령줄 유틸리티 certuil.exe 합니다. 곡선 타원 매개는 bcryptprimitives.dll에 저장 됩니다. Certutil.exe을 사용 하 여 관리자 추가 하거나 제거 곡선 매개 변수를와 Windows의 각각 합니다. Certutil.exe 레지스트리에서 곡선 매개 변수를 안전 하 게 저장합니다. Windows는 곡선와 관련 된 이름으로 곡선 매개 사용을 시작할 수 있습니다.    

#### <a name="displaying-registered-curves"></a>등록 된 곡선 표시

다음 certutil.exe 명령을 사용 하 여 컴퓨터의 현재 등록 곡선 목록을 표시 합니다.

```powershell
certutil.exe –displayEccCurve
```

![디스플레이 곡선 Certutil](../media/Transport-Layer-Security-protocol/certutil-display-curves.png)

*그림 1 Certutil.exe 출력의 등록 된 곡선 목록을 표시 합니다.*

#### <a name="adding-a-new-curve"></a>새 곡선 추가

조직에서는 만들고 신뢰할 수 있는 기타 기관과 연구 곡선 매개 변수를 사용할 수 있습니다.  
Windows에서 이러한 새로운 곡선 사용 하려는 관리자 곡선을 추가 해야 합니다.  
다음 certutil.exe 명령을 사용 하 여 곡선 현재 컴퓨터에 추가 하려면:

```powershell
Certutil —addEccCurue curveName curveParameters [curveOID] [curveType]
```

- **curveName** 인수 곡선 매개 추가한 곡선의 이름을 표시 합니다.
- **curveParameters** 인수 인증서 추가할 곡선 매개 포함 된 파일 이름을 나타냅니다.
- **curveOid** 인수의 인증서를 추가 하려면 (선택 사항) 곡선 매개 OID 포함 된 파일 이름을 나타냅니다.
- **curveType** 인수에서 명명 곡선 소수점 값을 나타냅니다는 [EC 라는 곡선 레지스트리](http://www.iana.org/assignments/tls-parameters/tls-parameters.xhtml#tls-parameters-8) (선택 사항).

![Certutil 곡선 추가](../media/Transport-Layer-Security-protocol/certutil-add-curves.png)

*그림 2 곡선 certutil.exe 사용 하 여 추가 합니다.*

#### <a name="removing-a-previously-added-curve"></a>이전에 추가한 곡선 제거

관리자 곡선 이전에 추가한 다음 certutil.exe 명령을 사용 하 여 제거할 수 있습니다.

```powershell
Certutil.exe –deleteEccCurve curveName
```

컴퓨터에서 곡선 관리자 후 Windows 명명된 곡선을 사용할 수 없습니다.

## <a name="managing-windows-ecc-curves-using-group-policy"></a>그룹 정책을 사용 하 여 Windows ECC 곡선 관리

조직 곡선 매개 enterprise 도메인 가입, 그룹 정책 기본 레지스트리 확장 하 고 그룹 정책을 사용 하 여 컴퓨터에 배포할 수 있습니다.  
곡선 배포 하는 과정은 다음과 같습니다.

1.  Windows 10 및 Windows Server 2016에 사용 하 여 **certutil.exe** 명명된 곡선 등록 된 새로운 Windows에 추가 해야 합니다.
2.  해당 같은 컴퓨터에서 새 그룹 정책 개체는 그룹 정책 GPMC (관리 콘솔)를 열고 만들고 편집 하기 합니다.
3.  로 이동 **컴퓨터 구성 | 기본 설정 | Windows 설정 | 레지스트리**합니다.  마우스 오른쪽 단추로 클릭 **레지스트리**합니다. 마우스로 가리키면 **새로** 선택한 **컬렉션 항목**합니다. 곡선 이름과 일치 하도록 컬렉션 항목을 이름을 바꿉니다. 각 레지스트리 키에서 항목 두 개 레지스트리 컬렉션 만들어집니다 *HKEY_LOCAL_MACHINE\CurrentControlSet\Control\Cryptography\ECCParameters*합니다.
4.  새 추가 하 여 새로 만든된 그룹 정책 기본 레지스트리 컬렉션을 구성 **레지스트리 항목이** 아래 나열 된 각 레지스트리 값 *HKEY_LOCAL_MACHINE\CurrentControlSet\Control\Cryptography\ECCParameters\ [curveName]*합니다.
5.  새 이름이 지정 된 곡선 받아야 하는 Windows 10 및 Windows Server 2016 컴퓨터를 그룹 정책 레지스트리 컬렉션 항목을 포함 하는 그룹 정책 개체를 배포 합니다.

    ![GPP 곡선 배포](../media/Transport-Layer-Security-protocol/gpp-distribute-curves.png)

    *곡선 배포 하려면 그룹 정책 기본을 사용 하 여 그림 3*

## <a name="managing-tls-ecc-order"></a>TLS ECC 주문 관리

부터 Windows 10 및 Windows Server 2016, ECC 곡선 주문 그룹 정책 설정을 사용할 수 있는 기본 TLS ECC 곡선 순서를 구성 합니다. 일반 ECC이 설정을, 조직을 사용 하 여 자신의 신뢰할 수 있는 라는 곡선 (TLS와 함께 사용에 대해 승인 된) 운영 체제에 추가할 수 있으며 이후 TLS 시나리오에서 사용 하 여 되도록 곡선 우선 순위 부여 그룹 정책 설정에 곡선 라는 해당를 추가. 새 곡선 우선 순위 부여 목록에서 정책 설정을 받은 후 다시 부팅 활성화 됩니다.     

![GPP 곡선 배포](../media/Transport-Layer-Security-protocol/gp-managing-tls-curve-priority-order.png)

*그림 4 관리 TLS 곡선 그룹 정책을 사용 하 여 우선 순위 부여*


