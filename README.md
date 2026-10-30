# Star Desk

**Star Desk** é o programa de acesso remoto **gratuito** da **Star Aduana**. Ele permite ver e controlar outro computador pela internet com criptografia de ponta a ponta, usando o **servidor próprio da empresa**, sem depender de AnyDesk ou TeamViewer.

O Star Desk é uma versão personalizada do [RustDesk](https://github.com/rustdesk/rustdesk) (licença AGPL-3.0), com a marca, as cores e o servidor da Star Aduana já embutidos.

## O que já vem pronto
- Nome **Star Desk**, ícone e logo da estrela da Star Aduana
- Visual preto e branco com verde de destaque (identidade do site staraduana.com)
- Servidor de ID/Relay `136.248.97.187` e chave pública **embutidos**: quem instala não configura nada
- Tudo que o RustDesk faz: controle de tela, mouse e teclado, transferência de arquivos, chat, vários monitores, acesso sem supervisão (senha fixa), conexão direta P2P ou por relay
- Instalador para **Windows 10 e 11 (64 bits)**: `.exe` (instala ou roda direto) e `.msi` (para instalar em vários PCs)

## Como gerar o instalador
O instalador é montado automaticamente pelo **GitHub Actions**:
1. Aba **Actions** › **Star Desk - Windows** › **Run workflow**.
2. Depois de ~40 a 60 minutos, os arquivos `StarDesk-<versão>-x86_64.exe` e `.msi` aparecem em **Releases** › *Star Desk (ultima versao)* e também como artefato da execução.

Também roda sozinho ao criar uma tag `v*` (ex.: `v1.0.0`).

## Onde ficam as personalizações
| O quê | Arquivo |
|---|---|
| Nome do app, servidor e chave | `libs/hbb_common/src/config.rs` (`APP_NAME`, `RENDEZVOUS_SERVERS`, `RS_PUB_KEY`) |
| Cores e tema | `flutter/lib/common.dart` (`MyTheme`) |
| Ícones e logo | `res/icon.ico`, `res/*.png`, `res/tray-icon.ico`, `flutter/assets/icon.*`, `flutter/assets/logo_*.png`, `flutter/windows/runner/resources/app_icon.ico` |
| Nome no Windows (propriedades do .exe) | `flutter/windows/runner/Runner.rc` |
| Build do Windows | `.github/workflows/star-desk.yml` |

## Servidor
O servidor (rustdesk-server: `hbbs` + `hbbr`) roda numa VM Oracle Cloud Always Free, portas 21115-21117 TCP e 21116 UDP. Se o servidor mudar de IP, troque `RENDEZVOUS_SERVERS` em `config.rs` e gere o instalador de novo.

## Licença
AGPL-3.0, a mesma do RustDesk (veja `LICENCE`). O código-fonte desta versão precisa continuar disponível neste repositório. O README original do RustDesk está em `README-RustDesk.md`.
