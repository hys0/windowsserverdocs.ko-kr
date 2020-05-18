---
title: Paramètres pris en charge du fichier RDP du Bureau à distance
description: Découvrez les paramètres du fichier RDP pour Bureau à distance
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 05/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 745f911367471d3708c57a3c777743a65c5bd4a8
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993349"
---
# <a name="supported-remote-desktop-rdp-file-settings"></a>Paramètres pris en charge du fichier RDP du Bureau à distance

Le tableau suivant contient la liste des paramètres du fichier RDP pris en charge et que vous pouvez utiliser avec les clients Bureau à distance.

Le tableau met également en évidence les paramètres pris en charge en tant que propriétés personnalisées avec Windows Virtual Desktop. Vous pouvez consulter [cette documentation](https://go.microsoft.com/fwlink/?linkid=2098243&clcid=0x409) qui explique comment utiliser PowerShell pour personnaliser les propriétés RDP des pools d’hôtes Windows Virtual Desktop.

## <a name="connection-information"></a>Informations de connexion

| Paramètre RDP                        | Description            | Valeurs                 | Valeur par défaut          | Windows Virtual Desktop |
|------------------------------------|------------------------|------------------------|:----------------------:|:-----------------------:|
| full address:s:value | Nom du PC :</br>Ce paramètre spécifie le nom ou l’adresse IP de l’ordinateur distant auquel vous souhaitez vous connecter.</br></br>Il s’agit du seul paramètre obligatoire dans un fichier RDP. | Un nom, une adresse IPv4 ou une adresse IPv6 valide. | | |
| alternate full address:s:value | Spécifie un autre nom ou une autre adresse IP de l’ordinateur distant. | Un nom, une adresse IPv4 ou une adresse IPv6 valide. | | |
| username:s:value | Spécifie le nom du compte d’utilisateur qui sera utilisé pour la connexion à l’ordinateur distant. | N’importe quel nom d’utilisateur valide. | | |
| domain:s:value | Spécifie le nom du domaine au sein duquel se trouve le compte d’utilisateur qui sera utilisé pour la connexion à l’ordinateur distant. | Un nom de domaine valide, tel que « CONTOSO ». | | |
| gatewayhostname:s:value | Spécifie le nom d’hôte de passerelle des services Bureau à distance. | Un nom, une adresse IPv4 ou une adresse IPv6 valide. | | |
| gatewaycredentialssource:i:value | Spécifie la méthode d’authentification de passerelle des services Bureau à distance. | - 0 : Demander le mot de passe (NTLM)</br>- 1 : Utiliser la carte à puce</br>- 4 : Autoriser l’utilisateur à sélectionner ultérieurement | 0 | |
| gatewayprofileusagemethod:i:value | Spécifie s’il faut utiliser les paramètres par défaut de la passerelle des services Bureau à distance. | - 0 : Utiliser le mode de profil par défaut, comme indiqué par l’administrateur</br>- 1 : Utiliser des paramètres explicites, comme indiqué par l’utilisateur | 0 | |
| gatewayusagemethod:i:value | Spécifie quand utiliser une passerelle des services Bureau à distance pour la connexion. | - 0 : Ne pas utiliser de passerelle des services Bureau à distance</br>- 1 : Toujours utiliser une passerelle des services Bureau à distance</br>- 2 : Utiliser une passerelle des services Bureau à distance si une connexion directe ne peut pas être établie avec l’hôte de session RD</br>- 3 : Utiliser les paramètres par défaut de la passerelle des services Bureau à distance</br>- 4 : Ne pas utiliser une passerelle des services Bureau à distance, ignorer la passerelle pour les adresses locales</br>Un réglage de cette valeur de propriété sur 0 ou 4 est semblable, mais le réglage sur 4 active l’option permettant d’ignorer les adresses locales. | 0 | |
| promptcredentialonce:i:value | Détermine si les informations d’identification d’un utilisateur sont enregistrées et utilisées pour la passerelle Bureau à distance et l’ordinateur distant. | - 0 : La session à distance n’utilisera pas les mêmes informations d’identification</br>- 1 : La session à distance utilisera les mêmes informations d’identification | 1 | |
| authentication level:i:value | Définit les paramètres de niveau d’authentification du serveur. | - 0 : Si l’authentification du serveur échoue, se connecter à l’ordinateur sans avertissement (se connecter et ne pas m’avertir)</br>- 1 : Si l’authentification du serveur échoue, ne pas établir de connexion (ne pas se connecter)</br>- 2 : Si l’authentification du serveur échoue, afficher un avertissement et m’autoriser à me connecter ou à refuser la connexion (m’avertir)</br>- 3 : Aucune exigence d’authentification spécifiée. | 3 | |
| enablecredsspsupport:i:value | Détermine l’utilisation par le client de l’authentification CredSSP (Credential Security Support Provider) si elle est disponible. | - 0 : RDP n’utilisera pas l’authentification CredSSP, même si le système d’exploitation la prend en charge</br>- 1 : RDP utilisera l’authentification CredSSP si le système d’exploitation la prend en charge | 1 | X |
| disableconnectionsharing:i:value | Détermine si le client se reconnecte à toute session déconnectée existante ou démarre une nouvelle connexion quand une nouvelle connexion est lancée. | - 0 : Se reconnecter à une session existante</br>- 1 : Initier une nouvelle connexion | 0 | X |
| alternate shell:s:value | Spécifie un programme à démarrer automatiquement dans la session à distance en tant que shell au lieu de l’Explorateur. | Chemin valide d’un fichier exécutable, tel que « C:\ProgramFiles\Office\word.exe » | | X |

## <a name="session-behavior"></a>Comportement de la session

| Paramètre RDP                        | Description            | Valeurs                 | Valeur par défaut          | Windows Virtual Desktop |
|------------------------------------|------------------------|------------------------|:----------------------:|:-----------------------:|
| autoreconnection enabled:i:value | Détermine si le client tente automatiquement de se reconnecter à l’ordinateur distant en cas d’arrêt de la connexion, une interruption de la connectivité réseau par exemple. | - 0 : Le client n’essaie pas de se reconnecter automatiquement</br>- 1 : Le client essaie de se reconnecter automatiquement | 1 | X |
| bandwidthautodetect:i:value | Détermine si la détection automatique du type de réseau est activée | - 0 : Désactiver la détection automatique du type de réseau</br>- 1 : Activer la détection automatique du type de réseau | 1 | X |
| networkautodetect:i:value | Détermine s’il faut utiliser la détection automatique de la bande passante réseau. Nécessite que bandwidthautodetect soit défini sur 1. | - 0 : Ne pas utiliser la détection automatique de la bande passante réseau</br> - 1 : Utiliser la détection automatique de la bande passante réseau | 1 | X |
| compression:i:value | Détermine si la compression en bloc est activée lorsqu’il est transmis par RDP vers l’ordinateur local.|- 0 : Désactiver la compression en bloc RDP</br>- 1 : Activer la compression en bloc RDP | 1 | X |
| videoplaybackmode:i:value| Détermine si la connexion utilise un streaming multimédia adapté au protocole RDP pour la lecture vidéo.|- 0 : Ne pas utiliser de diffusion multimédia en continu adaptée au protocole RDP pour la lecture vidéo</br>- 1 : Utiliser une diffusion multimédia en continu adaptée au protocole RDP pour la lecture vidéo lorsque cela est possible | 1 | X |

## <a name="device-redirection"></a>Redirection d’appareils

| Paramètre RDP                        | Description            | Valeurs                 | Valeur par défaut          | Windows Virtual Desktop |
|------------------------------------|------------------------|------------------------|:----------------------:|:-----------------------:|
| audiocapturemode:i:value | Redirection du microphone :</br>Indique si la redirection audio d’entrée est activée. | - 0 : Désactiver la capture audio à partir de l’appareil local</br>- 1 : Activer la capture audio à partir de l’appareil local et la redirection vers une application audio dans la session à distance | 0 | X |
| encode redirected video capture:i:value | Active ou désactive l’encodage de la vidéo redirigée. | - 0 : Désactiver l’encodage de la vidéo redirigée</br>- 1 : Activer l’encodage de la vidéo redirigée | 1 | X |
| redirected video capture encoding quality:i:value | Contrôle la qualité de la vidéo encodée. | - 0 : Vidéo à compression élevée. La qualité peut être altérée en cas de mouvements trop importants. </br>- 1 : Compression moyenne.</br>- 2 : Vidéo à faible compression avec une qualité d’image élevée. | 0 | X |
| audiomode:i:value | Emplacement de sortie audio :</br>Détermine si la machine locale ou distante joue l’audio. | - 0 : Lire des sons sur l’ordinateur local (s’exécute sur cet ordinateur)</br>- 1 : Lire des sons sur l’ordinateur distant (s’exécute sur l’ordinateur distant)</br>- 2 : Ne pas lire les sons (ne pas lire) | 0 | X |
| camerastoredirect:s:value | Redirection des caméras :</br>Configure les caméras à rediriger. Ce paramètre utilise une liste délimitée par des points-virgules des interfaces KSCATEGORY_VIDEO_CAMERA des caméras activées pour la redirection. | - * : Rediriger toutes les caméras</br> - Liste de caméras, par exemple camerastoredirect:s:\\?\usb#vid_0bda&pid_58b0&mi</br>- Il est possible d’exclure une caméra spécifique en ajoutant le caractère « - » devant la chaîne de liaison symbolique | Ne rediriger aucune caméra | X |
| devicestoredirect:s:value | Redirection des appareils USB :</br>Détermine les appareils sur l’ordinateur local qui sont redirigés et disponibles dans la session à distance. | - * : Rediriger tous les appareils pris en charge, y compris ceux qui sont connectés plus tard</br> - ID de matériel valide pour un ou plusieurs appareils | Ne rediriger aucun appareil | X |
| drivestoredirect:s:value | Redirection du lecteur/stockage :</br>Détermine les lecteurs de disque sur l’ordinateur local qui sont redirigés et disponibles dans la session à distance. | - Aucune valeur spécifiée : aucun lecteur n’est redirigé</br>- * : Rediriger tous les lecteurs de disque, y compris les disques connectés plus tard</br>- DynamicDrives : rediriger tous les lecteurs qui sont connectés ultérieurement</br>- Le lecteur et les étiquettes pour un ou plusieurs disques, comme « drivestoredirect:s:C:;E:; » : rediriger le ou les lecteurs spécifiés | Ne rediriger aucun lecteur | X |
| redirectclipboard:i:value | Redirection du Presse-papiers :</br>Détermine si la redirection du Presse-papiers est activée. | - 0 : Le presse-papiers sur l’ordinateur local n’est pas disponible dans la session à distance</br>- 1 : Le presse-papiers sur l’ordinateur local est disponible dans la session à distance | 1 | X |
| redirectprinters:i:value | Redirection de l’imprimante :</br>Détermine si les imprimantes configurées sur l’ordinateur client sont redirigées et disponibles dans la session à distance | - 0 : Les imprimantes sur l’ordinateur local ne sont pas disponibles dans la session à distance</br>- 1 : Les imprimantes sur l’ordinateur local sont disponibles dans la session à distance | 1 | X |
| redirectsmartcards:i:value | Redirection des périphériques de carte à puce :</br>Détermine si les périphériques de carte à puce sur l’ordinateur client sont redirigés et disponibles dans la session à distance. |- 0 : Le périphérique de carte à puce sur l’ordinateur local n’est pas disponible dans la session à distance</br>- 1 : Le périphérique de carte à puce sur l’ordinateur local est disponible dans la session à distance | 1 | X |

## <a name="display-settings"></a>Paramètres d'affichage

| Paramètre RDP                        | Description            | Valeurs                 | Valeur par défaut          | Windows Virtual Desktop |
|------------------------------------|------------------------|------------------------|:----------------------:|:-----------------------:|
| use multimon:i:value | Détermine si la session à distance utilise un ou plusieurs affichages à partir de l’ordinateur local. | - 0 : Ne pas activer la prise en charge de plusieurs affichages</br>- 1 : Activer la prise en charge de plusieurs affichages | 0 | X |
| selectedmonitors:s:value | Spécifie les affichages locaux à utiliser à partir de la session à distance. Les affichages sélectionnés doivent être contigus. Nécessite que use multimon soit défini sur 1.</br></br>Disponible uniquement sur les clients Boîte de réception Windows (MSTSC) et Bureau Windows (MSRDC). | Liste délimitée par des virgules des ID d’affichage spécifiques à l’ordinateur. Vous pouvez récupérer les ID en appelant mstsc.exe /l. Le premier ID listé est défini comme affichage principal dans la session. | Tous les affichages | X |
| maximizetocurrentdisplays:i:value | Détermine sur quel affichage la session à distance passe en mode plein écran lors d’un agrandissement. Nécessite que use multimon soit défini sur 1.</br></br>Disponible uniquement sur le client Bureau Windows (MSRDC). | - 0 : La session passe en mode plein écran sur les affichages initialement sélectionnés lors d’un agrandissement</br>- 1 : La session passe dynamiquement en mode plein écran sur les affichages touchés par la fenêtre de session lors d’un agrandissement | 0 | X |
| singlemoninwindowedmode:i:value | Détermine si une session à distance multi-affichage bascule automatiquement en mode mono-affichage en quittant le mode plein écran. Nécessite que use multimon soit défini sur 1.</br></br>Disponible uniquement sur le client Bureau Windows (MSRDC). | - 0 : La session conserve tous les affichages quand elle quitte le mode plein écran</br>- 1 : La session bascule en mode mono-affichage quand elle quitte le mode plein écran | 0 | X |
| screen mode id:i:value | Détermine si la fenêtre de session à distance s’affiche en mode plein écran quand vous lancez la connexion. | - 1 : La session à distance s’affiche dans une fenêtre</br>- 2 : La session à distance s’affiche en plein écran | 2 | X |
| smart sizing:i:value | Détermine si l’ordinateur local met à l’échelle le contenu de la session à distance en fonction de la taille de la fenêtre. | - 0 : Le contenu de la fenêtre locale n’est pas mis à l’échelle quand il est redimensionné</br>- 1 : Le contenu de la fenêtre locale est mis à l’échelle quand il est redimensionné | 0 | X |
| dynamic resolution:i:value | Détermine si la résolution de la session à distance est automatiquement mise à jour quand la fenêtre locale est redimensionnée. | - 0 : La résolution de la session reste statique pendant toute la durée de la session</br>- 1 : La résolution de la session est mise à jour quand la fenêtre locale est redimensionnée | 1 | X |
| desktop size id:i:value | Spécifie les dimensions du bureau de session à distance à partir d’un ensemble d’options prédéfinies. Ce paramètre est remplacé si les paramètres desktopheight et desktopwidth sont spécifiés.| \- 0 : 640×480</br>- 1 : 800×600</br>- 2 : 1024×768</br>- 3 : 1280×1024</br>- 4 : 1600×1200 | 1 | X |
| desktopheight:i:value | Spécifie la hauteur de résolution (en pixels) de la session à distance. | Valeur numérique comprise entre 200 et 8192 | Correspond à l’ordinateur local | X |
| desktopwidth:i:value | Spécifie la largeur de résolution (en pixels) de la session à distance. | Valeur numérique comprise entre 200 et 8192 | Correspond à l’ordinateur local | X |
| desktopscalefactor:i:value | Spécifie le facteur d’échelle de la session à distance pour que le contenu apparaisse plus grand. | Valeur numérique de la liste suivante : 100, 125, 150, 175, 200, 250, 300, 400, 500 | 100 | X |

## <a name="remoteapp"></a>RemoteApp

| Paramètre RDP                        | Description            | Valeurs                 | Valeur par défaut          | Windows Virtual Desktop |
|------------------------------------|------------------------|------------------------|:----------------------:|:-----------------------:|
| remoteapplicationcmdline:s:value | Paramètres de ligne de commande facultatifs pour RemoteApp. | Paramètres de ligne de commande valides. | | |
| remoteapplicationexpandcmdline:i:value | Détermine si les variables d’environnement contenues dans le paramètre de ligne de commande de RemoteApp doivent être développées localement ou à distance. | - 0 : Les variables d’environnement doivent être développées par les valeurs de l’ordinateur local</br>- 1 : Les variables d’environnement doivent être développées par les valeurs de l’ordinateur distant | 1 | |
| remoteapplicationexpandworkingdir | Détermine si les variables d’environnement contenues dans le paramètre de répertoire de travail de RemoteApp doivent être développées localement ou à distance. | - 0 : Les variables d’environnement doivent être développées par les valeurs de l’ordinateur local</br> - 1 : Les variables d’environnement doivent être développées par les valeurs de l’ordinateur distant.</br>Le répertoire de travail de RemoteApp est spécifié via le paramètre de répertoire de travail de l’interpréteur de commandes. | 1 | |
| remoteapplicationfile:s:value | Spécifie un fichier à ouvrir par la RemoteApp sur l’ordinateur distant.</br>Pour les fichiers locaux à ouvrir, vous devez également activer la redirection de lecteur pour le lecteur source. | Chemin de fichier valide. | | |
| remoteapplicationicon:s:value | Spécifie le fichier d’icône à afficher dans l’interface utilisateur client lors du lancement d’une RemoteApp. Si aucun nom de fichier n’est spécifié, le client utilisera l’icône standard de bureau à distance. Seuls les fichiers ICO sont pris en charge. | Chemin de fichier valide. | | |
| remoteapplicationmode:i:value | Détermine si une connexion est lancée en tant que session RemoteApp. | - 0 : Ne pas lancer une session RemoteApp</br>- 1 : Lancer une session RemoteApp | 1 | |
| remoteapplicationname:s:value | Spécifie le nom de la RemoteApp dans l’interface client lors du démarrage de la RemoteApp.| Nom complet de l’application. Par exemple, « Excel 2016 ». | | |
| remoteapplicationprogram:s:value | Spécifie l’alias ou le nom de l’exécutable de la RemoteApp. | Alias ou nom valide. Par exemple, « EXCEL ». | | |
