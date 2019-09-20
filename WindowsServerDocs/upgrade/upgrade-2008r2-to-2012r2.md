---
title: Windows Server 2008 r 2를 Windows Server 2012 r 2로 업그레이드 | Microsoft Docs
description: Windows Server 2008 r 2에서 Windows Server 2012 r 2로 이동 하는 전체 업그레이드를 수행 하는 방법에 대해 알아봅니다.
ms.prod: windows server
ms.technology: server-general
ms.topic: upgrade
author: RobHindman
ms.author: robhind
ms.date: 09/16/2019
ms.openlocfilehash: d5051239f7269eb4b6361187121ac960e06f6d9e
ms.sourcegitcommit: 27f0caf74e88781054250455c3c1adf06deb6234
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71125083"
---
# <a name="upgrade-windows-server-2008-r2-to-windows-server-2012-r2"></a>Windows Server 2008 R2를 Windows Server 2012 r 2로 업그레이드

서버를 평면화 하지 않고 이미 설정한 동일한 하드웨어 및 모든 서버 역할을 유지 하려는 경우에는 전체 업그레이드를 수행 하는 것이 좋습니다. 전체 업그레이드를 사용 하면 이전 운영 체제에서 최신 버전으로 전환 하는 동시에 설정, 서버 역할 및 데이터를 그대로 유지할 수 있습니다. 이 문서는 Windows Server 2008 r 2에서 Windows Server 2012 r 2로 이동 하는 데 도움이 됩니다.

Windows Server 2019로 업그레이드 하려면 먼저이 항목을 사용 하 여 Windows Server 2012 R2로 업그레이드 한 다음 [Windows server 2012 r 2에서 Windows server 2019로 업그레이드](upgrade-2012r2-to-2019.md)합니다.

## <a name="before-you-begin-your-in-place-upgrade"></a>전체 업그레이드를 시작 하기 전에

Windows Server 업그레이드를 시작 하기 전에 진단 및 문제 해결을 위해 장치에서 일부 정보를 수집 하는 것이 좋습니다. 이 정보는 업그레이드가 실패 하는 경우에만 사용할 수 있으므로 장치에서 정보를 가져올 수 있는 위치에 저장 해야 합니다.

### <a name="to-collect-your-info"></a>정보를 수집 하려면

1. 명령 프롬프트를 열고로 `c:\Windows\system32`이동한 다음 **printbrm.exe**를 입력 합니다.

2. 결과 시스템 정보를 장치 어딘가에 복사 하 여 붙여넣고 저장 합니다.

3. 명령 프롬프트에 **ipconfig/all** 을 입력 한 다음 결과 구성 정보를 복사 하 여 위와 동일한 위치에 붙여 넣습니다.

4. 레지스트리 편집기를 열고 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion hive로 이동한 다음 Windows Server **Buildlabex** (버전) 및 **EditionID** (버전)를 위와 동일한 위치에 복사 하 여 붙여 넣습니다.

모든 Windows Server 관련 정보를 수집한 후에는 운영 체제, 앱 및 가상 컴퓨터를 백업 하는 것이 좋습니다. 또한 서버에서 현재 실행 중인 모든 가상 컴퓨터를 **종료**하거나, **신속**하 게 마이그레이션하거나, **실시간으로 마이그레이션해야** 합니다. 전체 업그레이드 중에는 가상 컴퓨터를 실행할 수 없습니다.

## <a name="to-perform-the-upgrade"></a>업그레이드를 수행 하려면

1. **Buildlab ex** 값이 Windows Server 2008 r 2를 실행 하 고 있는지 확인 합니다.

2. Windows Server 2012 R2 설치 미디어를 찾은 **다음 setup.exe를 선택 합니다**.

    ![Setup.exe 파일을 보여 주는 Windows 탐색기](media/upgrade-2008r2-2012r2/setup-2012r2.png)

3. **예** 를 선택 하 여 설치 프로세스를 시작 합니다.

    ![설치 프로그램을 시작할 수 있는 권한을 요청 하는 사용자 계정 컨트롤](media/upgrade-2008r2-2012r2/start-setup-uac-box.png)

