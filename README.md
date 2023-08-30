# Conteiner Edge

## Objetivo
O objetivo principal do tutorial é demonstrar como criar, configurar e implantar dispositivos IoT Edge, fornecendo uma visão detalhada de todo o processo

## Introdução
O tutorial visa capacitar os desenvolvedores a entenderem e implementarem o conceito de dispositivos IoT Edge utilizando a plataforma Microsoft Azure. Ao longo do guia, os participantes são conduzidos através dos passos necessários para transformar uma Raspberry Pi em um dispositivo IoT Edge, capaz de executar serviços localmente e transmitir dados para a nuvem, através do Azure IoT Hub.

## Dispositivo Edge

Um dispositivo IoT Edge consiste basicamente em um dispositivo com um sistema operacional executando o IoT Edge Runtime, que é uma coletânea de software que permite o gerenciamento dos módulos do IoT Edge, que são pacotes executáveis compatíveis com contêineres Docke.

## Etapas do IOT Edge
O tutorial segue as etapas detalhadas para transformar uma Raspberry Pi em um dispositivo IoT Edge conectado ao Azure IoT Hub:

 1 - Pré-requisitos: É necessário possuir uma conta do Azure com créditos disponíveis e a Azure CLI instalada para gerenciar recursos via linha de comando. https://azure.microsoft.com/pt-br/free/

2 - Criação do IoT Hub: É criado um IoT Hub no Azure, que atua como ponto central para gerenciar e conectar dispositivos IoT Edge.

3 - Registro do Dispositivo: Um dispositivo IoT Edge (Raspberry Pi) é registrado no IoT Hub, gerando uma identidade para conexão.

4 - Instalação do IoT Edge Runtime: O IoT Edge Runtime é instalado na Raspberry Pi, preparando o dispositivo para executar módulos Edge.

5 - Configuração do Dispositivo: O dispositivo



## Criando uma instância no IOT Hub
Nessa etapa utilizaremos o PowerShel no azure para fazer as devidas configurações 

<img width="897" alt="Captura de tela 2023-08-29 211727" src="https://github.com/Henriquer88/Conteiner_Edge/assets/60757810/c109afd8-9388-4aff-bab3-9e992d9823a8">
                                 Página inicial do Azure
