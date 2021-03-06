---
title: Tutorial für Azure Container Instances – Bereitstellungs-App
description: Tutorial für Azure Container Instances (Teil 3 von 3) – Bereitstellen der Anwendung
services: container-instances
author: mmacy
manager: timlt
ms.service: container-instances
ms.topic: tutorial
ms.date: 03/21/2018
ms.author: marsma
ms.custom: mvc
ms.openlocfilehash: 29d7114f288f7387d0c7cd5c6afe2eaaa7a8c560
ms.sourcegitcommit: 48ab1b6526ce290316b9da4d18de00c77526a541
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="tutorial-deploy-a-container-to-azure-container-instances"></a>Tutorial: Bereitstellen eines Containers in Azure Container Instances

Dies ist das letzte Tutorial einer dreiteiligen Reihe. In den vorhergehenden Teilen der Reihe wurde [ein Containerimage erstellt](container-instances-tutorial-prepare-app.md) und [mithilfe von Push an eine Azure Container Registry-Instanz übermittelt](container-instances-tutorial-prepare-acr.md). Zum Abschluss der Reihe wird der Container in diesem Tutorial für Azure Container Instances bereitgestellt.

In diesem Tutorial führen Sie Folgendes durch:

> [!div class="checklist"]
> * Bereitstellen des Containers aus Azure Container Registry in Azure Container Instances
> * Anzeigen der ausgeführten Anwendung im Browser
> * Anzeigen der Protokolle des Containers

## <a name="before-you-begin"></a>Voraussetzungen

[!INCLUDE [container-instances-tutorial-prerequisites](../../includes/container-instances-tutorial-prerequisites.md)]

## <a name="deploy-the-container-using-the-azure-cli"></a>Bereitstellen des Containers mithilfe der Azure-Befehlszeilenschnittstelle

In diesem Abschnitt verwenden Sie die Azure CLI zum Bereitstellen des Images, das im [ersten Tutorial](container-instances-tutorial-prepare-app.md) erstellt und im [zweiten Tutorial](container-instances-tutorial-prepare-acr.md) per Pushvorgang in die Azure Container Registry übertragen wurde. Arbeiten Sie diese Tutorials durch, bevor Sie fortfahren.

### <a name="get-registry-credentials"></a>Abrufen von Registrierungsanmeldeinformationen

Beim Bereitstellen eines Images, das in einer privaten Containerregistrierung gehostet wird (wie im [zweiten Tutorial](container-instances-tutorial-prepare-acr.md)), müssen Sie die Anmeldeinformationen der Registrierung angeben.

Rufen Sie zuerst den vollständigen Namen des Anmeldeservers für die Containerregistrierung ab (ersetzen Sie `<acrName>` durch den Namen Ihrer Registrierung):

```azurecli
az acr show --name <acrName> --query loginServer
```

Rufen Sie als Nächstes das Kennwort der Containerregistrierung ab:

```azurecli
az acr credential show --name <acrName> --query "passwords[0].value"
```

### <a name="deploy-container"></a>Bereitstellen des Containers

Verwenden Sie nun den Befehl [az container create][az-container-create], um den Container bereitzustellen. Ersetzen Sie `<acrLoginServer>` und `<acrPassword>` durch die Werte, die Sie mit den beiden vorhergehenden Befehlen abgerufen haben. Ersetzen Sie `<acrName>` durch den Namen Ihrer Containerregistrierung.

```azurecli
az container create --resource-group myResourceGroup --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-username <acrName> --registry-password <acrPassword> --dns-name-label aci-demo --ports 80
```

Innerhalb weniger Sekunden sollten Sie eine erste Antwort von Azure erhalten. Der Wert `--dns-name-label` muss innerhalb der Azure-Region, in der Sie die Containerinstanz erstellen, eindeutig sein. Ändern Sie den Wert im vorherigen Befehl, wenn Sie beim Ausführen des Befehls eine Fehlermeldung bezüglich der **DNS-Namensbezeichnung** erhalten.

