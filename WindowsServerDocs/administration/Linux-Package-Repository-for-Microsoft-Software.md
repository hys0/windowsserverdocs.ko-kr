---
title: Microsoft 제품에 대 한 Linux 소프트웨어 리포지토리
description: 이 문서에서는 Microsoft 제품에 대 한 Linux 소프트웨어 패키지를 사용 하 고 설치 하는 방법을 설명 합니다.
ms.prod: windows-server
manager: szark
ms.technology: compute
ms.topic: article
ms.assetid: b5387444-595f-4f38-abb7-163a70ea1895
author: szarkos
ms.author: szark
ms.date: 10/16/2017
ms.openlocfilehash: b57a1e7243f989a4529a666880572a9ceaa57644
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852066"
---
# <a name="linux-software-repository-for-microsoft-products"></a>Microsoft 제품에 대 한 Linux 소프트웨어 리포지토리

## <a name="overview"></a>개요
Microsoft는 Linux 시스템용으로 다양 한 소프트웨어 제품을 빌드 및 지원 하 고 표준 APT 및 YUM 패키지 리포지토리를 통해 사용할 수 있도록 합니다. 이 문서에서는 Linux 시스템에서 리포지토리를 구성 하는 방법에 대해 설명 합니다. 그러면 배포의 표준 패키지 관리 도구를 사용 하 여 Microsoft의 Linux 소프트웨어를 설치/업그레이드할 수 있습니다.

Microsoft의 Linux 소프트웨어 리포지토리는 여러 하위 리포지토리로 구성 되어 있습니다.

 - prod – 프로덕션 하위 리포지토리가 프로덕션에서 사용 하기 위한 패키지에 대해 지정 됩니다. Microsoft에서 제공 하는 해당 지원 계약 또는 프로그램의 조건에 따라 Microsoft에서 이러한 패키지를 상업적으로 지원 합니다.

 - mssql-server-Microsoft SQL Server on Linux에 대 한 패키지를 포함 합니다. 참고 항목: [SQL Server on Linux](https://www.microsoft.com/sql-server/sql-server-vnext-including-Linux).

> [!Note]
> Linux 소프트웨어 리포지토리의 패키지에는 패키지에 있는 사용 조건이 적용 됩니다. 패키지를 사용 하기 전에 사용 조건을 읽어 보십시오. 패키지를 설치 하 고 사용 하면 이러한 조건에 동의 하는 것입니다. 사용 조건에 동의 하지 않는 경우 패키지를 사용 하지 마십시오.


## <a name="configuring-the-repositories"></a>리포지토리 구성
Linux 배포 및 버전에 적용 되는 Linux 패키지를 설치 하 여 리포지토리를 자동으로 구성할 수 있습니다. 패키지는 서명 된 패키지 및/또는 리포지토리 메타 데이터의 유효성을 검사 하기 위해 apt/yum/zypper와 같은 도구에서 사용 하는 GPG 공개 키와 함께 리포지토리 구성을 설치 합니다.

### <a name="enterprise-linux-rhel-and-variants"></a>Enterprise Linux (RHEL 및 변형)

 - Enterprise Linux 6 (64.RPM)

        sudo rpm -Uvh https://packages.microsoft.com/config/rhel/6/packages-microsoft-prod.rpm

 - Enterprise Linux 7 (EL7)

        sudo rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm


### <a name="ubuntu"></a>Ubuntu

 - Ubuntu 14.04 (t)

        curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
        sudo apt-add-repository https://packages.microsoft.com/ubuntu/14.04/prod
        sudo apt-get update

 - Ubuntu 16.04 (Xenial)

        curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
        sudo apt-add-repository https://packages.microsoft.com/ubuntu/16.04/prod
        sudo apt-get update

 - Ubuntu 18.04 (Bionic)

         curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
        sudo apt-add-repository https://packages.microsoft.com/ubuntu/18.04/prod
        sudo apt-get update

 - Ubuntu 18.10 (우주)

         curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
        sudo apt-add-repository https://packages.microsoft.com/ubuntu/18.10/prod
        sudo apt-get update

 - Ubuntu 19.04 (Disco)

         curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
        sudo apt-add-repository https://packages.microsoft.com/ubuntu/19.04/prod
        sudo apt-get update

### <a name="suse-linux-enterprise-12"></a>SUSE Linux Enterprise 12

        sudo rpm -Uvh https://packages.microsoft.com/config/sles/12/packages-microsoft-prod.rpm


## <a name="manual-configuration"></a>수동 구성
리포지토리 구성 파일은 [packages.microsoft.com/config](https://packages.microsoft.com/config/)에서 사용할 수 있습니다. 다음 URI 명명 규칙을 사용 하 여 이러한 파일의 이름과 위치를 찾을 수 있습니다.

        https://packages.microsoft.com/config/<Distribution>/<Version>/prod.(repo|list)

**패키지 및 리포지토리 서명 키**

 - Microsoft의 GPG 공개 키를 여기에서 다운로드할 수 있습니다. [https://packages.microsoft.com/keys/microsoft.asc](https://packages.microsoft.com/keys/microsoft.asc)
 - 공개 키 ID: Microsoft (릴리스 서명) <gpgsecurity@microsoft.com>
 - 공개 키 지문: `BC52 8686 B50D 79E3 39D3 721C EB3E 94AD BE12 29CF`

### <a name="examples"></a>예제:

 - RHEL/CentOS 7

        # Install repository configuration
        curl https://packages.microsoft.com/config/rhel/7/prod.repo > ./microsoft-prod.repo
        sudo cp ./microsoft-prod.repo /etc/yum.repos.d/

        # Install Microsoft's GPG public key
        curl https://packages.microsoft.com/keys/microsoft.asc > ./microsoft.asc
        sudo rpm --import ./microsoft.asc

 - Ubuntu 16.04

        # Install repository configuration
        curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
        sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/

        # Install Microsoft GPG public key
        curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
        sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/



