---
title: 컨테이너 네트워킹 개요
description: 이 항목 네트워킹 스택 컨테이너 Windows에 대 한 개요 이며 만들기 구성 하 고 관리 컨테이너 네트워크에 대 한 추가 지침은에 대 한 링크를 포함 합니다.
manager: ravirao
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 318659e5-e4a5-4e46-99d6-211dfc46f6b8
ms.author: pashort
author: jmesser81
ms.openlocfilehash: fd2f022948208d4aacce2994ff053e77384b28fc
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="container-networking-overview"></a>컨테이너 네트워킹 개요

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 네트워킹 스택 컨테이너 Windows에 대 한 개요 이며 만들기 구성 하 고 관리 컨테이너 네트워크에 대 한 추가 지침은에 대 한 링크를 포함 합니다.

Windows Server 컨테이너는 동일한 컨테이너 호스트에서 실행 되는 다른 서비스와에서 응용 프로그램 또는 서비스를 분리 하는 데 사용 하는 무게는 가벼우며 운영 체제 virtualization 방법입니다. 이 실현 하기 각 컨테이너 운영 체제, 프로세스, 파일 시스템, 레지스트리 및 IP 주소 고유한 보기를 있습니다.

Windows 가상 컴퓨터 네트워킹 관련에서 유사 하 게 컨테이너 기능이 합니다. 각 컨테이너 인바인드 및 아웃 바운드 교통 전달 되는 가상 스위치를에 연결 되어 있는 가상 네트워크 어댑터를 있습니다. 격리 같은 호스트에 컨테이너 사이 적용 하려면 각 Windows Server, Hyper-v 컨테이너 컨테이너 네트워크 어댑터는 설치에 네트워크 삽입 생성 됩니다. Windows Server 컨테이너 호스트 vNIC를 사용 하 여 가상 스위치를 연결. Hyper-v 컨테이너 합성 VM NIC (유틸리티 VM에 나타나지)를 사용 하 여 가상 스위치를 연결. 

컨테이너 끝점 호스트 로컬 네트워크 (예: NAT), 실제 네트워크 또는 Microsoft 소프트웨어 정의 네트워킹 (SDN) 스택 통해 생성 오버레이 가상 네트워크에 연결할 수 있습니다. 

작성 하 고 관리 오버레이/SDN 비 배포용 컨테이너 네트워크에 대 한 자세한 내용은 참조는 [Windows 컨테이너 네트워킹](https://msdn.microsoft.com/en-us/virtualization/windowscontainers/management/container_networking) msdn 가이드 합니다.

작성 하 고 관리 SDN 있는 모든 가상 네트워크 오버레이 컨테이너 네트워크에 대 한 자세한 내용은 참조 [컨테이너 끝점 테 가상 네트워크에 연결](../../manage/Connect-container-endpoints-to-a-Tenant-Virtual-Network.md)합니다. 