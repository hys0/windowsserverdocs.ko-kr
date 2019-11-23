---
title: 원격 서버 관리 도구
description: 원격 서버 관리 도구에 대 한 최상위 항목
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-rsat
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d54a1f5e-af68-497e-99be-97775769a7a7
author: coreyp-at-msft
ms.author: coreyp
manager: dansimp
ms.openlocfilehash: 121914f721cda7cbf0a117527b69568032d5541b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71387094"
---
# <a name="remote-server-administration-tools"></a>원격 서버 관리 도구

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 Windows 10에 대 한 원격 서버 관리 도구 지원 합니다.

> [!IMPORTANT]
> Windows 10 10 월 2018 업데이트부터 RSAT는 Windows 10의 **주문형 기능** 집합으로 포함 됩니다. 설치 지침은 아래의 **RSAT 버전을 사용 하는 경우를** 참조 하세요.

RSAT를 통해 IT 관리자는 windows 10 PC에서 Windows Server 역할 및 기능을 관리할 수 있습니다.

원격 서버 관리 도구에는 서버 관리자, mmc (Microsoft Management Console) 스냅인, 콘솔, Windows PowerShell cmdlet 및 공급자, Windows Server에서 실행 되는 역할 및 기능을 관리 하기 위한 몇 가지 명령줄 도구가 포함 되어 있습니다.

원격 서버 관리 도구에는 원격 서버에서 실행 되는 역할 및 기능을 관리 하는 데 사용할 수 있는 Windows PowerShell cmdlet 모듈이 포함 되어 있습니다. Windows PowerShell 원격 관리는 Windows Server 2016에서 기본적으로 활성화 되어, 있지만 Windows 10에서 기본적으로 사용 되지 않습니다. 원격 서버에 대 한 원격 서버 관리 도구의 일부인 cmdlet을 실행 하려면 원격 서버 관리 도구를 설치한 후 Windows 클라이언트 컴퓨터에서 관리자 권한 (관리자 권한으로 실행)으로 연 Windows PowerShell 세션에서 `Enable-PSremoting`를 실행 합니다.

## <a name="BKMK_Thresh"></a>Windows 10에 대 한 원격 서버 관리 도구
원격 서버 관리 도구에 대 한 Windows 10을 사용 하 여 제한 된 경우, Windows Server 2012 또는 Windows Server 2008 r 2에서 Windows Server 2016, Windows Server 2012 r 2를 실행 하는 컴퓨터에 특정 기술을 관리할 수 있습니다.

원격 서버 관리 도구에 대 한 Windows 10에는 Server Core 설치 옵션 또는 최소 서버 인터페이스 구성 Windows Server 2012 R2, Windows Server 2016 및 제한 된 경우, Windows Server 2012의 Server Core 설치 옵션을 실행 하는 컴퓨터의 원격 관리에 대 한 지원이 포함 됩니다. 그러나 원격 서버 관리 도구에 대 한 Windows 10은 모든 버전의 Windows Server 운영 체제에 설치할 수 없습니다.

### <a name="tools-available-in-this-release"></a>이번 릴리스에서 사용 가능한 도구
Windows 10에 대 한 원격 서버 관리 도구에서 사용할 수 있는 도구 목록은 [windows 운영 체제용 RSAT (원격 서버 관리 도구)](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems)의 표를 참조 하세요.

### <a name="system-requirements"></a>시스템 요구 사항
원격 서버 관리 도구에 대 한 Windows 10은 Windows 10을 실행 중인 컴퓨터에만 설치할 수 있습니다. 원격 서버 관리 도구는 Windows RT 8.1 또는 기타 시스템-온칩 장치를 실행 하는 컴퓨터에 설치할 수 없습니다.

Windows 10에 대 한 원격 서버 관리 도구은 Windows 10의 x86 기반 버전과 x64 기반 버전에서 모두 실행 됩니다.

> [!IMPORTANT]
> Windows 8.1, Windows 8, Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 또는 Windows 2000 Server 용 관리 도구 팩을 실행 하는 컴퓨터에는 Windows 10에 대 한 원격 서버 관리 도구 설치 하면 안 됩니다. 원격 서버 관리를 설치 하기 전에 컴퓨터에서 이전 시험판 버전 및 다른 언어 또는 로캘의 도구를 포함 하 여 이전 버전의 관리 도구 팩 또는 원격 서버 관리 도구를 모두 제거 합니다. Windows 10 용 도구입니다.

