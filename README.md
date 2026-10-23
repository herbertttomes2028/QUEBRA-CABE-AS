# 🧩 Quebra-Cabeça a Dois

Jogo de quebra-cabeça cooperativo online: duas pessoas, cada uma no seu celular (ou computador), montam **a mesma imagem ao mesmo tempo**, vendo os movimentos uma da outra em tempo real.

- Feito para **celular** (toque, tela em pé), mas funciona também no computador.
- **Tabuleiro grande**: ele ocupa quase toda a largura da tela, para você enxergar bem a imagem sendo montada.
- Não precisa instalar nada no seu computador: tudo é feito pelos sites do **GitHub** e do **Render**.
- Cada jogador digita o **próprio nome**; a pessoa que cria escolhe a **imagem** e a **quantidade de peças**.
- O código da sala é **gerado automaticamente** e o amigo entra por link ou por código.

---

## Como o jogo funciona

1. Quem cria a partida digita o **nome**, toca em **Criar partida**, escolhe a **imagem** e a **quantidade de peças** (6, 12, 20, 30 ou 48) e o jogo gera a sala com um código de 4 caracteres (ex.: `K7MQ`).
2. Ela envia o **link ou o código** (botões *Convidar* e *WhatsApp*) para o amigo.
3. O amigo abre o link, **digita o nome dele** e toca em **Entrar** (ou digita o código na tela inicial). O nome de cada um aparece no topo e nas peças que a pessoa estiver segurando.
4. As peças começam **embaralhadas e giradas** na bandeja, embaixo do tabuleiro. Na bandeja elas ficam **pequenas** (para sobrar espaço para o tabuleiro) e **crescem até o tamanho cheio quando você as arrasta**.
5. **Arraste** uma peça até o tabuleiro. Ao soltar perto do lugar certo (e com a peça na posição certa), ela **encaixa e trava**. Uma peça solta fora da bandeja continua no tamanho cheio; se você a devolver para a bandeja, ela volta a ficar pequena.
6. **Toque** numa peça para escolhê-la (ela ganha um contorno colorido, sem crescer, para não cobrir as vizinhas) e use o botão **↻ Girar**. Cada peça aceita **até 3 giros** por vez; depois disso é preciso encaixar ou soltá-la (ao soltar, os giros são renovados).
7. O **triângulo ▲** desenhado em cada peça mostra qual lado é o "de cima". Ajuda muito nas peças brancas ou de uma cor só: a peça está na posição certa quando o ▲ aponta para cima.
8. **Exclusividade:** enquanto uma pessoa segura uma peça (contorno colorido e etiqueta com o nome dela), a outra **não consegue** pegá-la, movê-la nem girá-la.
9. **💡 Lâmpada:** o botão é só o ícone da lâmpada. Ao apertar, a **imagem completa aparece esmaecida no tabuleiro, atrás das peças, por 4 segundos** e depois some sozinha. Cada jogador pode usar **10 vezes por partida** (o número pequeno no botão mostra quantas restam). Apertar de novo enquanto a imagem está visível não gasta outra dica, e só quem apertou vê a imagem. Recarregar a página não renova as dicas.
10. Quando todas as peças encaixam, aparece a tela de vitória com o **tempo** e quantas peças cada um (pelo nome) encaixou.

O menu (☰) permite copiar o link, **trocar a imagem ou a quantidade de peças** e recomeçar. Ao trocar ou recomeçar, as dicas voltam a 10 para cada um.

---

## Quantidade de peças

| Peças | Grade | Nível | Tabuleiro na tela* | Peça montada* | Peça na bandeja* |
|---|---|---|---|---|---|
| 6 | 2 × 3 | Bem fácil | ~310 px | ~155 px | ~57 px |
| 12 | 3 × 4 | Fácil | ~345 px | ~115 px | ~47 px |
| 20 | 4 × 5 | Médio | ~345 px | ~85 px | ~45 px |
| 30 | 5 × 6 | Difícil | ~330 px | ~65 px | ~44 px |
| 48 | 6 × 8 | Desafio | ~260 px | ~42 px | ~37 px (pequena; melhor em tela grande) |

