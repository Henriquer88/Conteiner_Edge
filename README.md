# Conteiner Edge

## Objetivo
O objetivo principal do tutorial é demonstrar como criar, configurar e implantar dispositivos IoT Edge, fornecendo uma visão detalhada de todo o processo

# Introdução
O tutorial visa capacitar os desenvolvedores a entenderem e implementarem o conceito de dispositivos IoT Edge utilizando a plataforma Microsoft Azure. Ao longo do guia, os participantes são conduzidos através dos passos necessários para transformar uma Raspberry Pi em um dispositivo IoT Edge, capaz de executar serviços localmente e transmitir dados para a nuvem, através do Azure IoT Hub.

## Dispositivo Edge

Um dispositivo IoT Edge consiste basicamente em um dispositivo com um sistema operacional executando o IoT Edge Runtime, que é uma coletânea de software que permite o gerenciamento dos módulos do IoT Edge, que são pacotes executáveis compatíveis com contêineres Docke.

# Etapas do IOT Edge
O tutorial segue as etapas detalhadas para transformar uma Raspberry Pi em um dispositivo IoT Edge conectado ao Azure IoT Hub:

 1 - Pré-requisitos: É necessário possuir uma conta do Azure com créditos disponíveis e a Azure CLI instalada para gerenciar recursos via linha de comando. https://azure.microsoft.com/pt-br/free/

2 - Criação do IoT Hub: É criado um IoT Hub no Azure, que atua como ponto central para gerenciar e conectar dispositivos IoT Edge.

3 - Registro do Dispositivo: Um dispositivo IoT Edge (Raspberry Pi) é registrado no IoT Hub, gerando uma identidade para conexão.

4 - Instalação do IoT Edge Runtime: O IoT Edge Runtime é instalado na Raspberry Pi, preparando o dispositivo para executar módulos Edge.

5 - Configuração do Dispositivo: O dispositivo



# Criando uma instância no IOT Hub
O tutorial simplifica a implementação do Azure IoT Edge usando o PowerShell. Siga essas etapas no PowerShell para criar um dispositivo IoT Edge.

<img width="800" alt="Captura de tela 2023-08-29 211727" src="https://github.com/Henriquer88/Conteiner_Edge/assets/60757810/c109afd8-9388-4aff-bab3-9e992d9823a8">
                                 Página inicial do Azure

* Adicione a extensão azure-iot para gerenciar serviços de IoT pela CLI:
  <img width="800" alt="Captura de tela 2023-08-29 213302" src="https://github.com/Henriquer88/Conteiner_Edge/assets/60757810/d38bc586-2e41-4b2a-a422-80091b639f2e">
  PowerShell Azure

* Crie um Resource Group:
  az group create -l brazilsouth -n MyResourceGroup
* Crie um IoT Hub:
  az iot hub create --resource-group MyResourceGroup --name MyIotHub --sku F1 --partition-count 2
* Crie um dispositivo Edge:
  az iot hub device-identity create --device-id MyRasp --hub-name MyIotHub --edge-enabled
* Recupere a Connection String do Dispositivo:
  az iot hub device-identity connection-string show --device-id MyRasp --hub-name MyIotHub

  # Configuração da Raspberry pi
   Agora faremos o download de pacotes de configuração do repositório da Microsoft e a instalação do IoT Edge Runtime
    curl https://packages.microsoft.com/config/debian/stretch/multiarch/prod.list > ./microsoft-prod.list

  <img width="306" alt="Captura de tela 2023-08-29 221527" 
   src="https://github.com/Henriquer88/Conteiner_Edge/assets/60757810/f023af55-8081-41c9-a6bc-59b4484ef651">
   Configuração do repositório da Microsoft

  $ sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
  * Instale a chave pública GPG Microsoft.
    $ curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
    $ sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/

  * Garanta que os repositórios e o sistema estão atualizados:
    $ sudo apt-get update && sudo apt-get upgrade

 * Download do script de instalação do Docker
   $ curl -fsSL https://get.docker.com -o get-docker.sh
   $ sudo sh get-docker.sh

 * Consultando a versão do Docker instalada
   $ docker version
   
   <img width="300" alt="Captura de tela 2023-08-29 224936" 
   src="https://github.com/Henriquer88/Conteiner_Edge/assets/60757810/967fe871-99ed-4dba-ba4c-454358e2af9c">


 * Verificação se a instação está correta
   Verificamos a instalação com um Hello-World
   
 <img width="245" alt="Captura de tela 2023-08-29 225514" src="https://github.com/Henriquer88/Conteiner_Edge/assets/60757810/f3e101fb-42da-455e-a9fd-718164c95a3e">







  


  
  



 

  
