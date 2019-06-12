---
title: 가상 네트워크에 대 한 암호화 구성
description: "' 암호화 사용 합니다.'로 표시 하는 서브넷 내에서 서로 통신 하는 가상 컴퓨터 간에 가상 네트워크 트래픽의 암호화를 허용 하는 가상 네트워크 암호화"
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: 378213f5-2d59-4c9b-9607-1fc83f8072f1
ms.author: pashort
author: shortpatti
ms.date: 08/08/2018
ms.openlocfilehash: d2c09c83a227c5a75ff5b1b39b2ef6d1286bbfc8
ms.sourcegitcommit: cd12ace92e7251daaa4e9fabf1d8418632879d38
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66501558"
---
# <a name="configure-encryption-for-a-virtual-subnet"></a>가상 서브넷에 대 한 암호화 구성

>적용 대상: Windows Server

' 암호화 사용 합니다.'로 표시 하는 서브넷 내에서 서로 통신 하는 Vm 간에 가상 네트워크 트래픽의 암호화에 대 한 가상 네트워크 암호화 허용 또한 가상 서브넷의 DTLS(데이터그램 전송 계층 보안)를 활용하여 패킷을 암호화합니다. DTLS는 실제 네트워크에 액세스하는 누군가에 의한 도청, 변조 및 위조를 방지합니다.

가상 네트워크 암호화가 필요합니다.
- 암호화 인증서를 각 SDN 사용이 가능한 Hyper-v 호스트에 설치 합니다.
- 해당 인증서의 지문이 참조 네트워크 컨트롤러에서 사용 되는 자격 증명 개체입니다.
- 가상 네트워크 각각에서 구성 암호화를 요구 하는 서브넷을 포함 합니다.

서브넷에서 암호화를 사용 하도록 설정 하면 해당 서브넷 내의 모든 네트워크 트래픽은 일어날 수도 수 있습니다 하는 모든 응용 프로그램 수준 암호화 하는 것 외에도 자동으로 암호화 됩니다.  암호화 된 것으로 표시 하는 경우에, 서브넷 교차 하는 트래픽은 자동으로 암호화 되지 않은 전송 됩니다. 가상 네트워크 경계를 교차 하는 모든 트래픽은 전송 암호화 되지 않은 합니다.

>[!NOTE]
>현재 연결 또는 연결 된 나중에 트래픽 자동으로 암호화 가져옵니다 하는지 여부를 동일한 서브넷에 다른 VM과 통신 합니다.

