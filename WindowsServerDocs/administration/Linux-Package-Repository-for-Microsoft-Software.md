---
title: Microsoft 제품용 Linux 소프트웨어 리포지토리에서
description: 이 문서에 사용 하 여 Microsoft 제품에 대 한 Linux 소프트웨어 패키지를 설치 하는 방법을 설명 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.service: na
manager: szark
ms.technology: compute
ms.topic: article
ms.assetid: b5387444-595f-4f38-abb7-163a70ea1895
author: szarkos
ms.author: szark
ms.date: 10/16/2017
ms.openlocfilehash: dbdbd0f436645f7e19c07e4f3278c5073636a547
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831864"
---
# <a name="linux-software-repository-for-microsoft-products"></a>Microsoft 제품용 Linux 소프트웨어 리포지토리에서

## <a name="overview"></a>개요
Microsoft은 소프트웨어 제품의 다양 한 Linux 시스템에 대 한 지원 및 표준 APT 및 YUM 패키지 리포지토리를 통해 사용할 수 있도록 작성 합니다. 이 문서는 있습니다 수 다음 설치/업그레이드 배포의 표준 패키지 관리 도구를 사용 하 여 Microsoft의 Linux 소프트웨어 있도록 Linux 시스템에 리포지토리를 구성 하는 방법을 설명 합니다.

Microsoft의 Linux 소프트웨어 리포지토리에서 여러 하위 저장소의 구성 됩니다.

 - prod-프로덕션 용도로 프로덕션 환경에서 사용 하는 패키지에 대 한 지정 된 하위 저장소입니다. 이러한 패키지는 해당 지원 계약 또는 Microsoft에 포함 된 프로그램의 조건에 따라 Microsoft에서 상업적으로 지원 됩니다.

 - mssql-server-이러한 리포지토리 패키지를 포함 Microsoft SQL Server Linux-참조에 대 한도: [Linux의 SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-vnext-including-Linux)합니다.

>[!Note]
Linux 소프트웨어 리포지토리에서 패키지를 패키지에 있는 사용 조건에 적용 됩니다. 패키지를 사용 하기 전에 사용 약관을 참조 하세요. 설치를 사용 하 여 패키지의 이러한 약관 수락 하는 것입니다. 사용 조건에 동의 하지 않는 경우에 패키지를 사용 하지 마십시오.


## <a name="configuring-the-repositories"></a>리포지토리 구성
리포지토리는 Linux 배포판 및 버전에 적용 되는 Linux 패키지를 설치 하 여 자동으로 구성할 수 있습니다. 패키지는 리포지토리 구성 하는 데 apt/yum/zypper와 같은 도구에서 서명 된 패키지 및/또는 저장소 메타 데이터의 유효성을 검사 GPG 공개 키와 함께 설치 합니다.

### <a name="enterprise-linux-rhel-and-variants"></a>Enterprise Linux (RHEL 및 변형)

 - Enterprise Linux 6 (EL6)

        sudo rpm -Uvh https://packages.microsoft.com/config/rhel/6/packages-microsoft-prod.rpm

 - Enterprise Linux 7 (EL7)

        sudo rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm


### <a name="ubuntu"></a>Ubuntu

 - Ubuntu 14.04 (신뢰할 수 있는)

        wget https://packages.microsoft.com/config/ubuntu/14.04/packages-microsoft-prod.deb
        sudo dpkg -i packages-microsoft-prod.deb
        sudo apt-get update

 - Ubuntu 16.04 (Xenial)

        wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb
        sudo dpkg -i packages-microsoft-prod.deb
        sudo apt-get update

 - Ubuntu 16.10 (Yakkety)

        wget https://packages.microsoft.com/config/ubuntu/16.10/packages-microsoft-prod.deb
        sudo dpkg -i packages-microsoft-prod.deb
        sudo apt-get update


### <a name="suse-linux-enterprise-12"></a>SUSE Linux Enterprise 12

        sudo rpm -Uvh https://packages.microsoft.com/config/sles/12/packages-microsoft-prod.rpm


## <a name="manual-configuration"></a>수동 구성
리포지토리 구성 파일에서 사용할 [packages.microsoft.com/config](https://packages.microsoft.com/config/)합니다. 이러한 파일의 위치와 이름을 다음 URI 명명 규칙을 사용 하 여 찾을 수 있습니다.

        https://packages.microsoft.com/config/<Distribution>/<Version>/prod.(repo|list)

**패키지 및 리포지토리 서명 키**

 - 여기 Microsoft GPG 공개 키를 다운로드할 수 있습니다. [https://packages.microsoft.com/keys/microsoft.asc](https://packages.microsoft.com/keys/microsoft.asc)
 - 공용 키 ID: Microsoft (릴리스 서명) <gpgsecurity@microsoft.com>
 - 공개 키 지문: `BC52 8686 B50D 79E3 39D3 721C EB3E 94AD BE12 29CF`

### <a name="examples"></a>예를 들면 다음과 같습니다.

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