\* Em um celular de 390 px de largura, com o aparelho em pé. Antes desta versão, com 12 peças, o tabuleiro tinha cerca de 227 px e cada peça montada, 75 px.

As peças são sempre quadradas. Como cada grade tem uma proporção um pouco diferente (por exemplo, 4 × 5 é mais "quadrada" que 3 × 4), o jogo **recorta o centro da imagem** para encaixar. Com imagens em pé 3:4 (como as incluídas), o recorte é de apenas 6% a 11% nas bordas. O botão 💡 e o tabuleiro sempre mostram a imagem já recortada, exatamente como será montada.

---

## Estrutura do projeto

```
quebra-cabeca/
├── package.json          dependências e comando de início (npm start)
├── server.js             servidor (Express + Socket.IO): regras e sincronização
├── render.yaml           (opcional) configuração pronta para o Render
├── .gitignore
├── README.md
└── public/
    ├── index.html        telas do jogo
    ├── style.css         visual
    ├── game.js           lógica do jogo no navegador
    └── imagens/
        ├── angel.jpg
        ├── batman.jpg
        ├── jesus.jpg
        ├── stitch-e-angel.jpg
        └── stitch.jpg
```

---

## Passo 1 — Suas imagens

O projeto já vem com as **5 imagens** que você enviou, convertidas para JPG (mais leves, de 100 a 190 KB cada, sem perda visível de qualidade).

Para trocar ou acrescentar imagens, mexa na pasta `public/imagens/`:

- O jogo mostra **todas** as imagens `.jpg`, `.jpeg`, `.png` ou `.webp` da pasta (até 12). Não precisa mudar nenhum código.
- O nome do arquivo vira o rótulo na tela: `stitch-e-angel.jpg` → "Stitch e Angel".
- **Não funcionam:** GIF, SVG, HEIC (foto do iPhone) e AVIF. Converta para JPG ou PNG.

**Dicas para ficar leve e bonito:**

- Formato ideal: **em pé (3:4)**, por exemplo **900 × 1200 pixels**.
- Arquivo de preferência **abaixo de 500 KB**. Se estiver em PNG e pesado, salve como JPG.
- Imagens com **fundo branco** funcionam (o tabuleiro tem um tom lilás e cada peça tem borda para você enxergar onde estão), mas a montagem fica mais difícil nas partes só brancas. Para essas peças, use o triângulo ▲ para saber qual lado é o de cima.

---

## Passo 2 — Envie o projeto para o GitHub (pelo site)

> **Importante:** o GitHub **guarda** o código, mas **não executa** o servidor do jogo (o GitHub Pages só serve páginas simples). Quem coloca o jogo no ar é o **Render**, no Passo 3, lendo o código direto do seu repositório.

1. Entre em <https://github.com> e faça login (ou crie uma conta gratuita).
2. Clique no **+** no canto superior direito → **New repository**.
3. Em *Repository name* escreva, por exemplo, `quebra-cabeca`. Deixe **Public** (ou Private, funciona nos dois) e clique em **Create repository**.
4. Na página do repositório vazio, clique em **uploading an existing file** (ou *Add file → Upload files*).
5. **Descompacte** o `.zip` do projeto no seu aparelho e **arraste o conteúdo da pasta `quebra-cabeca`** (os arquivos `server.js`, `package.json`, `README.md`, `render.yaml`, `.gitignore` e a pasta `public`) para a área de upload.
   - Os arquivos precisam ficar **na raiz** do repositório (`server.js` e `package.json` logo na primeira página, não dentro de outra pasta).
   - A pasta `public` (com `imagens` dentro) precisa subir **junto**. Se o seu navegador não aceitar arrastar pastas, use *Add file → Create new file*, digite o caminho no nome (por exemplo `public/index.html`) e cole o conteúdo; as imagens você envia pelo *Upload files* dentro da pasta `public/imagens`.
