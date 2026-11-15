# Aqua Launcher

Um launcher de jogos para Windows, leve e com visual próprio, que reúne em um só lugar os jogos da Steam, Epic, GOG e das suas pastas. Feito em Python com interface web (pywebview + HTML), com suporte completo a controle.

> Versão atual: **0.6.0**

## Recursos

**Biblioteca**
- Detecta automaticamente jogos da **Steam**, **Epic Games** e **GOG**, além de pastas de jogos que você escolher.
- Adição manual por executável, com argumentos de inicialização e opção de executar como administrador.
- Favoritos, busca e ordenação por nome, recentes ou mais jogados.
- Tempo de jogo, última sessão e histórico de sessões por jogo.
- Dois estilos: **Clássico** (lista lateral) e **Moderno** (quadrados grandes com a capa no fundo).
- Temas **Aqua** e **Preto**.

**Capas e ícones**
- Capa automática buscada na Steam (com busca opcional na web quando a Steam não tem).
- Capas personalizadas em imagem, GIF animado ou vídeo (MP4, WEBM, MOV), inclusive arrastando e soltando.
- Trailer da Steam como capa em vídeo.
- Ícone do executável extraído automaticamente, ou ícone personalizado.

**Lojas e catálogos**
- **Loja Steam** dentro do launcher: destaques, busca, instalação pelo cliente da Steam com progresso, e sua biblioteca Steam (usando uma chave de API gratuita sua).
- **Aqua Game Hub**: catálogo de jogos open source (Sorcade) com instalação de pacotes ZIP de releases oficiais do GitHub, e jogos gratuitos do itch.io.

**Controle**
- Navegação completa pelo controle (XInput e Gamepad API), com teclado virtual nos campos de texto.
- **Menu rápido no jogo**: segure um botão do controle (padrão: L3, por 2 segundos) durante um jogo para abrir um painel com tempo de sessão, conquistas em andamento, "Voltar ao jogo" e "Sair do jogo". Botão e tempo são configuráveis.

**Conquistas**
- Marcos por horas de jogo, conquistas de biblioteca, hábitos e personalização, emblemas especiais por código e a platina **LEVIATÃ**.
- O progresso fica em um cofre assinado e preso ao computador, para não ser alterado editando arquivos.
- Notificações por cima do jogo quando você desbloqueia algo.

**Dados e backup**
- Backup da biblioteca e das capas em um ZIP, com tela de carregamento e progresso.
- Importação do backup na configuração inicial.
- Cópia automática da biblioteca e recuperação em caso de arquivo danificado.
- Limpeza de capas antigas.

## Requisitos

- Windows 10 ou 11.
- [Microsoft Edge WebView2 Runtime](https://go.microsoft.com/fwlink/p/?LinkId=2124703) (já vem instalado na maioria dos computadores com Windows 11 e em muitos com Windows 10).
- Para jogos da Steam, Epic ou GOG: o respectivo cliente instalado.

## Instalação

1. Baixe o `AquaLauncher.exe` na aba **Releases** deste repositório.
2. Execute o arquivo. Não precisa instalar.
3. Na primeira abertura, escolha **Criar novos arquivos** ou **Importar arquivos de save** (um backup ZIP criado pelo próprio launcher).
4. Clique em **Detectar jogos** para importar os jogos encontrados.

O Windows SmartScreen pode avisar sobre um aplicativo desconhecido, já que o executável não é assinado. Se você baixou do repositório oficial, escolha "Mais informações" e depois "Executar assim mesmo".

## Controles

| Ação | Teclado / mouse | Controle |
|---|---|---|
| Navegar | Setas ou Tab | Direcional / analógico esquerdo |
| Confirmar | Enter / clique | A |
| Voltar | Esc | B |
| Buscar | Clique na busca | X |
| Detectar jogos | Botão na tela | Y |
| Trocar aba / jogo anterior e próximo | Clique | LB / RB |
| Jogar o jogo selecionado | Botão Jogar | Start |
| Configurações | Botão no rodapé | Select |
| Tela cheia | F11 | |
| Menu rápido (durante um jogo) | | Segurar L3 por 2 s (configurável) |

## Onde ficam os dados

Tudo fica em `%APPDATA%\AquaLauncher`:

| Arquivo | Conteúdo |
|---|---|
| `biblioteca.json` | Jogos e configurações |
| `biblioteca.bak` | Cópia automática anterior |
| `capas\` | Capas, vídeos, miniaturas e ícones |
| `GameHub\` | Jogos instalados pelo Aqua Game Hub |
| `conquistas.dat` | Cofre de conquistas (preso a este computador) |
| `aqua.log` | Registro de erros, útil para reportar problemas |

O backup do launcher inclui a biblioteca e as capas. A chave da Steam, os jogos do Game Hub e as conquistas **não** entram no backup.

## Privacidade e segurança

- A chave da API da Steam é guardada **cifrada** (DPAPI do Windows) e só neste computador. Ela nunca é incluída em backups.
- O launcher acessa a internet para: capas e loja da Steam, catálogos do Game Hub, busca opcional de capas na web e downloads que você iniciar.
- Jogos do Game Hub são programas de terceiros. O Aqua só instala ZIPs de releases do GitHub, confere o SHA-256 quando o GitHub o publica e **nunca executa** instaladores automaticamente. Instale apenas projetos em que você confia.
- A busca de capas na web vem **desligada** em instalações novas (Configurações > Geral).

## Executando a partir do código

```bash
pip install pywebview psutil
python main.py
```

Os arquivos `main.py` e `index.html` precisam ficar na mesma pasta. O `tkinter` (já incluído no Python para Windows) é usado no menu sobreposto ao jogo.

### Gerando o executável

```bash
pip install pyinstaller
pyinstaller --noconsole --onefile --name AquaLauncher --add-data "index.html;." main.py
```

O executável é gerado em `dist\AquaLauncher.exe`.

## Solução de problemas

- **A janela não abre:** instale o WebView2 Runtime (link nos requisitos) e confira o `aqua.log`.
- **"O Aqua Launcher já está aberto":** só uma cópia pode rodar por vez.
- **Jogo da Steam não abre:** o cliente da Steam precisa estar instalado.
- **Capa em vídeo não toca:** use MP4 (H.264) ou WEBM.
- **Minha biblioteca Steam não aparece:** deixe "Detalhes dos jogos" como Público no perfil e confira a chave de API e o Steam ID.

## Licença

MIT
