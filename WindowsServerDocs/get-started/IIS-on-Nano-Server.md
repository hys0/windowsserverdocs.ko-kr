---
title: Nano Server의 IIS
description: Nano 서버의 IIS 구성에 대한 세부 정보
ms.prod: windows-server
ms.service: na
manager: DonGill
ms.technology: server-nano
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 09/06/2017
ms.assetid: 16984724-2d77-4d7b-9738-3dff375ed68c
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: 04c2d7eab2f149505758ab21f08cd6b8bdb74b85
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71360297"
---
# <a name="iis-on-nano-server"></a>Nano Server의 IIS

>적용 대상: Windows Server 2016

> [!IMPORTANT]
> Windows Server, 버전 1709부터 [컨테이너 기본 OS 이미지](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image)로만 Nano 서버를 사용할 수 있습니다. [Nano 서버 변경 사항](nano-in-semi-annual-channel.md)을 확인하여 그 의미를 알아보세요. 

Microsoft-NanoServer-IIS-Package와 함께 -Package 매개 변수를 사용하여 Nano 서버에 IIS(인터넷 정보 서비스) 서버 역할을 설치할 수 있습니다. 패키지 설치를 포함하여 Nano 서버를 구성하는 방법에 대한 정보는 [Nano 서버 설치](Getting-Started-with-Nano-Server.md)를 참조하세요.  

이 Nano 서버 릴리스에는 다음 IIS 기능이 제공됩니다.  

|기능|기본적으로 사용하도록 설정됨|  
|-----------|----------------------|  
|**일반적인 HTTP 기능**||  
|기본 문서|x|  
|디렉터리 검색|x|  
|HTTP 오류|x|  
|정적 콘텐츠|x|  
|HTTP 리디렉션||  
|**상태 및 진단**||  
|HTTP 로깅|x|  
|사용자 지정 로깅||  
|요청 모니터||  
|추적||  
|**성능**||  
|정적 콘텐츠 압축|x|  
|정적 콘텐츠 압축||  
|**보안**||  
|요청 필터링|x|  
|기본 인증||  
|클라이언트 인증서 매핑 인증||  
|다이제스트 인증||  
|IIS 클라이언트 인증서 매핑 인증||  
|IP 및 도메인 제한||  
|URL 권한 부여||  
|Windows 인증||  
|**애플리케이션 개발**||  
|응용 프로그램 초기화||  
|CGI||  
|ISAPI 확장||  
|ISAPI 필터||  
|SSI(Server Side Include)||  
|WebSocket 프로토콜||  
|**관리 도구**||  
|Windows PowerShell용 IIS 관리 모듈|x|  

