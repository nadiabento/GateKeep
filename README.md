# GateKeep

# 🚗 Smart Garage Opener (Geofencing)

Sistema inteligente de automação residencial projetado para abrir o portão da garagem de forma 100% automática por proximidade. O aplicativo monitoriza a localização em segundo plano e aciona o portão assim que o utilizador entra num **raio de 200 metros** de casa.

---

## 🚀 Funcionalidades Principais

* **Cerca Virtual (Geofencing):** Criação de um perímetro invisível de 200m em redor da habitação.
* **Segundo Plano Eficiente:** Utiliza as APIs nativas do iOS/Android para detetar a entrada na zona com o mínimo impacto na bateria.
* **Segurança Reforçada:** Envio de tokens de autenticação cifrados para evitar aberturas não autorizadas.
* **Logs de Acesso:** Registo local ou na nuvem de todas as vezes que o portão foi acionado.

## 🛠️ Tecnologias e Arquitetura

O projeto está dividido em duas partes fundamentais:

1. **Client (App Móvel):** Construído em [Flutter / React Native] utilizando bibliotecas de localização em segundo plano.
2. **Server / Hardware (Garagem):** Microcontrolador [ESP32 / Raspberry Pi] ligado fisicamente ao botão do motor do portão através de um módulo Relé.

---

## 📦 Estrutura do Projeto Sugerida

```text
├── app/                  # Código fonte do aplicativo móvel (Mobile)
│   ├── src/
│   └── package.json / pubspec.yaml
├── hardware/             # Código fonte do microcontrolador (Firmware)
│   ├── garage_relay.ino  # Script para ESP32/Arduino
│   └── config.h.example  # Exemplo de configuração de Wi-Fi e chaves
└── README.md             # Documentação do projeto
```

---

## 📋 Como Funciona o Fluxo

1. **Aproximação:** O utilizador desloca-se em direção a casa.
2. **Deteção:** O sistema operativo do telemóvel deteta a entrada no raio de 200m (Geofence Trigger).
3. **Autenticação:** O app gera uma requisição HTTPS (ou payload MQTT) segura com uma chave de autenticação (API Key).
4. **Acionamento:** O microcontrolador (ESP32) recebe a ordem via Wi-Fi, fecha o contacto do relé durante 1 segundo (simulando o clique do comando) e o portão abre.

---

## 🛠️ Pré-requisitos para Instalação

Antes de começares, vais precisar de:
* Um editor de código como o **VS Code**.
* **Node.js** ou **Flutter SDK** instalado (dependendo da escolha do app).
* Um microcontrolador **ESP32** com ligação Wi-Fi e um **Módulo Relé de 5V/12V**.
* Configurar permissões de "Localização Sempre Ativa" (Always Allow) no telemóvel.

---

## 🔐 Notas de Segurança

⚠️ **Importante:** Nunca guardes as tuas credenciais de Wi-Fi ou tokens de segurança diretamente no código público do Git. Utiliza ficheiros `.env` ou `config.h` e adiciona-os ao teu `.gitignore`.