### <a name="verify-deployment-progress"></a>Überprüfen des Bereitstellungsstatus

Verwenden Sie zum Anzeigen des Bereitstellungsstatus den Befehl [az container show][az-container-show]:

```azurecli
az container show --resource-group myResourceGroup --name aci-tutorial-app --query instanceView.state
```

Führen Sie den Befehl [az container show][az-container-show] erneut aus, bis der Status nicht mehr *Ausstehend*, sondern *Wird ausgeführt* lautet. Das sollte nach maximal einer Minute der Fall sein. Wenn für den Container *Wird ausgeführt* angezeigt wird, fahren Sie mit dem nächsten Schritt fort.

## <a name="view-the-application-and-container-logs"></a>Anzeigen der Anwendungs- und Containerprotokolle

Wenn die Bereitstellung erfolgreich war, zeigen Sie mit dem Befehl [az container show][az-container-show] den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) des Containers an:

```bash
az container show --resource-group myResourceGroup --name aci-tutorial-app --query ipAddress.fqdn
```

Beispiel: 
```console
$ az container show --resource-group myResourceGroup --name aci-tutorial-app --query ipAddress.fqdn
"aci-demo.eastus.azurecontainer.io"
```

Navigieren Sie zum Anzeigen der ausgeführten Anwendung in Ihrem bevorzugten Browser zum angezeigten DNS-Namen:

![„Hello World“-Anwendung im Browser][aci-app-browser]

Sie können auch die Protokollausgabe des Containers anzeigen:

```azurecli
az container logs --resource-group myResourceGroup --name aci-tutorial-app
```

Beispielausgabe:

```bash
$ az container logs --resource-group myResourceGroup --name aci-tutorial-app
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://aci-demo.eastus.azurecontainer.io/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="clean-up-resources"></a>Bereinigen von Ressourcen

Wenn Sie die in dieser Tutorialreihe erstellten Ressourcen nicht mehr benötigen, können Sie den Befehl [az group delete][az-group-delete] ausführen, um die Ressourcengruppe und alle darin enthaltenen Ressourcen zu entfernen. Dieser Befehl löscht die von Ihnen erstellte Containerregistrierung sowie den ausgeführten Container und alle zugehörigen Ressourcen.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Nächste Schritte

In diesem Tutorial haben Sie Ihren Container in Azure Container Instances bereitgestellt. Die folgenden Schritte wurden durchgeführt:

> [!div class="checklist"]
> * Bereitstellen des Containers aus der Azure Container Registry-Instanz mithilfe der Azure-Befehlszeilenschnittstelle
> * Anzeigen der Anwendung im Browser
> * Anzeigen der Containerprotokolle

Nachdem Sie sich mit den Grundlagen vertraut gemacht haben, können Sie sich jetzt eingehender über Azure Container Instances informieren, z.B. über die Funktionsweise von Containergruppen:

> [!div class="nextstepaction"]
> [Containergruppen in Azure Container Instances](container-instances-container-groups.md)

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png

<!-- LINKS - external -->
[docker-linux]: https://docs.docker.com/engine/installation/#supported-platforms
[docker-login]: https://docs.docker.com/engine/reference/commandline/login/
[docker-mac]: https://docs.docker.com/docker-for-mac/
[docker-push]: https://docs.docker.com/engine/reference/commandline/push/
[docker-tag]: https://docs.docker.com/engine/reference/commandline/tag/
[docker-windows]: https://docs.docker.com/docker-for-windows/

<!-- LINKS - internal -->
[az-container-create]: /cli/azure/container#az_container_create
[az-container-show]: /cli/azure/container#az_container_show
[az-group-delete]: /cli/azure/group#az_group_delete
[azure-cli-install]: /cli/azure/install-azure-cli
[prepare-app]: ./container-instances-tutorial-prepare-app.md
