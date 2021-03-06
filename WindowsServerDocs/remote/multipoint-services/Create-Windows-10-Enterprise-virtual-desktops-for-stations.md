---
title: 스테이션용 Windows 10 Enterprise 가상 데스크톱 만들기
description: 스테이션에 대해 Windows Server 2016 데스크톱을 만드는 방법 알아보기
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 63f08b5b-c735-41f4-b6c8-411eff85a4ab
author: evaseydl
ms.author: evas
manager: scottman
ms.openlocfilehash: 40af6ea98aa91730f78bde8a71f2ad9a741a6490
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859806"
---
# <a name="create-windows-10-enterprise-virtual-desktops-for-stations"></a>스테이션용 Windows 10 Enterprise 가상 데스크톱 만들기
MultiPoint 서비스에서이 옵션 구성은 필수 애플리케이션가 각 사용자에 대 한 클라이언트 운영 체제의 자체 인스턴스를 필요로 하는 경우에 주로 사용 됩니다. Windows 서버에 설치할 수 없는 애플리케이션 및 여러 인스턴스를 동일한 호스트 컴퓨터에서 실행 되지 않는 애플리케이션을 예로 들 수 있습니다.  
  
> [!NOTE]  
> 이러한 가상 데스크톱을 VDI 라고도 되므로 기본 MultiPoint 서비스 데스크톱 세션 보다 훨씬 더 많은 리소스 집약적 기본 MultiPoint 서비스 세션을 사용 하는 것이 좋습니다 가능한 경우.  
  
## <a name="prerequisites"></a>필수 조건  
시스템을 스테이션 가상 데스크톱 만들기, MultiPoint 서비스 하는지 확인 하도록 준비 하려면 다음 요구 사항을 충족 합니다.      
  
|하드웨어|요구 사항|         |
|------------|----------------|----------------| 
|CPU (멀티미디어)|1 코어 또는 가상 컴퓨터 별로 스레드|  
|솔리드 스테이트 드라이브 (SSD)|용량 > = 스테이션 당 20GB + 40GB MultiPoint 서비스 호스트 운영 체제에 대 한<p>임의 읽기\/쓰기 IOPS > 스테이션 당 3 K =|  
|RAM|Windows MultiPoint Server 호스트 운영 체제에 대 한 2GB + 2GB 스테이션|  
|그래픽|DX11|  
|BIOS|가상화 – SLAT 두 번째 수준 주소 변환 ()를 사용 하도록 구성 하는 BIOS CPU 설정|  
  
-   **스테이션** -MultiPoint 서비스 시스템에 대 한 스테이션을 설정 합니다. 자세한 내용은 참조 [추가 스테이션을 MultiPoint 서비스 연결](Attach-additional-stations-to-your-MultiPoint-services-computer.md)합니다.  
  
-   **도메인** -도메인 환경에서 Windows MultiPoint Server 컴퓨터에 추가한 도메인 및 도메인 사용자가 MultiPoint 서비스 호스트 운영 체제에서 로컬 관리자 그룹에 추가 되었습니다.  
  
## <a name="procedures"></a>절차  
다음 절차에 따라 수행할 수 있는 작업:  
  
