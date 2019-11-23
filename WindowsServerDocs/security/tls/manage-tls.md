---
title: TLS (전송 계층 보안) 관리
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
author: justinha
ms.author: justinha
manager: brianlic-msft
ms.date: 05/16/2018
ms.openlocfilehash: a4ac1ea5b0648dbb80f103c146ad3df23fc04ab7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402344"
---
# <a name="manage-transport-layer-security-tls"></a>TLS (전송 계층 보안) 관리

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10

## <a name="configuring-tls-cipher-suite-order"></a>TLS 암호 그룹 순서 구성

Windows 버전 마다 다른 TLS 암호 그룹 및 우선 순위 순서를 지원 합니다. 다른 Windows 버전에서 Microsoft Schannel Provider가 지 원하는 기본 순서는 [TLS/SSL (SCHANNEL SSP)의 암호 그룹](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx) 을 참조 하세요.

> [!NOTE] 
> CNG 함수를 사용 하 여 암호 그룹 목록을 수정할 수도 있습니다. 자세한 내용은 [Schannel 암호 그룹 우선 순위 매기기](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx) 를 참조 하세요.

TLS 암호 그룹 순서에 대 한 변경 내용은 다음 부팅에 적용 됩니다. 다시 시작 하거나 종료할 때 까지는 기존 순서가 적용 됩니다.

> [!WARNING] 
> 기본 우선 순위 순서에 대 한 레지스트리 설정 업데이트는 지원 되지 않으며 업데이트를 제공 하 여 다시 설정할 수 있습니다. 

### <a name="configuring-tls-cipher-suite-order-by-using-group-policy"></a>그룹 정책를 사용 하 여 TLS 암호 그룹 순서 구성

SSL 암호 그룹 순서 그룹 정책 설정을 사용 하 여 기본 TLS 암호 그룹 순서를 구성할 수 있습니다.

1. 그룹 정책 관리 콘솔에서 **컴퓨터 구성** > **관리 템플릿** > **네트워크** > **SSL 구성 설정**으로 이동 합니다.
2. **SSL 암호 그룹 순서**를 두 번 클릭 한 다음 **사용** 옵션을 클릭 합니다.
3. **SSL 암호 그룹** 상자를 마우스 오른쪽 단추로 클릭 하 고 팝업 메뉴에서 **모두 선택** 을 선택 합니다.

   ![그룹 정책 설정](../media/Transport-Layer-Security-protocol/ssl-cipher-suite-order-gp-setting.png)

4. 선택한 텍스트를 마우스 오른쪽 단추로 클릭 하 고 팝업 메뉴에서 **복사** 를 선택 합니다.
5. 텍스트를 notepad.exe와 같은 텍스트 편집기에 붙여넣고 새 cipher suite 주문 목록으로 업데이트 합니다.

   > [!NOTE]
   > TLS 암호 그룹 순서 목록은 완전 한 쉼표로 구분 된 형식 이어야 합니다. 각 암호 그룹 문자열은 오른쪽에 쉼표 (,)로 끝납니다. 
   > 
   > 또한 암호 그룹의 목록은 1023 자로 제한 됩니다.

6. **SSL 암호 그룹** 의 목록을 업데이트 된 정렬 된 목록으로 바꿉니다.
7. 클릭 **확인** 또는 **적용**합니다.

### <a name="configuring-tls-cipher-suite-order-by-using-mdm"></a>MDM을 사용 하 여 TLS 암호 그룹 순서 구성