6. Role até o fim e clique em **Commit changes**.

Confira: no repositório você deve ver `server.js`, `package.json` e a pasta `public` na primeira tela.

---

## Passo 3 — Coloque o jogo no ar no Render (grátis)

1. Entre em <https://render.com> e crie uma conta (pode usar o login do GitHub).
2. Clique em **New +** → **Web Service**.
3. Escolha **Build and deploy from a Git repository** e conecte sua conta do GitHub (autorize o acesso ao repositório `quebra-cabeca`).
4. Selecione o repositório e clique em **Connect**.
5. Preencha:

   | Campo | Valor |
   |---|---|
   | **Name** | `quebra-cabeca` (vira parte do endereço) |
   | **Region** | a mais próxima (ex.: *Ohio* ou *Virginia*) |
   | **Branch** | `main` |
   | **Runtime / Language** | `Node` |
   | **Build Command** | `npm install` |
   | **Start Command** | `npm start` |
   | **Instance Type** | `Free` |

6. (Opcional) Em *Advanced* → **Health Check Path**: `/health`.
7. Clique em **Create Web Service** e aguarde o *deploy* (1 a 3 minutos). Quando aparecer **Live**, o endereço estará no topo da página do serviço, algo como `https://quebra-cabeca.onrender.com`.

> **Alternativa mais rápida:** o projeto traz um `render.yaml`. No Render, use **New + → Blueprint**, escolha o repositório e confirme. Ele preenche tudo acima sozinho.

---

## Atualizando um jogo que já está no ar

Se você já publicou uma versão anterior, não precisa refazer nada no Render:

1. No GitHub, abra o repositório → **Add file → Upload files**.
2. Arraste os arquivos novos **com o mesmo nome** (`server.js`, `public/index.html`, `public/style.css`, `public/game.js`, `README.md`). Eles substituem os antigos. Para a pasta `public`, arraste o conteúdo mantendo a estrutura (ou entre na pasta `public` do repositório antes de enviar os três arquivos de dentro dela).
3. Entre em `public/imagens`, **apague** as imagens antigas (`imagem1.jpg` a `imagem4.jpg`: abra cada arquivo, ícone de lixeira → *Commit changes*) e envie as novas.
4. Clique em **Commit changes**. O Render percebe a mudança e publica sozinho em 1 a 3 minutos (status *Deploying* → *Live*).
5. Recarregue o jogo no celular. Se ainda aparecer a versão antiga, feche a aba e abra de novo.

---

## Passo 4 — Jogar

1. Abra o endereço do Render no celular.
2. Digite o **seu nome**, toque em **Criar partida**, escolha a imagem e a quantidade de peças e toque em **Criar partida** de novo.
3. Toque em **Convidar** (ou **WhatsApp**) e mande para o amigo.
4. O amigo abre o link, digita o nome dele e toca em **Entrar**. O relógio começa quando os dois estão na sala.

---

## Como testar

### Antes de chamar o amigo (sem instalar nada)

Depois de publicado no Render:

1. No computador, abra o endereço do jogo em **duas abas** (ou uma aba normal e uma anônima).
2. Na primeira aba, digite um nome e crie a partida. Copie o código.
3. Na segunda aba, digite outro nome e o código em **Entrar com código** (ou abra o link `…/?sala=CÓDIGO`).
4. Mova uma peça numa aba e veja se ela se mexe na outra, com a etiqueta do nome. Tente pegar, na segunda aba, uma peça que a primeira está segurando: o jogo deve avisar.
5. Aperte a lâmpada 💡: a imagem deve aparecer esmaecida atrás das peças, no tabuleiro, e sumir sozinha depois de 4 segundos. O número no botão cai de 10 para 9 (só na tela de quem apertou).
6. Arraste uma peça da bandeja: ela deve crescer enquanto você a move e voltar a ficar pequena se você a soltar de volta na bandeja.