이 서버 관리자 릴리스를 사용 하 여 Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 r 2를 실행 하는 원격 서버에 액세스 하 고이를 관리 하려면 Se를 사용 하 여 이전 Windows Server 운영 체제를 관리할 수 있도록 여러 업데이트를 설치 해야 합니다. r 관리자. Windows 10 용 원격 서버 관리 도구에서 서버 관리자를 사용 하 여 Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2008 r 2를 관리 하도록 준비 하는 방법에 대 한 자세한 내용은 서버 관리자를 사용 하 여 [여러 원격 서버 관리](https://technet.microsoft.com/library/hh831456.aspx)를 참조 하세요.

원격 서버 관리 도구에 대 한 Windows 10에 포함 된 도구를 사용 하 여 관리 하려면 원격 서버에서 Windows PowerShell 및 서버 관리자 원격 관리를 활성화 되어야 합니다. Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012를 실행 하는 서버에서는 원격 관리가 기본적으로 사용 됩니다. 사용되지 않는 경우 원격 관리를 사용하도록 설정하는 방법에 대한 자세한 내용은 [서버 관리자를 사용하여 여러 원격 서버 관리](https://go.microsoft.com/fwlink/p/?LinkId=241358)를 참조하세요.

## <a name="install-uninstall-and-turn-offon-rsat-tools"></a>RSAT 도구 설치, 제거 및 설정/해제

### <a name="use-features-on-demand-fod-to-install-specific-rsat-tools-on-windows-10-october-2018-update-or-later"></a>필요 시 기능 ()을 사용 하 여 Windows 10 10 월 2018 업데이트 이상에 특정 RSAT 도구를 설치 합니다.

Windows 10 10 월 2018 업데이트부터 RSAT는 Windows 10에서 바로 **주문형 기능** 집합으로 포함 됩니다. 이제 RSAT 패키지를 다운로드 하는 대신 **설정** 에서 **선택적 기능 관리** 로 이동 하 여 **기능 추가** 를 클릭 하면 사용 가능한 RSAT 도구 목록을 볼 수 있습니다. 필요한 특정 RSAT 도구를 선택 하 고 설치 합니다. 설치 진행률을 보려면 [ **뒤로** ] 단추를 클릭 하 여 [ **선택적 기능 관리** ] 페이지에서 상태를 확인 하십시오.

[ **주문형 기능을**통해 제공 되는 RSAT 도구 목록을](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-non-language-fod#remote-server-administration-tools-rsat)참조 하세요. 그래픽 **설정** 앱을 통해 설치 하는 것 외에도 [**DISM/Add-Capability**](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities#using-dism-add-capability-to-add-or-remove-fods)을 사용 하 여 명령줄 또는 자동화를 통해 특정 RSAT 도구를 설치할 수 있습니다.

주문형 기능의 한 가지 장점으로는 설치 된 기능이 Windows 10 버전 업그레이드에도 유지 됩니다.

#### <a name="to-uninstall-specific-rsat-tools-on-windows-10-october-2018-update-or-later-after-installing-with-fod"></a>Windows 10 10 월 2018 업데이트 이상에서 특정 RSAT 도구를 제거 하려면 (with d를 사용 하 여 설치한 후)

Windows 10에서 **설정** 앱을 열고, **선택적 기능 관리**로 이동 하 고, 제거 하려는 특정 RSAT 도구를 선택 하 여 제거 합니다. 일부 경우에는 종속성을 수동으로 제거 해야 합니다. 특히 rsat 도구 B에서 RSAT 도구 A가 필요한 경우 rsat 도구 B가 아직 설치 되어 있으면 A rsat 도구를 제거 하도록 선택 하면 실패 합니다. 이 경우 RSAT tool B를 먼저 제거한 다음 RSAT tool A를 제거 합니다. 또한 일부 경우에는 도구가 아직 설치 되어 있어도 RSAT 도구를 제거 하는 것 처럼 보일 수 있습니다. 이 경우 PC를 다시 시작 하면 도구 제거를 완료 합니다.

종속성을 [포함 한 RSAT 도구 목록을](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-non-language-fod#remote-server-administration-tools-rsat)참조 하세요. 그래픽 설정 앱을 통해를 제거 하는 것 외에도 [**DISM/Remove-Capability**](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities#using-dism-add-capability-to-add-or-remove-fods)을 사용 하 여 명령줄 또는 자동화를 통해 특정 RSAT 도구를 제거할 수 있습니다.

### <a name="when-to-use-which-rsat-version"></a>RSAT 버전을 사용 하는 경우

10 월 2018 업데이트 (1809) 이전 버전의 Windows 10이 있는 경우 **주문형 기능**을 사용할 수 없습니다. RSAT 패키지를 다운로드 하 여 설치 해야 합니다.

- 위에 설명 된 대로 windows Server 2019 또는 이전 버전을 관리 하기 위해 windows 10 10 월 2018 업데이트 (1809) 이상에 설치할 경우 windows **10에서 직접 RSAT를 설치**합니다.

- **아래에 설명 된 대로 WS_1803 RSAT 패키지를 다운로드 하 여 설치**합니다. windows server, 버전 1803 또는 windows server, 버전 1709을 관리 하기 위해 Windows 10 4 월 2018 업데이트 (1803) 또는 이전 버전에 설치 하는 경우입니다.

- Windows Server 2016 또는 이전 버전 관리를 위해 Windows 10 4 월 2018 업데이트 (1803) 또는 이전 버전에 설치 하는 경우 **아래에 설명 된 대로 WS2016 RSAT 패키지를 다운로드 하 여 설치**합니다.

#### <a name="BKMK_installthresh"></a>RSAT 패키지를 다운로드 하 여 Windows 10 용 원격 서버 관리 도구 설치

1.  원격 서버 관리 도구에 대 한 Windows 10 패키지를 다운로드는 [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/?LinkID=404281)합니다. 다운로드 센터 웹 사이트에서 설치 프로그램을 실행하거나 다운로드 패키지를 로컬 컴퓨터 또는 공유에 저장합니다.

    > [!IMPORTANT]
    > Windows 10을 실행 중인 컴퓨터에서 원격 서버 관리 도구에 대 한 Windows 10만 설치할 수 있습니다. 원격 서버 관리 도구는 Windows RT 8.1 또는 기타 시스템-온칩 장치를 실행 하는 컴퓨터에 설치할 수 없습니다.

2.  다운로드 패키지를 로컬 컴퓨터나 공유에 저장한 경우 도구를 설치하려는 컴퓨터의 아키텍처에 따라 **WindowsTH-KB2693643-x64.msu** 또는 **WindowsTH-KB2693643-x86.msu**설치 프로그램을 두 번 클릭합니다.

3.  **Windows 업데이트 독립 실행형 설치 관리자** 대화 상자에서 메시지가 표시되면 **예**를 클릭합니다.

4.  사용 조건을 읽고 이에 동의합니다. **동의함**을 클릭합니다.

5.  설치를 완료하는 데 몇 분 정도 소요될 수 있습니다.

##### <a name="to-uninstall-remote-server-administration-tools-for-windows-10-after-rsat-package-install"></a>Windows 10 용 원격 서버 관리 도구를 제거 하려면 (RSAT 패키지 설치 후)

1. 바탕 화면에서 **시작**, **모든 앱**, **Windows 시스템**, **제어판**을 차례로 클릭합니다.

2. **프로그램**에서 **프로그램 제거**를 클릭합니다.

3. **설치된 업데이트 보기**를 클릭합니다.

4. **Microsoft Windows 업데이트(KB2693643)** 를 마우스 오른쪽 단추로 클릭한 다음 **제거**를 클릭합니다.

5. 이 업데이트를 제거할 것인지 묻는 메시지가 표시되면 **예**를 클릭합니다.
   S
   ##### <a name="to-turn-off-specific-tools-after-rsat-package-install"></a>특정 도구 (RSAT 패키지 설치 후)를 해제 하려면

6. 바탕 화면에서 **시작**, **모든 앱**, **Windows 시스템**, **제어판**을 차례로 클릭합니다.

7. **프로그램**을 클릭한 다음 **프로그램 및 기능** 에서 **Windows 기능 사용/사용 안 함**을 클릭합니다.

8. **Windows 기능** 대화 상자에서 **원격 서버 관리 도구**를 확장한 다음 **역할 관리 도구** 또는 **기능 관리 도구**를 확장합니다.

9. 끄려는 도구에 대한 확인란의 선택을 취소합니다.

   > [!NOTE]
   > 서버 관리자 해제를 설정 하면 컴퓨터를 다시 시작 해야, 및에서 액세스할 수 있었던 도구는는 **도구** 서버 관리자의 메뉴에서 열어야는 **관리 도구** 폴더입니다.

10. 사용하지 않으려는 도구를 모두 끄면 **확인**을 클릭합니다.

### <a name="run-remote-server-administration-tools"></a>원격 서버 관리 도구 실행

> [!NOTE]
> 원격 서버 관리 도구에 대 한 Windows 10을 설치한 후의 **관리 도구** 폴더에 표시 되는 **시작** 메뉴. 다음 위치에서 도구에 액세스할 수 있습니다.
>
> -   **도구** 서버 관리자 콘솔의 메뉴.
> -   **제어판\시스템 및 보안\관리 도구**
> -   **관리 도구** 폴더에서 바탕 화면에 저장된 바로 가기. 바로 가기를 만들려면 **제어판\시스템 및 보안\관리 도구** 링크를 마우스 오른쪽 단추로 클릭하고 **바로 가기 만들기**를 클릭합니다.

Windows 10의 원격 서버 관리 도구 일부로 설치 된 도구는 로컬 클라이언트 컴퓨터를 관리 하는 데 사용할 수 없습니다. 실행 하는 도구에 관계 없이 도구를 실행할 원격 서버 또는 여러 원격 서버를 지정 해야 합니다. 서버 관리자 서버 풀에 있는 도구를 사용 하 여 서버를 관리 하기 전에 관리 하려는 원격 서버를 추가 하는 대부분의 도구에는 서버 관리자와 통합 되어 있는데는 **도구** 메뉴. 서버를 서버 풀에 추가하는 방법과 서버의 사용자 지정 그룹을 만드는 방법에 대한 자세한 내용은 [서버 관리자에 서버 추가](https://go.microsoft.com/fwlink/p/?LinkId=241353) 및 [서버 그룹 생성 및 관리](https://go.microsoft.com/fwlink/?LinkId=247328)를 참조하세요.

Windows 10에 대 한 원격 서버 관리 도구에서는 서버 관리자 콘솔의 **도구** 메뉴에서 mmc 스냅인 및 대화 상자와 같은 모든 GUI 기반 서버 관리 도구에 액세스할 수 있습니다. 도구를 설치한 후 클라이언트 기반 운영 체제를 실행 하는 원격 서버 관리 도구에 대 한 Windows 10을 실행 하는 컴퓨터, 서버 관리자를 원격 서버 관리 도구에 대 한 Windows 10에 포함 된 클라이언트 컴퓨터에서 기본적으로 자동으로 열립니다. 없는 **로컬 서버** 클라이언트 컴퓨터에서 실행 하는 서버 관리자 콘솔의 페이지입니다.

##### <a name="to-start-server-manager-on-a-client-computer"></a>클라이언트 컴퓨터에서 서버 관리자를 시작하려면

1.  **시작** 메뉴에서 **모든 앱**을 클릭한 다음 **관리 도구**를 클릭합니다.

2.  **관리 도구** 폴더에서 **서버 관리자**를 클릭합니다.

서버 관리자 콘솔 **도구** 메뉴에는 표시 되지 않지만 Windows PowerShell Cmdlet 및 명령 프롬프트 관리 도구는 역할 및 기능에 대 한 원격 서버 관리 도구의 일부로도 설치 됩니다. 예를 들어 관리자 권한으로 Windows PowerShell 세션을 열고 (관리자 권한으로 실행) cmdlet `Get-Command -Module RDManagement`실행 하면 cmdlet이 원격 데스크톱 서비스 역할의 전부 또는 일부를 실행 하는 원격 서버를 대상으로 하는 한, 원격 서버 관리 도구 설치 후 로컬 컴퓨터에서 실행할 수 있는 원격 데스크톱 서비스 cmdlet 목록이 결과에 포함 됩니다.

##### <a name="to-start-windows-powershell-with-elevated-user-rights-run-as-administrator"></a>관리자 권한으로 Windows PowerShell을 시작하려면(관리자 권한으로 실행)

1.  **시작** 메뉴에서 **모든 앱**, **Windows 시스템**, **Windows PowerShell**을 차례로 클릭합니다.

2.  Windows PowerShell 관리자 권한으로 바탕 화면에서를 실행 하려면 마우스 오른쪽 단추로 클릭는 **Windows PowerShell** 바로 가기를 마우스 클릭 한 다음 **관리자 권한으로 실행**합니다.

> [!NOTE]
> 서버 관리자에서 역할 또는 그룹 페이지에서 관리 되는 서버를 마우스 오른쪽 단추로 클릭 한 다음 클릭 하 여 특정 서버에서 대상으로 하는 Windows PowerShell 세션을 시작할 수도 있습니다 **Windows PowerShell**합니다.


## <a name="known-issues"></a>알려진 문제

### <a name="issue-rsat-fod-installation-fails-with-error-code-0x800f0954"></a>**문제**: RSAT를 설치 하지 못했습니다. 오류 코드 0x800f0954

> **영향**: WSUS/SCCM 환경에서 Windows 10 1809 (10 월 2018 업데이트)에 대 한 RSAT
> 
> **해결**방법: WSUS 또는 SCCM을 통해 업데이트를 수신 하는 도메인에 가입 된 PC에 ods를 설치 하려면 Windows 업데이트 또는 로컬 공유에서 직접 ds를 다운로드할 수 있도록 그룹 정책 설정을 변경 해야 합니다. 해당 설정을 변경 하는 방법에 대 한 자세한 내용과 지침은 [WSUS/SCCM을 사용 하는 경우 주문형 기능](https://docs.microsoft.com/windows/deployment/update/fod-and-lang-packs)을 사용 하는 방법을 참조 하세요.

---

### <a name="issue-rsat-fod-installation-via-settings-app-does-not-show-statusprogress"></a>**문제**: 설정 앱을 통해 RSAT를 설치 하면 상태/진행률이 표시 되지 않음

> **영향**: Windows 10 1809에서 RSAT (2018 업데이트 10 월)
> 
> **해결**방법: 설치 진행률을 보려면 [ **뒤로** ] 단추를 클릭 하 여 [ **선택적 기능 관리** ] 페이지에서 상태를 확인 하십시오.

---

### <a name="issue-rsat-fod-uninstallation-via-settings-app-may-fail"></a>**문제**: 설정 앱을 통해 RSAT를 제거 하는 작업이 실패할 수 있음

> **영향**: Windows 10 1809에서 RSAT (2018 업데이트 10 월)
> 
> **해결**방법: 일부 경우에는 종속성을 수동으로 제거 해야 하므로 제거 실패가 발생 합니다. 특히 rsat 도구 B에서 RSAT 도구 A가 필요한 경우 rsat 도구 B가 아직 설치 되어 있으면 A rsat 도구를 제거 하도록 선택 하면 실패 합니다. 이 경우 RSAT tool B를 먼저 제거한 다음 RSAT tool A를 제거 합니다. 종속성을 포함 하 여 RSAT의 목록을 참조 하세요.

---

### <a name="issue-rsat-fod-uninstallation-appears-to-succeed-but-the-tool-is-still-installed"></a>**문제**: RSAT가 성공적으로 제거 되었지만 도구가 아직 설치 되어 있습니다.

> **영향**: Windows 10 1809에서 RSAT (2018 업데이트 10 월)
> 
> **해결**방법: PC를 다시 시작 하면 도구 제거를 완료 합니다.

---

### <a name="issue-rsat-missing-after-windows-10-upgrade"></a>**문제**: Windows 10 업그레이드 후 RSAT가 누락 됨

> **영향**: 모든 RSAT. MSU 패키지 설치 (RSAT (RSAT) 이전)가 자동으로 다시 설치 되지 않음
> 
> **해결**방법: rsat 설치는 rsat로 인 한 OS 업그레이드에서 지속 될 수 없습니다. MSU는 Windows 업데이트 패키지로 제공 됩니다. Windows 10을 업그레이드 한 후에 RSAT를 다시 설치 하세요. 이 제한은 Windows 10 1809부터 시작 하는 이유 중 하나입니다. 설치 된 RSAT는 이후 Windows 10 버전 업그레이드에 따라 유지 됩니다.

## <a name="see-also"></a>참고 항목
>- [Windows 10에 대 한 원격 서버 관리 도구](https://go.microsoft.com/fwlink/?LinkID=404281)
>- [Windows Vista, Windows 7, Windows 8, Windows Server 2008, Windows Server 2008 R2, Windows Server 2012 및 Windows Server 2012 R2 용 RSAT (원격 서버 관리 도구)](https://go.microsoft.com/fwlink/p/?LinkID=221055)