>[!TIP]
>암호화 된 서브넷에만 통신 하도록 응용 프로그램을 제한 해야 하는 경우 액세스 제어 목록 (Acl)만 하 여 현재 서브넷 내의 통신을 허용 합니다. 자세한 내용은 [사용 하 여 액세스 제어 목록 (Acl) 데이터 센터 네트워크 트래픽 흐름을 관리 하려면](https://docs.microsoft.com/windows-server/networking/sdn/manage/use-acls-for-traffic-flow)합니다.


## <a name="step-1-create-the-encryption-certificate"></a>1단계. 암호화 인증서 만들기
각 호스트에는 암호화 인증서가 설치 되어 있어야 합니다. 모든 테 넌 트에 동일한 인증서를 사용 하거나 각 테 넌 트에 대 한 고유한 단일을 생성할 수 있습니다. 

1.  인증서를 생성 합니다.  

```
    $subjectName = "EncryptedVirtualNetworks"
    $cryptographicProviderName = "Microsoft Base Cryptographic Provider v1.0";
    [int] $privateKeyLength = 1024;
    $sslServerOidString = "1.3.6.1.5.5.7.3.1";
    $sslClientOidString = "1.3.6.1.5.5.7.3.2";
    [int] $validityPeriodInYear = 5;

    $name = new-object -com "X509Enrollment.CX500DistinguishedName.1"
    $name.Encode("CN=" + $SubjectName, 0)

    #Generate Key
    $key = new-object -com "X509Enrollment.CX509PrivateKey.1"
    $key.ProviderName = $cryptographicProviderName
    $key.KeySpec = 1 #X509KeySpec.XCN_AT_KEYEXCHANGE
    $key.Length = $privateKeyLength
    $key.MachineContext = 1
    $key.ExportPolicy = 0x2 #X509PrivateKeyExportFlags.XCN_NCRYPT_ALLOW_EXPORT_FLAG 
    $key.Create()

    #Configure Eku
    $serverauthoid = new-object -com "X509Enrollment.CObjectId.1"
    $serverauthoid.InitializeFromValue($sslServerOidString)
    $clientauthoid = new-object -com "X509Enrollment.CObjectId.1"
    $clientauthoid.InitializeFromValue($sslClientOidString)
    $ekuoids = new-object -com "X509Enrollment.CObjectIds.1"
    $ekuoids.add($serverauthoid)
    $ekuoids.add($clientauthoid)
    $ekuext = new-object -com "X509Enrollment.CX509ExtensionEnhancedKeyUsage.1"
    $ekuext.InitializeEncode($ekuoids)

    # Set the hash algorithm to sha512 instead of the default sha1
    $hashAlgorithmObject = New-Object -ComObject X509Enrollment.CObjectId
    $hashAlgorithmObject.InitializeFromAlgorithmName( $ObjectIdGroupId.XCN_CRYPT_HASH_ALG_OID_GROUP_ID, $ObjectIdPublicKeyFlags.XCN_CRYPT_OID_INFO_PUBKEY_ANY, $AlgorithmFlags.AlgorithmFlagsNone, "SHA512")


    #Request Certificate
    $cert = new-object -com "X509Enrollment.CX509CertificateRequestCertificate.1"

    $cert.InitializeFromPrivateKey(2, $key, "")
    $cert.Subject = $name
    $cert.Issuer = $cert.Subject
    $cert.NotBefore = (get-date).ToUniversalTime()
    $cert.NotAfter = $cert.NotBefore.AddYears($validityPeriodInYear);
    $cert.X509Extensions.Add($ekuext)
    $cert.HashAlgorithm = $hashAlgorithmObject
    $cert.Encode()

    $enrollment = new-object -com "X509Enrollment.CX509Enrollment.1"
    $enrollment.InitializeFromRequest($cert)
    $certdata = $enrollment.CreateRequest(0)
    $enrollment.InstallResponse(2, $certdata, 0, "")
```

스크립트를 실행 한 후 새 인증서에 표시를 내 저장소:

    PS D:\> dir cert:\\localmachine\my


    PSParentPath: Microsoft.PowerShell.Security\Certificate::localmachine\my

    Thumbprint                                Subject
    ----------                                -------
    84857CBBE7A1C851A80AE22391EB2C39BF820CE7  CN=MyNetwork
    5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks

2. 파일에 인증서를 내보냅니다.<p>인증서, 개인 키를 사용 하 여 하나 및 없는의 사본을 두 개 필요합니다.

```
   $subjectName = "EncryptedVirtualNetworks"
   $cert = Get-ChildItem cert:\localmachine\my | ? {$_.Subject -eq "CN=$subjectName"}
   [System.io.file]::WriteAllBytes("c:\$subjectName.pfx", $cert.Export("PFX", "secret"))
   Export-Certificate -Type CERT -FilePath "c:\$subjectName.cer" -cert $cert
```

3. 각 hyper-v 호스트에 인증서 설치 

   PS c:\> dir c:\$subjectname.*


~~~
    Directory: C:\


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        9/22/2017   4:54 PM            543 EncryptedVirtualNetworks.cer
-a----        9/22/2017   4:54 PM           1706 EncryptedVirtualNetworks.pfx
~~~

4. Hyper-v 호스트에서 설치

```
   $server = "Server01"

   $subjectname = "EncryptedVirtualNetworks"
   copy c:\$SubjectName.* \\$server\c$
   invoke-command -computername $server -ArgumentList $subjectname,"secret" {
       param (
           [string] $SubjectName,
           [string] $Secret
       )
       $certFullPath = "c:\$SubjectName.cer"

       # create a representation of the certificate file
       $certificate = new-object System.Security.Cryptography.X509Certificates.X509Certificate2
       $certificate.import($certFullPath)

       # import into the store
       $store = new-object System.Security.Cryptography.X509Certificates.X509Store("Root", "LocalMachine")
       $store.open("MaxAllowed")
       $store.add($certificate)
       $store.close()

       $certFullPath = "c:\$SubjectName.pfx"
       $certificate = new-object System.Security.Cryptography.X509Certificates.X509Certificate2
       $certificate.import($certFullPath, $Secret, "MachineKeySet,PersistKeySet")

       # import into the store
       $store = new-object System.Security.Cryptography.X509Certificates.X509Store("My", "LocalMachine")
       $store.open("MaxAllowed")
       $store.add($certificate)
       $store.close()

       # Important: Remove the certificate files when finished
       remove-item C:\$SubjectName.cer
       remove-item C:\$SubjectName.pfx
   }
```

5. 환경의 각 서버에 대해 반복 합니다.<p>각 서버에 대 한 반복을 한 후 루트 및 각 Hyper-v 호스트의 내 저장소에 설치 된 인증서를 사용 해야 합니다. 

6. 인증서의 설치를 확인 합니다.<p>내용을 확인 하 여 인증서를 확인 합니다 내 및 루트 인증서 저장소:

   PS c:\> 입력 pssession Server1

~~~
[Server1]: PS C:\> get-childitem cert://localmachine/my,cert://localmachine/root | ? {$_.Subject -eq "CN=EncryptedVirtualNetworks"}

PSParentPath: Microsoft.PowerShell.Security\Certificate::localmachine\my

Thumbprint                                Subject
----------                                -------
5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks


PSParentPath: Microsoft.PowerShell.Security\Certificate::localmachine\root

Thumbprint                                Subject
----------                                -------
5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks
~~~

7. 지문을 기록해 둡니다.<p>네트워크 컨트롤러에서 인증서 자격 증명 개체를 만들려면 필요 하기 때문에 지문 참고를 해야 합니다.

## <a name="step-2-create-the-certificate-credential"></a>2단계. 인증서 자격 증명 만들기

각 네트워크 컨트롤러에 연결 된 Hyper-v 호스트에 인증서를 설치한 후에 이제 사용 하 여 네트워크 컨트롤러를 구성 해야 합니다.  이 위해 네트워크 컨트롤러 PowerShell 모듈이 설치 된 컴퓨터에서 인증서 지문을 포함 하는 자격 증명 개체를 만들어야 합니다. 


    # Replace with thumbprint from your certificate
    $thumbprint = "5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6"  

    # Replace with your Network Controller URI
    $uri = "https://nc.contoso.com"

    Import-module networkcontroller

    $credproperties = new-object Microsoft.Windows.NetworkController.CredentialProperties
    $credproperties.Type = "X509Certificate"
    $credproperties.Value = $thumbprint
    New-networkcontrollercredential -connectionuri $uri -resourceid "EncryptedNetworkCertificate" -properties $credproperties -force

>[!TIP]
>암호화 된 각 가상 네트워크에 대해이 자격 증명을 다시 사용할 수 있습니다 하거나 배포 하 고 각 테 넌 트에 대 한 고유한 인증서를 사용할 수 있습니다.


## <a name="step-3-configuring-a-virtual-network-for-encryption"></a>3단계. 암호화에 대 한 Virtual Network 구성

이 단계를 이미 만든 가상 네트워크 이름 "My 네트워크" 하나 이상의 가상 서브넷 포함 가정 합니다.  가상 네트워크를 만드는 방법에 대 한 정보를 참조 하세요 [만들기, 삭제 또는 업데이트 테 넌 트 가상 네트워크](../Manage/Create,-Delete,-or-Update-Tenant-Virtual-Networks.md)합니다.

>[!NOTE]
>현재 연결 또는 연결 된 나중에 트래픽 자동으로 암호화 가져옵니다 하는지 여부를 동일한 서브넷에 다른 VM과 통신 합니다.

1.  네트워크 컨트롤러에서 가상 네트워크 및 자격 증명 개체를 검색 합니다.

    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "MyNetwork" $certcred = Get-NetworkControllerCredential -ConnectionUri $uri -ResourceId "EncryptedNetworkCertificate"

2.  인증서 자격 증명에 대 한 참조를 추가 하 고 개별 서브넷에서 암호화 사용

    $vnet.properties.EncryptionCredential = $certcred

    # <a name="replace-the-subnets-index-with-the-value-corresponding-to-the-subnet-you-want-encrypted"></a>서브넷 인덱스를 암호화 하려는 서브넷에 해당 하는 값을 바꿉니다.  
    # <a name="repeat-for-each-subnet-where-encryption-is-needed"></a>암호화가 필요한 각 서브넷에 대 한 반복
    $vnet.properties.Subnets[0].properties.EncryptionEnabled = $true

3.  네트워크 컨트롤러에 업데이트 된 가상 네트워크 개체를 넣어야 합니다.

    New-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId $vnet.ResourceId -Properties $vnet.Properties -force


_**축 하!** _ 다음이 단계를 완료 하면 완료 했습니다. 


## <a name="next-steps"></a>다음 단계



