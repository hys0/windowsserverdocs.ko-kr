---
title: 가상 데스크톱 관리
description: MultiPoint 서비스에서 가상 데스크톱 (VDI)를 관리 하는 방법 알아보기
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fa9ac0ed-47cb-4811-91ff-4fcb62d7858b
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 7afc6d2a65cd5cd3b116db5d65fd97e4cc770690
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861444"
---
# <a name="manage-virtual-desktops"></a>가상 데스크톱 관리
단일 컴퓨터 VDI를 사용 하면 각를 구성할 수 있습니다 *로컬* MultiPoint 서비스 스테이션이 스테이션과 동일한 MultiPoint 서비스 컴퓨터에서 Hyper-v 가상 컴퓨터 (VM)에서 실행 중인 Windows 10 Enterprise 게스트 운영 체제에 연결 합니다 스테이션 합니다. 이러한 가상 데스크톱 스테이션은 Windows 서버 버전에 설치할 수 없는 응용 프로그램을 사용하여 사용자 지정할 수 있습니다.  
  
## <a name="enable-the-virtual-desktop-feature"></a>가상 데스크톱 기능을 사용 하도록 설정  
  
1.  MultiPoint 관리자를 연 다음 **가상 데스크톱** 탭을 클릭합니다.  
  
2.  **VDI 작업**에서 **Create virtual desktop**(가상 데스크톱 만들기)을 클릭한 다음 Windows 10 Enterprise .iso 또는 VHD를 찾습니다.  
  
시스템이 다시 시작되며 이 작업은 몇 분 정도 걸릴 수 있습니다.  
  
## <a name="create-a-virtual-desktop-template"></a>가상 데스크톱 템플릿을 만들려면  
  
1.  MultiPoint 관리자를 연 다음 **가상 데스크톱** 탭을 클릭합니다.  
  
2.  **VDI 작업**에서 **Create virtual desktop**(가상 데스크톱 만들기)을 클릭한 다음 Windows 10 Enterprise .iso 또는 VHD를 찾습니다.  
  
    DVD를 사용하는 경우 프로그램이 Windows 10 Enterprise .wim 파일을 자동으로 찾습니다. 그러지 않으면 **찾아보기**를 클릭한 후 Windows 10 Enterprise .iso 또는 VHD 파일을 탐색합니다.  
  
    필요한 경우 접두사를 수정합니다. 기본적으로 호스트 컴퓨터 이름으로 설정됩니다.  
  
    > [!NOTE]  
    > 접두사는 템플릿 및 가상 데스크톱 스테이션의 이름을 지정하는 데 사용됩니다. 템플릿 이름은 접두사 \-t로 지정됩니다. 가상 데스크톱 스테이션의 이름은 접두사 \-*n*으로 지정됩니다. 여기서 *n*은 스테이션 ID입니다.  
  
4.  템플릿에서 생성된 모든 가상 스테이션 데스크톱에 로그온하는 데 사용되는 로컬 관리자 계정의 이름과 암호를 입력한 후 **확인**을 클릭합니다.  
  
    템플릿을 만드는 데는 몇 분 정도 걸립니다.  
      
    다음으로 가상 데스크 템플릿을 사용자 지정하는 방법을 알아봅니다.  
      
    > [!NOTE]  
    > MultiPoint Server가 도메인에 가입된 경우 대화 상자에 템플릿으로 만든 가상 컴퓨터가 도메인에 가입해야 하는지 여부를 지정할 수 있는 추가 필드가 있습니다.   
  
## <a name="import-a-virtual-desktop-template"></a>가상 데스크톱 템플릿 가져오기  
다른 MultiPoint Server에서 가상 데스크톱 템플릿을 만든 경우 다음 단계에 따라 해당 템플릿을 가져올 수 있습니다.  

1.  MultiPoint 관리자를 연 다음 **가상 데스크톱** 탭을 클릭합니다.  
  
2.  VDI 작업에서 **Create virtual desktop template**(가상 데스크톱 템플릿 가져오기)을 클릭합니다.  
  
3.  템플릿을 찾고 가져온 템플릿의 경로와 접두사를 정의합니다.  
  
## <a name="customize-the-virtual-desktop-template"></a>가상 데스크톱 템플릿 사용자 지정  
가상 데스크톱 템플릿을 만든 후에 응용 프로그램 및 소프트웨어 업데이트를 사용하여 템플릿을 사용자 지정하고 시스템 설정을 구성할 수 있습니다.   

1. MultiPoint 관리자를 연 다음 **가상 데스크톱** 탭을 클릭합니다.  
2. 가상 데스크톱 템플릿을 선택한 다음 **Customize virtual desktop template**(가상 데스크톱 템플릿 사용자 지정)을 클릭합니다.  
템플릿이 별도의 창에 열리고 가상 템플릿을 사용자 지정하는 가장 중요한 단계를 강조하는 추가 지침이 표시됩니다. 이러한 지침을 자세히 검토합니다.  
  
## <a name="create-virtual-desktop-stations"></a>가상 데스크톱 스테이션 만들기  
  
1.  MultiPoint 관리자를 스테이션 모드로 연 다음 **가상 데스크톱** 탭을 클릭합니다.  
  
    > [!NOTE]  
    > MultiPoint 서비스 시스템이 스테이션 모드로 실행되고 있지 않은 경우 이 절차를 완료하기 전에 먼저 시스템을 다시 시작합니다.  
  
2.  왼쪽에서 가상 데스크톱 템플릿을 선택\-창입니다. 템플릿 이름은 <접두사 -t>입니다.  
  
3.  템플릿 작업에서 **Create virtual desktop stations**(가상 데스크톱 스테이션 만들기)를 클릭한 다음 **확인**을 클릭합니다.  
  
    가상 데스크톱 스테이션을 만드는 프로세스는 몇 분 정도 걸립니다.  
  
    > [!NOTE]  
    > 로컬 스테이션이 현재 연결 되어 있는 경우 세션\-기반 가상 데스크톱, 로그 오프 해야 새로 만든된 가상 데스크톱 스테이션 중 하나에 연결 하려면 해당 스테이션 합니다.  
  
### <a name="validate-the-newly-created-customized-virtual-station-desktops"></a>새로 만든 사용자 지정 가상 스테이션 데스크톱의 유효성 검사  
  
로컬 관리자 계정 또는 도메인 계정을 사용 하 여 가상 데스크톱 스테이션 중 하나 이상에 로그온 하 여 사용자 지정된 가상 스테이션 데스크톱을 검증 하 고 확인 한 다음 새 VM\-기반된 가상 데스크톱이 작동 제대로 합니다.  
  
## <a name="disable-virtual-desktops"></a>가상 데스크톱 사용 안 함  
  
가상 데스크톱을 사용하지 않도록 설정하면 Hyper-V 기능이 해제됩니다. 모든 사용자가 로그오프되고 시스템이 다시 시작됩니다. 시스템이 다시 시작된 후 모든 가상 스테이션이 MultiPoint 로컬 세션에 할당됩니다.  

1. MultiPoint 관리자를 스테이션 모드로 연 다음 **가상 데스크톱** 탭을 클릭합니다.  
  
2. VDI 작업에서 **Disable virtual desktop**(가상 데스크톱 사용 안 함)을 클릭합니다. 