Windows 10 정책 CSP는 TLS 암호 그룹의 구성을 지원 합니다. 자세한 내용은 [Cryptography/TLSCipherSuites](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/policy-configuration-service-provider#cryptography-tlsciphersuites) 를 참조 하세요.

### <a name="configuring-tls-cipher-suite-order-by-using-tls-powershell-cmdlets"></a>TLS PowerShell Cmdlet을 사용 하 여 TLS 암호 그룹 순서 구성

TLS PowerShell 모듈은 TLS 암호 그룹의 순서 있는 목록을 가져오고, 암호 그룹을 사용 하지 않도록 설정 하 고, 암호 그룹을 사용 하도록 설정 하는 기능을 지원 합니다. 자세한 내용은 [TLS 모듈](https://technet.microsoft.com/itpro/powershell/windows/tls/tls) 을 참조 하세요.

## <a name="configuring-tls-ecc-curve-order"></a>TLS ECC 곡선 순서 구성 

Windows 10 & Windows Server 2016부터 ECC 곡선 순서는 암호화 그룹 순서에 관계 없이 구성할 수 있습니다. TLS 암호 모음 순서 목록에 타원 curve 접미사가 있으면 사용 하도록 설정 된 경우 new 타원 curve 우선 순위 순서로 재정의 됩니다. 이렇게 하면 조직에서 그룹 정책 개체를 사용 하 여 동일한 암호 그룹 순서로 여러 버전의 Windows를 구성할 수 있습니다.

> [!NOTE]
> Windows 10 이전에는 암호화 도구 문자열을 타원 곡선으로 추가 하 여 곡선 우선 순위를 결정 했습니다.

### <a name="managing-windows-ecc-curves-using-certutil"></a>CertUtil을 사용 하 여 Windows ECC 곡선 관리

Windows 10 및 Windows Server 2016부터 Windows는 명령줄 유틸리티 certutil.exe를 통해 타원 curve 매개 변수 관리를 제공 합니다. 타원 curve 매개 변수는 bcryptprimitives에 저장 됩니다. 관리자는 certutil.exe를 사용 하 여 각각 Windows에서 곡선 매개 변수를 추가 하 고 제거할 수 있습니다. Certutil은 레지스트리에 안전 하 게 곡선 매개 변수를 저장 합니다. 곡선 매개 변수를 곡선에 연결 된 이름으로 사용 하기 시작할 수 있습니다.    

#### <a name="displaying-registered-curves"></a>등록 된 곡선 표시

다음 certutil 명령을 사용 하 여 현재 컴퓨터에 등록 된 곡선 목록을 표시 합니다.

```powershell
certutil.exe –displayEccCurve
```

![Certutil 표시 곡선](../media/Transport-Layer-Security-protocol/certutil-display-curves.png)

*그림 1 Certutil.exe 출력-등록 된 곡선 목록을 표시 합니다.*

#### <a name="adding-a-new-curve"></a>새 곡선 추가

조직에서는 다른 신뢰할 수 있는 엔터티에서 조사 된 곡선 매개 변수를 만들고 사용할 수 있습니다.  
Windows에서 이러한 새 곡선을 사용 하려는 관리자는 곡선을 추가 해야 합니다.  
다음 certutil 명령을 사용 하 여 현재 컴퓨터에 곡선을 추가 합니다.

```powershell
Certutil —addEccCurue curveName curveParameters [curveOID] [curveType]
```

- **Curvename** 인수는 곡선 매개 변수가 추가 된 곡선의 이름을 나타냅니다.
- **CurveParameters** 인수는 추가 하려는 곡선의 매개 변수를 포함 하는 인증서의 파일 이름을 나타냅니다.
- **CurveOid** 인수는 추가 하려는 곡선 매개 변수의 OID를 포함 하는 인증서의 파일 이름을 나타냅니다 (선택 사항).
- **CurveType** 인수는 [EC 명명 된 곡선 레지스트리에서](http://www.iana.org/assignments/tls-parameters/tls-parameters.xhtml#tls-parameters-8) 명명 된 곡선의 10 진수 값을 나타냅니다 (선택 사항).

![Certutil 곡선 추가](../media/Transport-Layer-Security-protocol/certutil-add-curves.png)

*그림 2 certutil.exe를 사용 하 여 곡선 추가*

#### <a name="removing-a-previously-added-curve"></a>이전에 추가한 곡선 제거

관리자는 다음 certutil 명령을 사용 하 여 이전에 추가한 곡선을 제거할 수 있습니다.

```powershell
Certutil.exe –deleteEccCurve curveName
```

관리자가 컴퓨터에서 곡선을 제거한 후에는 명명 된 곡선을 사용할 수 없습니다.

## <a name="managing-windows-ecc-curves-using-group-policy"></a>그룹 정책를 사용 하 여 Windows ECC 곡선 관리

조직에서는 그룹 정책 및 그룹 정책 기본 설정 레지스트리 확장을 사용 하 여 엔터프라이즈, 도메인에 가입 된 컴퓨터에 곡선 매개 변수를 배포할 수 있습니다.  
곡선을 배포 하는 프로세스는 다음과 같습니다.

1.  Windows 10 및 Windows Server 2016에서는 **certutil.exe** 를 사용 하 여 windows에 등록 된 새 새 곡선을 추가 합니다.
2.  동일한 컴퓨터에서 그룹 정책 관리 콘솔 (GPMC)를 열고 새 그룹 정책 개체를 만든 다음 편집 합니다.
3.  **컴퓨터 구성으로 이동 | 기본 설정 | Windows 설정 | 레지스트리**.  **레지스트리**를 마우스 오른쪽 단추로 클릭 합니다. **새** 항목 위로 마우스를 이동 하 고 **컬렉션 항목**을 선택 합니다. 곡선의 이름과 일치 하도록 컬렉션 항목의 이름을 바꿉니다. *HKEY_LOCAL_MACHINE \currentcontrolset\control\cryptography\eccparameters*에서 각 레지스트리 키에 대해 하나의 레지스트리 컬렉션 항목을 만듭니다.
4.  *HKEY_LOCAL_MACHINE \currentcontrolset\control\cryptography\eccparameters\[curveName]* 아래에 나열 된 각 레지스트리 값에 새 **레지스트리 항목** 을 추가 하 여 새로 만든 그룹 정책 기본 설정 레지스트리 컬렉션을 구성 합니다.
5.  새 명명 된 곡선을 받아야 하는 Windows 10 및 Windows Server 2016 컴퓨터에 그룹 정책 레지스트리 컬렉션 항목을 포함 하는 그룹 정책 개체를 배포 합니다.

    ![GPP 분포 곡선](../media/Transport-Layer-Security-protocol/gpp-distribute-curves.png)

    *그림 3 그룹 정책 기본 설정을 사용 하 여 곡선 분포*

## <a name="managing-tls-ecc-order"></a>TLS ECC 주문 관리

Windows 10 및 Windows Server 2016부터 ECC 곡선 순서 그룹 정책 설정을 사용 하 여 기본 TLS ECC 곡선 순서를 구성할 수 있습니다. 조직에서는 일반 ECC 및이 설정을 사용 하 여 TLS에서 사용 하도록 승인 된 고유한 명명 된 곡선을 운영 체제에 추가한 다음, 이러한 명명 된 곡선을 곡선 우선 순위에 추가 하 그룹 정책 설정 하 여 이후 TLS에서 사용 되는지 확인 합니다. 핸드셰이크. 새 곡선 우선 순위 목록은 정책 설정을 받은 후 다음에 다시 부팅할 때 활성화 됩니다.     

![GPP 분포 곡선](../media/Transport-Layer-Security-protocol/gp-managing-tls-curve-priority-order.png)

*그림 4 그룹 정책를 사용 하 여 TLS 곡선 우선 순위 관리*