4. Windows Server 2012 R2 화면에서 **지금 설치**를 선택 합니다.

5. 인터넷에 연결 된 장치의 경우 **온라인으로 이동을 선택 하 여 지금 업데이트를 설치 합니다 (권장)** .

    ![중요 한 Windows 업데이트를 얻기 위해 온라인으로 전환 하도록 선택 하는 화면](media/upgrade-2008r2-2012r2/imp-updates-win-setup.png)

6. 설치 하려는 Windows Server 2012 R2 버전을 선택 하 고 **다음**을 선택 합니다.

    ![설치할 Windows Server 2012 R2 버전을 선택 하는 화면](media/upgrade-2008r2-2012r2/select-os-edition.png)

7. **사용 조건에 동의** 함을 선택 하 여 배포 채널 (예: 정품, 볼륨 라이선스, OEM, ODM 등)에 따라 사용권 계약의 약관에 동의한 후 **다음**을 선택 합니다.

    ![사용권 계약에 동의 하는 화면](media/upgrade-2008r2-2012r2/license-terms.png)

8. 업그레이드 **선택: Windows를 설치 하 고 파일, 설정 및 응용** 프로그램을 유지 하 여 전체 업그레이드를 선택 합니다.

    ![설치 유형을 선택 하는 화면](media/upgrade-2008r2-2012r2/choose-install-upgrade.png)

9. 설치 프로그램은 [Windows server 설치 및 업그레이드](https://docs.microsoft.com/windows-server/get-started/installation-and-upgrade) 문서의 정보를 사용 하 여 앱이 windows server 2012 r 2와 호환 되는지 확인 하 고 **다음**을 선택 합니다.

    ![앱 호환성을 확인 하는 화면이 표시 됩니다.](media/upgrade-2008r2-2012r2/compatibility-report.png)

10. 업그레이드가 권장 되지 않는다는 페이지가 표시 되 면이를 무시 하 고 **확인**을 선택할 수 있습니다. 이 파일은 새로 설치를 묻는 메시지를 표시 하기 위해 준비 되었지만 반드시 필요한 것은 아닙니다.

    ![업그레이드 진행률을 보여 주는 화면](media/upgrade-2008r2-2012r2/upgrading-windows-with-progress.png)

    현재 위치의 업그레이드를 시작 하 여 진행 중인 **Windows 업그레이드** 화면을 보여 줍니다. 업그레이드가 완료 되 면 서버가 다시 시작 됩니다.

## <a name="after-your-upgrade-is-done"></a>업그레이드가 완료 된 후

업그레이드가 완료 되 면 Windows Server 2012 r 2로의 업그레이드에 성공 했는지 확인 해야 합니다.

### <a name="to-make-sure-your-upgrade-was-successful"></a>업그레이드에 성공 했는지 확인 하려면

1. 레지스트리 편집기를 열고 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion hive로 이동 하 여 **ProductName**을 봅니다. Windows server **2012 R2 Datacenter**와 같은 windows Server 2012 r2 버전이 표시 되어야 합니다.

2. 모든 응용 프로그램이 실행 중이 고 응용 프로그램에 대 한 클라이언트 연결이 성공적인 지 확인 합니다.

업그레이드 하는 동안 문제가 발생할 수 있다고 생각 되는 `%SystemRoot%\Panther` 경우 (일반적으로 `C:\Windows\Panther`) 디렉터리를 복사 하 여 압축 하 고 Microsoft 지원에 문의 하세요.

## <a name="next-steps"></a>다음 단계

하나 이상의 업그레이드를 수행 하 여 Windows Server 2012 r 2에서 Windows Server 2019로 이동할 수 있습니다. 자세한 지침은 windows [server 2012 R2에서 Windows server 2019로 업그레이드](upgrade-2012r2-to-2019.md)를 참조 하세요.

## <a name="related-articles"></a>관련 문서

- Windows Server 2012 r 2에 대 한 자세한 내용 및 정보는 [Windows server 2012 r2 및 Windows server 2012](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh801901(v=ws.11))를 참조 하십시오.