-   [가상 데스크톱에 대 한 템플릿 만들기](#create-a-template-for-virtual-desktops)  
  
-   [템플릿에서 가상 데스크톱 만들기](#create-virtual-machine-desktops-from-the-template)  
  
-   [기존 가상 데스크톱 템플릿 복사](#copy-an-existing-virtual-desktop-template)  
  
### <a name="create-a-template-for-virtual-desktops"></a>가상 데스크톱 템플릿 만들기  
가상 데스크톱에 대 한 템플릿을 만들려면 MultiPoint Server의 가상 데스크톱 기능을 설정 해야 합니다.  
  
##### <a name="to-enable-the-virtual-desktop-feature"></a>가상 데스크톱 기능을 사용 하도록 설정 하려면  
  
1.  로컬 관리자 계정 또는 로컬 관리자 그룹의 구성원 인 도메인 계정으로 도메인에 MultiPoint 서버 호스트 운영 체제에 로그온 합니다.  
  
2.  **시작** 화면에서 MultiPoint 관리자를 엽니다.  
  
3.  클릭 된 **가상 데스크톱** 탭을 클릭 **가상 데스크톱을 사용 하도록 설정**, 클릭 하 고 **확인**, 시스템을 다시 시작 될 때까지 기다립니다.  
  
다음 단계에서는 가상 데스크톱 템플릿을 만드는 것입니다. 말 그대로 다중 포인트 관리자에 대 한 가상 데스크톱 스테이션을 만들려면 서식 파일로 사용할 수 있는 가상 하드 디스크 (VHD) 파일을 만듭니다. Windows에 대 한 실제 설치 미디어를 사용 하거나 또는 합니다. ISO 이미지 파일을 원본으로 서식 파일에 대 한 합니다. 또한 사용할 수는 있습니다. Windows 설치의 VHD를 제공 합니다. 실제 설치 디스크를 사용 하려면 삽입 해야 디스크 마법사를 시작 하기 전에 참고 합니다.  
  
##### <a name="to-create-a-virtual-desktop-template"></a>가상 데스크톱 템플릿을 만들려면  
  
1.  로컬 관리자 계정으로, 도메인, 로컬 관리자 그룹의 구성원 인 도메인 계정에서 MultiPoint 서버 호스트 운영 체제에 로그온 합니다.  
  
2.  **시작** 화면에서 MultiPoint 관리자를 엽니다.  
  
3.  클릭 하 고 **가상 데스크톱** 탭 합니다.  
  
4.   로컬 SSD을 Windows 10 Enterprise.iso 파일을 복사 합니다.  
  
5.  가상 데스크톱 탭 클릭 **가상 데스크톱 템플릿 만들기.**   
  
6.  **접두사**, 서식 파일 및 서식 파일을 사용 하 여 만든 가상 데스크톱을 식별 하는 데 접두사를 입력 합니다. 기본 접두사는 호스트 컴퓨터 이름입니다.  
  
    접두사는 템플릿 및 가상 데스크톱 스테이션의 이름을 지정하는 데 사용됩니다. 연결 된 템플릿은 수 <*접두사*>-t입니다. 가상 데스크톱 스테이션 이름은 <*접두사*>-*n*, 여기서 *n* 스테이션 식별자입니다.  
  
7.  사용자 이름 및 템플릿에 대 한 로컬 관리자 계정에 사용할 암호를 입력 합니다. 도메인에 로컬 관리자 그룹에 추가 될 도메인 계정의 자격 증명을 입력 합니다. 이 계정에 로그온 하는 템플릿 데 사용할 수 하 고 모든 가상 데스크톱 스테이션 템플릿에서 만든 키를 누릅니다.  
  
8. 클릭 **확인**, 템플릿 작성이 완료 될 때까지 기다립니다.  
  
9. 새 템플릿이 **가상 데스크톱** 탭에 나열 됩니다. 템플릿이 해제 됩니다.  
  
다음 단계에서는 소프트웨어 및 가상 데스크톱에서 원하는 설정을 사용 하 여 서식 파일을 구성 하는 것입니다. 서식 파일에서 모든 가상 데스크톱을 만들기 전에이 수행 해야 합니다.  
  
##### <a name="to-customize-a-virtual-desktop-template"></a>가상 데스크톱 템플릿을 사용자 지정 하려면  
  
1.  로컬 관리자 계정 또는 일부를 로컬 Administrators 그룹의 도메인 계정 사용 하 여 도메인에서 MultiPoint 서버 호스트 운영 체제에 로그온 합니다.  
  
2.  **시작** 화면에서 MultiPoint 관리자를 엽니다.  
  
3.  클릭 하 고 **가상 데스크톱** 탭 합니다.  
  
4.  사용자 지정, 클릭 하려는 템플릿을 선택 **사용자 지정 서식 파일**, 를 클릭 하 고 **확인**합니다.  
  
    > [!NOTE]  
    > 가상 데스크톱 스테이션을 만들려면 사용 되지 않은 템플릿을 사용할 수 있습니다. 이미 사용 중인 서식 파일을 업데이트 하려는 경우 서식 파일의 복사본을 사용 하 여 해야는 **템플릿 가져오기** 나중에 설명 된 작업에서 [기존 가상 데스크톱 템플릿 복사](#copy-an-existing-virtual-desktop-template)합니다.  
  
    Hyper-v에서 템플릿이 열립니다 **VM 연결** 창 및 자동 로그온 내장 된 Administrator 계정을 사용 하 여 수행 됩니다.  
  
5.  이 시점에서 애플리케이션 및 소프트웨어 업데이트를 설치 하 고, 설정을 변경 하 고, 관리자 프로필을 업데이트할 수 있습니다. 템플릿의 기본 제공 관리자 프로필에 대 한 모든 변경 내용은 템플릿에서 만든 가상 데스크톱 스테이션의 기본 사용자 프로필로 복사 됩니다.  
  
    도메인에 대 여 스테이션을 연결 하는 경우 로컬 사용자 계정을 만들고 사용자 지정 하는 동안 로컬 관리자 그룹에 추가 하는 것이 좋습니다.  
  
    > [!NOTE]  
    > 템플릿을 사용자 지정 하는 동안 시스템을 다시 시작 되 면 시스템이 다시 시작 후 자동 로그온 내장 된 Administrator 계정을 사용 하 여 실패할 수 있습니다. 사용자가 만든 로컬 관리자 계정을 사용 하 여 로그온 수동으로이 문제를 해결 하려면 기본 제공 관리자 계정의 암호를 변경, 로그 오프 한 다음 다시 로그온 기본 제공 관리자 계정 및 새 암호를 사용 하 여 합니다. (할 사용자가 로컬 관리자 계정을 사용 하 여 로그온 할 때 생성 된 프로필을 삭제 합니다.)  
  
6.  시스템 구성을 마친 후에는 관리자의 바탕 화면에서 **CompleteCustomization** 바로 가기를 두 번 클릭 하 여 Sysprep을 실행 한 다음 템플릿을 종료 합니다. 사용자 지정 하는 동안 Sysprep 도구는 이미지를 만들기 위해 Windows 설치를 준비 하려면 모든 고유한 시스템 정보를 제거 합니다.  
  
### <a name="create-virtual-machine-desktops-from-the-template"></a>템플릿에서 가상 컴퓨터 데스크톱 만들기  
가상 데스크톱 템플릿으로 수, 가상 데스크톱 만들기를 시작할 준비가 되었습니다. 데스크톱을 원하는 대로 구성 합니다. MultiPoint Server 컴퓨터에 연결 된 각 장치에 대 한 가상 데스크톱 만들어질 수 있습니다. 다음에 사용자를 스테이션에 로그온 하기 전에 표시 된 세션 기반 데스크톱 대신 가상 데스크톱이 표시 됩니다.  
  
> [!NOTE]  
> 이 절차는 MultiPoint Server 중인 경우에 적용 *스테이션 모드*합니다. 시스템에 있으면 *콘솔 모드*, 다중 포인트 관리자에서 스테이션 모드를 전환할 수 있습니다. 기본 MultiPoint 설정을 사용 하는 경우에 컴퓨터를 다시 시작 하 여 스테이션 모드를 시작할 수 있습니다. 기본적으로는 MultiPoint Server 컴퓨터가 항상 모드로 시작 스테이션  
  
##### <a name="to-create-virtual-desktops-for-your-stations"></a>프로그램 스테이션에 대 한 가상 데스크톱을 만들려면  
  
1.  Windows MultiPoint server (예: 원격 데스크톱 연결을 사용 하 여 Windows 컴퓨터)에서 원격 스테이션에서 로그온 한 로컬 관리자를 사용 하 여 계정 또는 도메인에 도메인 계정을 로컬 관리자 그룹입니다.  
  
    > [!NOTE]  
    > 또는 로컬 스테이션을 사용 하 여 서버에 로그온 할 수 있습니다. 그러나 스테이션 가상 데스크톱을 만들 때 로그 다른 스테이션 새 가상 데스크톱에 연결 하기 위해 가상 데스크톱을 만드는 데 사용한 하는 장치는 오프 해야 합니다.  
  
2.  **시작** 화면에서 MultiPoint 관리자를 엽니다.  
  
3.  컴퓨터가 콘솔 모드의 경우 스테이션 모드로 전환 합니다.  
  
    1.  에 **홈** 탭을 클릭 하 여 **스테이션 모드로 전환**합니다.  
  
    2.  컴퓨터 다시 시작 되 면 관리자로 로그인 합니다.  
  
4.  클릭 하 고 **가상 데스크톱** 탭 합니다.  
  
5.  가상 데스크톱 템플릿을 선택 하는 스테이션 사용, 클릭 하려는 **가상 데스크톱 스테이션을 만들**, 클릭 하 고 **확인**합니다.  
  
작업이 완료 되 면 각 로컬 장치는 가상 컴퓨터 기반의 가상 데스크톱에 연결 됩니다.  
  
> [!NOTE]  
> 사용자 계정을 로컬 스테이션 중 하나에 로그온 하는 경우에 새로 만든된 스테이션 가상 데스크톱의 하나에 연결 하려면 스테이션을 가져오려는 세션에서 로그 아웃 해야 합니다.  
  
### <a name="copy-an-existing-virtual-desktop-template"></a>기존 가상 데스크톱 템플릿 복사  
사용자 지정 하 고 사용할 수 있는 기존 가상 데스크톱 템플릿 복사본을 만들려면 다음 절차를 사용 합니다. 이 다음과 같은 상황에서 유용할 수 있습니다.  
  
-   복사할 마스터 템플릿 MultiPoint Server 호스트 컴퓨터에서 네트워크 공유에서 마스터 템플릿에서 가상 데스크톱 스테이션을 만들 수 있도록 합니다.  
  
-   현재 사용 중인 사용자 지정을 추가로 만들 수 있도록 하는 서식 파일의 복사본을 만듭니다.  
  
##### <a name="to-import-a-virtual-desktop-template"></a>가상 데스크톱 템플릿을 가져오려면  
  
1.  MultiPoint 서버에 관리자로 로그온 합니다.  
  
2.  **시작** 화면에서 MultiPoint 관리자를 엽니다.  
  
3.  클릭 하 고 **가상 데스크톱** 탭 합니다.  
  
4.  클릭 **가상 데스크톱 템플릿 가져오기**, 를 사용 하 여 **찾아보기** 가져올.vhd 파일 (템플릿)을 선택 합니다. 서식 파일을 가져올 때 원래.vhd 복사본이 이루어집니다. 기본적으로 MultiPoint 서비스에서는 c:에서.vhd 파일을 저장\\사용자\\공용\\문서\\하이퍼\-V\\가상 하드 디스크\\ 폴더입니다.  
  
5.  새 서식 파일에 대 한 접두사를 입력 한 다음 클릭 **확인**합니다.  
  
6.  를 하는 추가 로컬 서식 파일에 사용자 지정 하는 경우 접두사 이름 접두사의 끝에 버전 번호를 증분 하 여 변경할 수 있습니다. 또는 마스터 서식 파일을 가져오는 경우 기본 접두사 이름 끝에 마스터 서식 파일의 버전을 추가 하려는 수도 있습니다.  
  
7.  작업이 완료 되 면 템플릿을 사용자 지정할 수도 있고 스테이션을 만들려고 하는 사용할 수 있습니다.  
