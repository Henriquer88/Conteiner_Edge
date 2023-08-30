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
   
   <img width="300" alt="Captura de tela 2023-08-29 225514" 
   src="https://github.com/Henriquer88/Conteiner_Edge/assets/60757810/f3e101fb-42da-455e-a9fd-718164c95a3e">

 * Instalação da versão mais atualizada do IoT Edge Runtime
   $ sudo apt-get install aziot-edge --fix-missing

 * Vamos agora à segunda etapa do provisionamento manual, configurando o dispositivo com sua string de conexão que o permite conectar a sua identidade na nuvem. O comando iotedge config mp cria um arquivo de configuração no dispositivo e adiciona a string de conexão passada como argumento. Utilize o seguinte comando usando a string que você guardou anteriormente.
   
<img width="891" alt="Captura de tela 2023-08-29 231434" src="https://github.com/Henriquer88/Conteiner_Edge/assets/60757810/e3ab796a-a90b-40f2-b988-e4664ae38fe2">

$ sudo iotedge config mp --connection-string 'PASTE_DEVICE_CONNECTION_STRING_HERE'

$ sudo iotedge config apply

Seguindo os passos acima teremos o seguite resultado :

<img width="300" alt="Captura de tela 2023-08-29 231914" src="https://github.com/Henriquer88/Conteiner_Edge/assets/60757810/8295aecc-23a3-40b2-9871-e265ef0bb1c6">

* Verifique o status do serviço do IoT Edge:
  $ sudo iotedge system status

<img width="253" alt="Captura de tela 2023-08-29 232246" src="https://github.com/Henriquer88/Conteiner_Edge/assets/60757810/91e2575b-9301-480e-91ec-8c63595d5641">

* Verificação das configurações aplicadas
  $ sudo iotedge check

  <img width="347" alt="Captura de tela 2023-08-29 232522" src="https://github.com/Henriquer88/Conteiner_Edge/assets/60757810/4b97f282-6165-4d76-b0d8-6d41182411cb">
O erro acima é esperado porque o módulo edgeHub ainda não foi criado. Será criado numa próxima etapa.

*  Verificação  dos módulos em execução
   
  <img width="339" alt="Captura de tela 2023-08-29 232730" src="https://github.com/Henriquer88/Conteiner_Edge/assets/60757810/ad04091d-a777-45df-a0f7-37cecf6e9243">

 ## Configuração do Azure
  Primeiramente, vá para o painel do IoT Hub e examine o gráfico que mostra a contagem de mensagens utilizadas, localizado no menu "Visão Geral". Isso lhe permitirá confirmar a conexão estabelecida pelo dispositivo. Em seguida, navegue até o menu de dispositivos IoT Edge e selecione o dispositivo específico. Lá, clique na opção "Módulos" localizada na parte inferior da tela para verificar o status dos diversos módulos presentes no dispositivo.

  <img width="945" alt="Captura de tela 2023-08-29 233450" src="https://github.com/Henriquer88/Conteiner_Edge/assets/60757810/8a6334f6-5d42-474a-bd74-caf9c8089902">

  Esses dados nos confirmam que a fase de provisionamento foi concluída com êxito. Note o campo "Resposta do Tempo de Execução" com a mensagem "417 - A configuração de implantação do dispositivo não está definida", o que indica que o dispositivo está pronto para receber uma nova implantação. Mantenha-se nessa janela para prosseguir com a próxima etapa

##  Deploy de um módulo gerador de dados de temperatura e umidade simulados

  Para realizar a implantação dos módulos no dispositivo, é necessário especificar as imagens, o registro de contêineres e as rotas das mensagens que os módulos utilizarão ao serem executados no dispositivo. Essas informações são fornecidas por meio do IoT Hub, que comporá automaticamente um arquivo chamado "Deployment Manifest" (Manifesto de Implantação). O dispositivo Edge continuamente verifica a presença de novos "Deployment Manifests" ou atualizações no IoT Hub. Ele faz o download desse arquivo para acessar as imagens diretamente no Container Registry indicado pelo arquivo. Isso permite que os contêineres sejam criados localmente, com base nas imagens e tags especificadas. A figura abaixo ilustra a interação entre os diversos elementos desse processo.

  :<img width="438" alt="Captura de tela 2023-08-29 234045" src="https://github.com/Henriquer88/Conteiner_Edge/assets/60757810/96ab4209-d590-4760-bab6-b1aeea58082f">:

Na sequência, a partir da janela anterior, localize e clique na opção "Set Modules" na barra de navegação superior. Isso o levará à seção de "IoT Edge Modules". Aí, clique em "Add" e selecione a alternativa "Marketplace Module" para buscar por uma imagem disponível no Marketplace. Na caixa de busca que aparece, digite "Simulated" e escolha o módulo chamado "Simulated Temperature Sensor"

  <img width="475" alt="Captura de tela 2023-08-29 235001" src="https://github.com/Henriquer88/Conteiner_Edge/assets/60757810/7c23faf2-5cb9-4f78-a810-4d26a9f9520a">

  <img width="629" alt="Captura de tela 2023-08-29 235522" src="https://github.com/Henriquer88/Conteiner_Edge/assets/60757810/03631f9f-6c04-4877-b9ff-cc8b064972f4">
                               Janela de Configuração

Além disso, na seção chamada "IoT Edge Modules", continue navegando e clique em "Runtime Settings". Dentro dessa seção, realize a modificação da versão dos módulos "Edge Agent" e "Edge Hub" para a versão mais recente, que é a 1.2. Depois de fazer essa alteração, não se esqueça de aplicar as mudanças antes de prosseguir.   

<img width="421" alt="Captura de tela 2023-08-29 235801" src="https://github.com/Henriquer88/Conteiner_Edge/assets/60757810/149e6916-960f-470f-aa5b-2df2379fe66d">

Clique em next para irmos para a próxima etapa do deployment, a etapa de configuração de rotas. Uma rota é composta por um nome que identifica a rota e um valor que descreve o caminho das mensagens. Podemos configurar uma rota para estabelecer comunicação entre módulos e entre o dispositivo e o IoT Hub. No nosso caso, vamos configurar uma rota para que as mensagens produzidas pelo módulo de simulação sejam escoadas para o IoT Hub. 

<img width="879" alt="Captura de tela 2023-08-30 000514" src="https://github.com/Henriquer88/Conteiner_Edge/assets/60757810/cd64acf1-c9f0-41b5-b350-b70550e82603">

Na janela do dispositivo, você verá um destaque que indica o status dos módulos após um deployment bem-sucedido. Isso significa que os módulos foram implantados com sucesso no dispositivo e estão em execução. Esse status é uma confirmação de que as etapas anteriores, incluindo a configuração das imagens dos módulos, as rotas de comunicação e a revisão do "Deployment Manifest", foram concluídas com êxito. Verificar esse status é essencial para garantir que a solução IoT Edge esteja operando conforme o planejado.

## Verificação do Status dos módulos 

 - $ sudo iotedge list
 - $ sudo iotedge check




<img width="336" alt="Captura de tela 2023-08-30 000852" src="https://github.com/Henriquer88/Conteiner_Edge/assets/60757810/50736b47-3f85-4529-addf-6bc82e89c9a3">




  












  


  
  



 

  