IIS의 다른 구성(예: ASP.NET, PHP 및 Java 사용)과 기타 관련 콘텐츠에 대한 문서는 [http://iis.net/learn](http://iis.net/learn)에 게시되어 있습니다.  

## <a name="installing-iis-on-nano-server"></a>Nano 서버에 IIS 설치  
이 서버 역할을 오프라인으로(Nano 서버를 끄고) 설치할 수도 있고 온라인으로(Nano 서버가 실행 중인 상태로) 설치할 수도 있지만 오프라인 설치를 권장합니다.  

오프라인 설치의 경우 이 예제와 같이 New-NanoServerImage의 -Packages 매개 변수를 사용하여 패키지를 추가합니다.  

`New-NanoServerImage -Edition Standard -DeploymentType Guest -MediaPath f:\ -BasePath .\Base -TargetPath .\Nano1.vhd -ComputerName Nano1 -Package Microsoft-NanoServer-IIS-Package`  

기존 VHD 파일이 있는 경우 VHD를 탑재한 다음 **Add-Package** 옵션을 사용하여 오프라인으로 DISM.exe를 통해 IIS를 설치할 수 있습니다.   
다음 예제 단계는 BasePath 옵션에 지정된 디렉터리에서 실행하는 것으로 가정합니다. 이 디렉터리는 New-NanoServerImage를 실행하여 생성된 것입니다.  

1.  mkdir mountdir
2.  .\Tools\dism.exe /Mount-Image /ImageFile:.\NanoServer.vhd /Index:1 /MountDir:.\mountdir
3.  .\Tools\dism.exe /Add-Package /PackagePath:.\packages\Microsoft-NanoServer-IIS-Package.cab /Image:.\mountdir
4.  .\Tools\dism.exe /Add-Package /PackagePath:.\packages\en-us\Microsoft-NanoServer-IIS-Package_en-us.cab /Image:.\mountdir
5.  .\Tools\dism.exe /Unmount-Image /MountDir:.\MountDir /Commit


> [!NOTE]  
> 4단계에서는 언어 팩을 추가합니다. 이 예제에서는 EN-US를 설치합니다.  

이제 IIS를 사용하여 Nano 서버를 시작할 수 있습니다.  

### <a name="installing-iis-on-nano-server-online"></a>온라인으로 Nano 서버에 IIS 설치  
서버 역할은 오프라인으로 설치하는 것이 좋지만, 컨테이너 시나리오에서 온라인으로(Nano 서버가 실행 중인 상태로) 설치해야 할 수도 있습니다. 이렇게 하려면 다음 단계를 따르십시오.  

1.  설치 미디어의 패키지 폴더를 실행 중인 Nano 서버에(예: C:\packages) 로컬로 복사합니다.  

2.  다른 컴퓨터에서 새 Unattend.xml 파일을 만들어 Nano 서버에 복사합니다. 이 XML 콘텐츠를 복사하여 새로 만든 XML 파일에 붙여 넣습니다.  



```  

    <unattend xmlns="urn:schemas-microsoft-com:unattend">  
    <servicing>  
        <package action="install">  
            <assemblyIdentity name="Microsoft-NanoServer-IIS-Package" version="10.0.14393.0" processorArchitecture="amd64" publicKeyToken="31bf3856ad364e35" language="neutral" />  
            <source location="c:\packages\Microsoft-NanoServer-IIS-Package.cab" />  
        </package>  
        <package action="install">  
            <assemblyIdentity name="Microsoft-NanoServer-IIS-Package" version="10.0.14393.0" processorArchitecture="amd64" publicKeyToken="31bf3856ad364e35" language="en-US" />  
            <source location="c:\packages\en-us\Microsoft-NanoServer-IIS-Package_en-us.cab" />  
        </package>  
    </servicing>  
    <cpi:offlineImage cpi:source="" xmlns:cpi="urn:schemas-microsoft-com:cpi" />  
</unattend>  
```  




3. 새로 만든(또는 복사한) XML 파일에서, \packages를 패키지 콘텐츠를 복사한 디렉터리로 편집합니다.  

4. 새로 만든 XML 파일이 있는 디렉터리로 전환하고 다음 명령을 실행합니다.  

   **dism /online /apply-unattend:.\unattend.xml**  


5. 다음 명령을 실행하여 IIS 패키지와 관련 언어 팩이 올바르게 설치되었는지 확인합니다.  

   **dism /online /get-packages**  

   "패키지 ID: Microsoft-NanoServer-IIS-Package~31bf3856ad364e35~amd64~~10.0.14393.1000"이 두 번 나열되고, 릴리스 유형: 언어 팩이 한 번 나열되고, 릴리스 유형: 기능 팩이 한 번 나열되어야 합니다.  

6. **net start w3svc**를 사용하여 또는 Nano 서버를 다시 시작하여 W3SVC 서비스를 시작합니다.  

## <a name="starting-iis"></a>IIS 시작  
IIS가 설치되어 실행되면 웹 요청을 처리할 준비가 완료된 것입니다. http://\<Nano 서버 IP 주소>에서 기본 IIS 웹 페이지를 검색하여 IIS가 실행 중인지 확인합니다. 물리적 컴퓨터에서 복구 콘솔을 사용하여 IP 주소를 확인할 수 있습니다. 가상 머신에서 Windows PowerShell 프롬프트를 사용하고 다음 명령을 실행하여 IP 주소를 얻을 수 있습니다.  

`Get-VM -name <VM name> | Select -ExpandProperty networkadapters | select IPAddresses`  

기본 IIS 웹 페이지에 액세스할 수 없는 경우 Nano 서버의 **c:\inetpub** 디렉터리를 검색하여 IIS 설치를 두 번 클릭합니다.  

## <a name="enabling-and-disabling-iis-features"></a>IIS 기능 설정 및 해제  
IIS 역할을 설치하면 기본적으로 다양한 IIS 기능이 활성화됩니다(이 토픽의 "Nano 서버의 IIS 개요" 섹션에 제공되는 테이블 참조). DISM.exe를 사용하여 추가 기능을 설정하거나 해제할 수 있습니다.

IIS의 각 기능은 구성 요소 집합으로 존재합니다. 예를 들어 Windows 인증 기능은 다음 요소를 구성합니다.  

|섹션|구성 요소|  
|-----------|--------------------------|  
|`<globalModules>`|`<add name="WindowsAuthenticationModule" image="%windir%\System32\inetsrv\authsspi.dll`|  
|`<modules>`|`<add name="WindowsAuthenticationModule" lockItem="true" \/>`|  
|`<windowsAuthentication>`|`<windowsAuthentication enabled="false" authPersistNonNTLM\="true"><providers><add value="Negotiate" /><add value="NTLM" /><br /></providers><br /></windowsAuthentication>`|  

IIS 하위 기능 전체 집합은 이 토픽의 부록 1에 포함되어 있고 해당 구성 요소는 이 토픽의 부록 2에 포함되어 있습니다.  


### <a name="example-installing-windows-authentication"></a>예: Windows 인증 설치  

1.  Nano 서버에서 Windows PowerShell 원격 세션 콘솔을 엽니다.  

2.  `DISM.exe`를 사용하여 Windows 인증 모듈을 엽니다.

    ```
    dism /Enable-Feature /online /featurename:IIS-WindowsAuthentication /all
    ```

    `/all` 스위치는 사용자가 선택한 기능이 의존하는 모든 기능을 설치합니다.

### <a name="example-uninstalling-windows-authentication"></a>예: Windows 인증 제거  

1.  Nano 서버에서 Windows PowerShell 원격 세션 콘솔을 엽니다.  

2.  `DISM.exe`를 사용하여 Windows 인증 모듈을 제거합니다.

    ```
    dism /Disable-Feature /online /featurename:IIS-WindowsAuthentication
    ```

## <a name="other-common-iis-configuration-tasks"></a>기타 일반적인 IIS 구성 작업  
**웹 사이트 만들기**  

이 cmdlet을 사용합니다.  

`PS D:\> New-IISSite -Name TestSite -BindingInformation "*:80:TestSite" -PhysicalPath c:\test`  

그런 다음 `Get-IISSite`를 실행하여 사이트 상태를 확인할 수 있습니다(웹 사이트 이름, ID, 상태, 실제 경로 및 바인딩을 반환).  

**웹 사이트 삭제**  

`Remove-IISSite -Name TestSite -Confirm:$false`을 실행합니다.  

**가상 디렉터리 만들기**  

Get-IISServerManager 매개 변수가 반환하는 IISServerManager 개체를 사용하여 가상 디렉터리를 만들 수 있습니다. 이 개체는 .NET Microsoft.Web.Administration.ServerManager API를 노출합니다. 이 예제에서, 다음 명령은 사이트 컬렉션의 "기본 웹 사이트" 요소 및 애플리케이션 섹션의 루트 애플리케이션 요소("/")에 액세스합니다. 그런 다음 해당 응용 프로그램 요소에 대한 VirtualDirectories 컬렉션의 Add() 메서드를 호출하여 새 디렉터리를 만듭니다.  

```  
PS C:\> $sm = Get-IISServerManager  
PS C:\> $sm.Sites["Default Web Site"].Applications["/"].VirtualDirectories.Add("/DemoVirtualDir1", "c:\test\virtualDirectory1")  
PS C:\> $sm.Sites["Default Web Site"].Applications["/"].VirtualDirectories.Add("/DemoVirtualDir2", "c:\test\virtualDirectory2")  
PS C:\> $sm.CommitChanges()  
```  

**애플리케이션 풀 만들기**  

마찬가지로 Get-IISServerManager를 사용하여 응용 프로그램 풀을 만들 수 있습니다.  

```  
PS C:\> $sm = Get-IISServerManager  
PS C:\> $sm.ApplicationPools.Add("DemoAppPool")  
```  

**HTTPS 및 인증서 구성**  

Nano 서버에서 웹 사이트에 대한 HTTPS를 구성하는 방법을 보여 주는 이 예제처럼, Certoc.exe 유틸리티를 사용하여 인증서를 가져옵니다.  

1.  Nano 서버를 실행하지 않는 다른 컴퓨터에서 인증서를 만들어서(사용자 고유의 인증서 이름 및 암호 사용) c:\temp\test.pfx로 내보냅니다.  

    `$newCert = New-SelfSignedCertificate -DnsName "www.foo.bar.com" -CertStoreLocation cert:\LocalMachine\my`  

    `$mypwd = ConvertTo-SecureString -String "YOUR_PFX_PASSWD" -Force -AsPlainText`  

    `Export-PfxCertificate -FilePath c:\temp\test.pfx -Cert $newCert -Password $mypwd`  

2.  test.pfx 파일을 Nano 서버 컴퓨터로 복사합니다.  

3.  Nano 서버에서, 다음 명령을 사용하여 "내" 저장소로 인증서를 가져옵니다.  

    **certoc.exe -ImportPFX -p YOUR_PFX_PASSWD My c:\temp\test.pfx**  

4.  `Get-ChildItem Cert:\LocalMachine\my`를 사용하여 이 새 인증서의 지문을 검색합니다(이 예에서는 61E71251294B2A7BB8259C2AC5CF7BA622777E73).  

5.  다음 Windows PowerShell 명령을 사용하여 기본 웹 사이트(또는 바인딩을 추가하려면 웹 사이트)에 HTTPS 바인딩을 추가합니다.  

    ```  
    $certificate = get-item Cert:\LocalMachine\my\61E71251294B2A7BB8259C2AC5CF7BA622777E73  
    # Use your actual thumbprint instead of this example  
    $hash = $certificate.GetCertHash()  

    Import-Module IISAdministration  
    $sm = Get-IISServerManager  
    $sm.Sites["Default Web Site"].Bindings.Add("*:443:", $hash, "My", "0")    # My is the certificate store name  
    $sm.CommitChanges()  
    ```  

    또한 다음 구문을 통해 특정 호스트 이름으로 SNI(서버 이름 표시)를 사용할 수 있습니다. `$sm.Sites["Default Web Site"].Bindings.Add("*:443:www.foo.bar.com", $hash, "My", "Sni".`  

## <a name="appendix-1-list-of-iis-sub-features"></a>부록 1: IIS 하위 기능 목록

- IIS-웹 서버
- IIS-일반적인 Http 기능
- IIS-정적 콘텐츠
- IIS-기본 문서
- IIS-디렉터리 검색
- IIS-Http 오류
- IIS-Http 리디렉션
- IIS-애플리케이션 개발
- IIS-CGI
- IIS-ISAPI 확장
- IIS-ISAPI 필터
- IIS-SSI(Server Side Include)
- IIS-WebSocket
- IIS-애플리케이션 초기화
- IIS-보안
- IIS-기본 인증
- IIS-Windows 인증
- IIS-다이제스트 인증
- IIS-클라이언트 인증서 매핑 인증
- IIS-IIS 인증서 매핑 인증
- IIS-URL 권한 부여
- IIS-요청 필터링
- IIS-IP 보안
- IIS-인증서 공급자
- IIS-성능
- IIS-Http 정적 압축
- IIS-Http 동적 압축
- IIS-상태 및 진단
- IIS-Http 로깅
- IIS-로깅 라이브러리
- IIS-요청 모니터
- IIS-Http 추적
- IIS-사용자 지정 로깅

## <a name="appendix-2-elements-of-http-features"></a>부록 2: HTTP 기능의 요소  
IIS의 각 기능은 구성 요소 집합으로 존재합니다. 이 부록에는 이 Nano 서버 릴리스의 모든 기능에 대한 구성 요소가 나열되어 있습니다.  

### <a name="common-http-features"></a>일반적인 HTTP 기능  
**기본 문서**  

|섹션|구성 요소|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name="DefaultDocumentModule" image="%windir%\System32\inetsrv\defdoc.dll" />`|  
|`<modules>`|`<add name="DefaultDocumentModule" lockItem="true" />`|  
|`<handlers>`|`<add name="StaticFile" path="*" verb="*" modules="DefaultDocumentModule" resourceType="EiSecther" requireAccess="Read" />`|  
|`<defaultDocument>`|`<defaultDocument enabled="true"><br /><files><br /> <add value="Default.htm" /><br />        <add value="Default.asp" /><br />        <add value="index.htm" /><br />        <add value="index.html" /><br />        <add value="iisstart.htm" /><br />    </files><br /></defaultDocument>`|  

`StaticFile <handlers>` 항목이 이미 존재할 수 있습니다. 만약 그렇다면 \<모듈 > 특성에 "DefaultDocumentModule"을 추가하고 쉼표로 구분합니다.  

**디렉터리 검색**  

|섹션|구성 요소|  
|----------------|--------------------------|   
|`<globalModules>`|`<add name="DirectoryListingModule" image="%windir%\System32\inetsrv\dirlist.dll" />`|  
|`<modules>`|`<add name="DirectoryListingModule" lockItem="true" />`|  
|`<handlers>`|`<add name="StaticFile" path="*" verb="*" modules="DirectoryListingModule" resourceType="Either" requireAccess="Read" />`|  

`StaticFile <handlers>` 항목이 이미 존재할 수 있습니다. 만약 그렇다면 \<모듈 > 특성에 "DirectoryListingModule"을 추가하고 쉼표로 구분합니다.  

**HTTP 오류**  

|섹션|구성 요소|  
|----------------|--------------------------|   
|`<globalModules>`|`<add name="CustomErrorModule" image="%windir%\System32\inetsrv\custerr.dll" />`|  
|`<modules>`|`<add name="CustomErrorModule" lockItem="true" />`|  
|`<httpErrors>`|`<httpErrors lockAttributes="allowAbsolutePathsWhenDelegated,defaultPath"><br />    <error statusCode="401"    prefixLanguageFilePath="%SystemDrive%\inetpub\custerr" path="401.htm" ><br />    <error statusCode="403" prefixLanguageFilePath="%SystemDrive%\inetpub\custerr" path="403.htm" /><br />    <error statusCode="404" prefixLanguageFilePath="%SystemDrive%\inetpub\custerr" path="404.htm" /><br />    <error statusCode="405" prefixLanguageFilePath="%SystemDrive%\inetpub\custerr" path="405.htm" /><br />    <error statusCode="406" prefixLanguageFilePath="%SystemDrive%\inetpub\custerr" path="406.htm" /><br />    <error statusCode="412" prefixLanguageFilePath="%SystemDrive%\inetpub\custerr" path="412.htm" /><br />    <error statusCode="500" prefixLanguageFilePath="%SystemDrive%\inetpub\custerr" path="500.htm" /><br />    <error statusCode="501" prefixLanguageFilePath="%SystemDrive%\inetpub\custerr" path="501.htm" /><br />    <error statusCode="502" prefixLanguageFilePath="%SystemDrive%\inetpub\custerr" path="502.htm" /><br /></httpErrors>`|  

**정적 콘텐츠**  

|섹션|구성 요소|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name="StaticFileModule" image="%windir%\System32\inetsrv\static.dll" />`|  
|`<modules>`|`<add name="StaticFileModule" lockItem="true" />`|  
|`<handlers>`|`<add name="StaticFile" path="*" verb="*" modules="StaticFileModule" resourceType="Either" requireAccess="Read" />`|  

`StaticFile \<handlers>` 항목이 이미 존재할 수 있습니다. 만약 그렇다면 \<모듈 > 특성에 "StaticFileModule"을 추가하고 쉼표로 구분합니다.  

**HTTP 리디렉션**  

|섹션|구성 요소|  
|----------------|--------------------------|    
|`<globalModules>`|`<add name="HttpRedirectionModule" image="%windir%\System32\inetsrv\redirect.dll" />`|  
|`<modules>`|`<add name="HttpRedirectionModule" lockItem="true" />`|  
|`<httpRedirect>`|`<httpRedirect enabled="false" />`|  

### <a name="health-and-diagnostics"></a>상태 및 진단  
**HTTP 로깅**  

|섹션|구성 요소|  
|----------------|--------------------------|   
|`<globalModules>`|`<add name="HttpLoggingModule" image="%windir%\System32\inetsrv\loghttp.dll" />`|  
|`<modules>`|`<add name="HttpLoggingModule" lockItem="true" />`|  
|`<httpLogging>`|`<httpLogging dontLog="false" />`|  

**사용자 지정 로깅**  

|섹션|구성 요소|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name="CustomLoggingModule" image="%windir%\System32\inetsrv\logcust.dll" />`|  
|`<modules>`|`<add name="CustomLoggingModule" lockItem="true" />`|  

**요청 모니터**  

|섹션|구성 요소|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name="RequestMonitorModule" image="%windir%\System32\inetsrv\iisreqs.dll" />`|  

**추적**  

|섹션|구성 요소|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name="TracingModule" image="%windir%\System32\inetsrv\iisetw.dll" \/><br /><add name="FailedRequestsTracingModule" image="%windir%\System32\inetsrv\iisfreb.dll" />`|  
|`<modules>`|`<add name="FailedRequestsTracingModule" lockItem="true" />`|  
|`<traceProviderDefinitions>`|`<traceProviderDefinitions><br />    <add name="WWW Server" guid\="{3a2a4e84-4c21-4981-ae10-3fda0d9b0f83}"><br />        <areas><br />            <clear /><br />            <add name="Authentication" value="2" /><br />            <add name="Security" value="4" /><br />            <add name="Filter" value="8" /><br />            <add name="StaticFile" value="16" /><br />            <add name="CGI" value="32" /><br />            <add name="Compression" value="64" /><br />            <add name="Cache" value="128" /><br />            <add name="RequestNotifications" value="256" /><br />            <add name="Module" value="512" /><br />            <add name="FastCGI" value="4096" /><br />            <add name="WebSocket" value="16384" /><br />        </areas><br />    </add><br />    <add name="ISAPI Extension" guid="{a1c2040e-8840-4c31-ba11-9871031a19ea}"><br />        <areas><br />            <clear /><br />        </areas><br />    </add><br /></traceProviderDefinitions>`|  

### <a name="performance"></a>성능  
**정적 콘텐츠 압축**  

|섹션|구성 요소|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name="StaticCompressionModule" image="%windir%\System32\inetsrv\compstat.dll" />`|  
|`<modules>`|`<add name="StaticCompressionModule" lockItem="true" />`|  
|`<httpCompression>`|`<httpCompression directory="%SystemDrive%\inetpub\temp\IIS Temporary Compressed Files"><br />    <scheme name="gzip" dll="%Windir%\system32\inetsrv\gzip.dll" /><br />   <staticTypes><br />        <add mimeType="text/*" enabled="true" /><br />        <add mimeType="message/*" enabled="true" /><br />        <add mimeType="application/javascript" enabled="true" \/><br />        <add mimeType="application/atom+xml" enabled="true" /><br />        <add mimeType="application/xaml+xml" enabled="true" /><br />        <add mimeType="\*\*" enabled="false" /><br />    </staticTypes><br /></httpCompression>`|  

**동적 콘텐츠 압축**  

|섹션|구성 요소|  
|-----------|--------------------------|  
|`<globalModules>`|`<add name="DynamicCompressionModule" image="%windir%\System32\inetsrv\compdyn.dll" />`|  
|`<modules>`|`<add name="DynamicCompressionModule" lockItem="true" />`|  
|`<httpCompression>`|`<httpCompression directory\="%SystemDrive%\inetpub\temp\IIS Temporary Compressed Files"><br />    <scheme name="gzip" dll="%Windir%\system32\inetsrv\gzip.dll" \/><br />    \<dynamicTypes><br />        <add mimeType="text/*" enabled="true" \/><br />        <add mimeType="message/*" enabled="true" /><br />        <add mimeType="application/x-javascript" enabled="true" /><br />        <add mimeType="application/javascript" enabled="true" /><br />        <add mimeType="*/*" enabled="false" /><br />    <\/dynamicTypes><br /></httpCompression>`|  

### <a name="security"></a>보안  
**요청 필터링**  


|       섹션        |                                                                                                                                        구성 요소                                                                                                                                        |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  `<globalModules>`   |                                                                                                        `<add name="RequestFilteringModule" image="%windir%\System32\inetsrv\modrqflt.dll" />`                                                                                                        |
|     `<modules>`      |                                                                                                                       `<add name="RequestFilteringModule" lockItem="true" />`                                                                                                                        |
| \`<requestFiltering> | `<requestFiltering><br />    <fileExtensions allowUnlisted="true" applyToWebDAV="true" /><br />    <verbs allowUnlisted="true" applyToWebDAV="true" /><br />    <hiddenSegments applyToWebDAV="true"><br />        <add segment="web.config" /><br />    </hiddenSegments><br /></requestFiltering>` |

**기본 인증**  

|섹션|구성 요소|  
|----------------|--------------------------|   
|`<globalModules>`|`<add name="BasicAuthenticationModule" image="%windir%\System32\inetsrv\authbas.dll" />`|  
|`<modules>`|`<add name="WindowsAuthenticationModule" lockItem="true" />`|  
|`<basicAuthentication>`|`<basicAuthentication enabled="false" />`|  

**클라이언트 인증서 매핑 인증**  

|섹션|구성 요소|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name="CertificateMappingAuthentication" image="%windir%\System32\inetsrv\authcert.dll" />`|  
|`<modules>`|`<add name="CertificateMappingAuthenticationModule" lockItem="true" />`|  
|`<clientCertificateMappingAuthentication>`|`<clientCertificateMappingAuthentication enabled="false" />`|  

**다이제스트 인증**  

|섹션|구성 요소|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name="DigestAuthenticationModule" image="%windir%\System32\inetsrv\authmd5.dll" />`|  
|`<modules>`|`<add name="DigestAuthenticationModule" lockItem="true" />`|  
|`<other>`|`<digestAuthentication enabled="false" />`|  

**IIS 클라이언트 인증서 매핑 인증**  


|                  섹션                   |                                         구성 요소                                         |
|--------------------------------------------|--------------------------------------------------------------------------------------------------------|
|             `<globalModules>`              | `<add name="CertificateMappingAuthenticationModule" image="%windir%\System32\inetsrv\authcert.dll" />` |
|                `<modules>`                 |               `<add name="CertificateMappingAuthenticationModule" lockItem="true" `/>\`                |
| `<clientCertificateMappingAuthentication>` |                      `<clientCertificateMappingAuthentication enabled="false" />`                      |

**IP 및 도메인 제한**  

|섹션|구성 요소|  
|----------------|--------------------------|  
|`<globalModules>`|```<add name="IpRestrictionModule" image="%windir%\System32\inetsrv\iprestr.dll" /><br /><add name="DynamicIpRestrictionModule" image="%windir%\System32\inetsrv\diprestr.dll" />```|  
|`<modules>`|`<add name="IpRestrictionModule" lockItem="true" \/><br /><add name="DynamicIpRestrictionModule" lockItem="true" \/>`|  
|`<ipSecurity>`|`<ipSecurity allowUnlisted="true" />`|  

**URL 권한 부여**  

|섹션|구성 요소|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name="UrlAuthorizationModule" image="%windir%\System32\inetsrv\urlauthz.dll" />`|  
|`<modules>`|`<add name="UrlAuthorizationModule" lockItem="true" />`|  
|`<authorization>`|`<authorization><br />    <add accessType="Allow" users="*" /><br /></authorization>`|  

**Windows 인증**  

|섹션|구성 요소|  
|----------------|--------------------------|    
|`<globalModules>`|`<add name="WindowsAuthenticationModule" image="%windir%\System32\inetsrv\authsspi.dll" />`|  
|`<modules>`|`<add name="WindowsAuthenticationModule" lockItem="true" />`|  
|`<windowsAuthentication>`|`<windowsAuthentication enabled="false" authPersistNonNTLM\="true"><br />    <providers><br />        <add value="Negotiate" /><br />        <add value="NTLM" /><br />    <\providers><br /><\windowsAuthentication><windowsAuthentication enabled="false" authPersistNonNTLM\="true"><br />    <providers><br />        <add value="Negotiate" /><br />        <add value="NTLM" /><br />    <\/providers><br /><\/windowsAuthentication>`|  

### <a name="application-development"></a>응용 프로그램 개발  
**애플리케이션 초기화**  

|섹션|구성 요소|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name="ApplicationInitializationModule" image="%windir%\System32\inetsrv\warmup.dll" />`|  
|`<modules>`|`<add name="ApplicationInitializationModule" lockItem="true" />`|  

**CGI**  

|섹션|구성 요소|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name="CgiModule" image="%windir%\System32\inetsrv\cgi.dll" /><br /><add name="FastCgiModule" image="%windir%\System32\inetsrv\iisfcgi.dll" />`|  
|`<modules>`|`<add name="CgiModule" lockItem="true" /><br /><add name="FastCgiModule" lockItem="true" />`|  
|`<handlers>`|`<add name="CGI-exe" path="*.exe" verb="\*" modules="CgiModule" resourceType="File" requireAccess="Execute" allowPathInfo="true" />`|  

**ISAPI 확장**  

|섹션|구성 요소|  
|----------------|--------------------------|    
|`<globalModules>`|`<add name="IsapiModule" image="%windir%\System32\inetsrv\isapi.dll" />`|  
|`<modules>`|`<add name="IsapiModule" lockItem="true" />`|  
|`<handlers>`|`<add name="ISAPI-dll" path="*.dll" verb="*" modules="IsapiModule" resourceType="File" requireAccess="Execute" allowPathInfo="true" />`|  

**ISAPI 필터**  

|섹션|구성 요소|  
|----------------|--------------------------|    
|`<globalModules>`|`<add name="IsapiFilterModule" image="%windir%\System32\inetsrv\filter.dll" />`|  
|`<modules>`|`<add name="IsapiFilterModule" lockItem="true" />`|  

**SSI(Server Side Include)**  

|섹션|구성 요소|  
|----------------|--------------------------|  
|`<globalModules>`|<`add name="ServerSideIncludeModule" image="%windir%\System32\inetsrv\iis_ssi.dll" />`|  
|`<modules>`|`<add name="ServerSideIncludeModule" lockItem="true" />`|  
|`<handlers>`|`<add name="SSINC-stm" path="*.stm" verb="GET,HEAD,POST" modules="ServerSideIncludeModule" resourceType="File" \/><br /><add name="SSINC-shtm" path="*.shtm" verb="GET,HEAD,POST" modules="ServerSideIncludeModule" resourceType="File" /><br /><add name="SSINC-shtml" path="*.shtml" verb="GET,HEAD,POST" modules="ServerSideIncludeModule" resourceType="File" />`|  
|`<serverSideInclude>`|`<serverSideInclude ssiExecDisable="false" />`|  

**WebSocket 프로토콜**  

|섹션|구성 요소|  
|----------------|--------------------------|    
|`<globalModules>`|`<add name="WebSocketModule" image="%windir%\System32\inetsrv\iiswsock.dll" />`|  
|`<modules>`|`<add name="WebSocketModule" lockItem="true" />`|  