### No celular

1. Abra o endereço no celular e crie a partida.
2. No computador (ou em outro celular), entre pelo link.
3. Teste: arrastar com o dedo, tocar numa peça e girar, encaixar, a lâmpada, bloquear e desbloquear a tela (o jogo reconecta sozinho) e terminar o quebra-cabeça.
4. Experimente 6, 12 e 20 peças. Se for jogar com 30 ou 48, confira se o tamanho das peças está confortável para o seu dedo.

### No seu computador, se um dia tiver o Node.js instalado (opcional)

```
npm install
npm start
```

Abra `http://localhost:3000` em duas abas e siga o mesmo teste acima.

---

## Se algo não funcionar

- **A primeira abertura demora (30–60 s):** é normal no plano gratuito do Render, que "dorme" depois de uns 15 minutos sem uso. Abra o link antes de chamar o amigo.
- **O link de convite pede o nome em vez de entrar direto:** é o esperado. O amigo digita o nome e toca em **Entrar**.
- **"Não encontramos essa sala":** confira o código (4 caracteres, letras e números). A sala também some se o Render reiniciar o serviço; é só criar outra.
- **"Essa sala já tem duas pessoas":** a sala comporta exatamente duas pessoas. Se alguém caiu, ao voltar pelo mesmo link ela retoma o lugar (e as dicas já usadas continuam usadas).
- **Aparece "Reconectando…":** a internet oscilou. O jogo volta sozinho e mantém o progresso.
- **"Nenhuma imagem encontrada":** a pasta `public/imagens` está vazia ou foi enviada fora do lugar no GitHub.
- **A imagem não aparece:** verifique se a extensão é `.jpg`, `.jpeg`, `.png` ou `.webp` e se o arquivo abre normalmente.
- **Ainda vejo as imagens ou o visual antigos depois de atualizar:** espere o Render marcar **Live** e recarregue a página (feche e abra a aba).
- **Jogo na horizontal:** funciona, mas as peças ficam menores. O ideal é jogar com o celular **em pé**.

---

## Checklist antes de publicar

- [ ] As imagens que quero estão em `public/imagens/` e as de exemplo antigas (`imagem1.jpg` a `imagem4.jpg`) foram apagadas.
- [ ] As imagens são leves (de preferência abaixo de 500 KB) e abrem normalmente.
- [ ] No GitHub, `server.js` e `package.json` aparecem na **primeira tela** do repositório (não dentro de outra pasta).
- [ ] A pasta `public` subiu com `index.html`, `style.css`, `game.js` e a pasta `imagens`.
- [ ] No Render: Build Command `npm install` e Start Command `npm start`.
- [ ] O deploy terminou como **Live** e `https://SEU-ENDERECO.onrender.com/health` mostra `ok`.
- [ ] Abri o jogo em duas abas com nomes diferentes: criar partida, entrar, mover uma peça e ver nas duas telas.
- [ ] Testei a quantidade de peças que pretendo usar (6, 12, 20, 30 ou 48) no celular.
- [ ] Testei girar (máx. 3 giros), encaixar e a tela de vitória com os nomes.
- [ ] Testei a lâmpada 💡: a imagem aparece atrás das peças, some sozinha depois de 4 segundos e cada jogador tem 10 usos.
- [ ] Conferi que o tabuleiro está grande o bastante na tela do celular e que as peças da bandeja são fáceis de pegar com o dedo.
- [ ] Testei a exclusividade (a segunda pessoa não consegue pegar a peça que a primeira segura).
- [ ] Combinei com o amigo de abrir o link um pouco antes (por causa do "sono" do plano gratuito).

Bom jogo! 🧩
