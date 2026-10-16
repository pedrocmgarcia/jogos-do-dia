# Jogos do Dia

Um site para duas pessoas (Pessoa A e Pessoa B) registrarem os resultados do Termo, Dueto, Quarteto, Globle e Flagle e verem o placar uma da outra. Funciona no celular e não pede login.

## Arquivos

| Arquivo | Para que serve |
|---|---|
| `index.html` | O site inteiro. A lista de jogos fica no bloco "Edite aqui". |
| `config.js` | Os nomes das colunas e a configuração do Firebase. |
| `firestore.rules` | As regras de segurança do banco. Você cola no Firebase. |

Enquanto o `config.js` estiver sem a configuração do Firebase, o site roda em **modo de teste**: tudo funciona, mas os resultados ficam salvos só no aparelho.

---

## Passo 1: Criar o banco no Firebase (uns 10 min)

1. Entre em https://console.firebase.google.com com uma conta Google e clique em **Criar um projeto**. Dê um nome qualquer (ex.: `jogos-do-dia`). Você pode desativar o Google Analytics.
2. No menu da esquerda, abra **Criação > Firestore Database** e clique em **Criar banco de dados**.
   - Local: `southamerica-east1 (São Paulo)`.
   - Modo: **produção**.
3. Ainda no Firestore, abra a aba **Regras**, apague o que estiver lá, cole o conteúdo de `firestore.rules` e clique em **Publicar**.
4. Volte para a página inicial do projeto (ícone de engrenagem > **Configurações do projeto**). Em **Seus apps**, clique no ícone **Web** (`</>`), dê um apelido e **não** marque Firebase Hosting.
5. O Firebase mostra um bloco `const firebaseConfig = { ... }`. Copie só o objeto e cole no `config.js`, no lugar de `null`:

   ```js
   export const firebaseConfig = {
     apiKey: "...",
     authDomain: "...",
     projectId: "...",
     storageBucket: "...",
     messagingSenderId: "...",
     appId: "...",
   };
   ```

6. No mesmo `config.js`, troque `"Pessoa A"` e `"Pessoa B"` pelos nomes que vocês quiserem ver nas colunas.

> Sobre a configuração do Firebase: ela vai ficar visível no site e no repositório, e isso é o esperado para apps Web do Firebase (ela identifica o projeto, não dá acesso de administrador). Quem protege os dados são as regras do passo 3. Mesmo assim, não cole esses valores em chats nem em ferramentas de IA: edite o `config.js` direto no seu computador ou no GitHub.

## Passo 2: Publicar no GitHub Pages (uns 10 min)

1. Entre em https://github.com e crie um repositório novo (**New repository**), por exemplo `jogos-do-dia`. Ele precisa ser **Public** para o GitHub Pages gratuito funcionar.
2. Na página do repositório, clique em **Add file > Upload files**, arraste `index.html`, `config.js`, `firestore.rules` e este `LEIA-ME.md`, e clique em **Commit changes**.
3. Vá em **Settings > Pages**. Em **Branch**, escolha `main` e a pasta `/ (root)`, e clique em **Save**.
4. Depois de 1 ou 2 minutos, o endereço aparece no topo dessa página, no formato `https://SEU-USUARIO.github.io/jogos-do-dia/`.

## Passo 3: Proteger a chave (recomendado, 3 min)

Limite a chave do Firebase para funcionar só no seu site:

1. Abra https://console.cloud.google.com/apis/credentials e selecione o projeto do Firebase no topo.
2. Clique na chave chamada **Browser key (auto created by Firebase)**.
3. Em **Restrições de aplicativos**, escolha **Sites** e adicione `https://SEU-USUARIO.github.io/*`.
4. Salve.

## Passo 4: Usar

1. Mande o link para a outra pessoa.
2. Na primeira vez, cada pessoa toca em **Sou Pessoa A** ou **Sou Pessoa B**. O celular lembra a escolha (dá para trocar depois).
3. Depois de jogar, toque em **Registrar** no jogo e cole o texto de compartilhar. O número de tentativas se preenche sozinho quando dá.
4. Dica: no celular, use "Adicionar à tela inicial" no navegador para abrir o site como se fosse um app.

## Bom saber

- **Não tem senha.** Quem tiver o link consegue ver e registrar resultados nas duas colunas. Para duas pessoas que confiam uma na outra, isso basta. Se um dia precisar, dá para adicionar um código de acesso.
- **O repositório é público.** Qualquer pessoa pode ver o código do site. Os resultados ficam no Firebase, não no GitHub.
- **Custo:** o uso de duas pessoas fica muito abaixo do limite gratuito do Firebase (plano Spark) e do GitHub Pages.
- **Para mudar a lista de jogos,** edite o bloco "Edite aqui" no `index.html` e a função `jogos()` no `firestore.rules` (e publique as regras de novo no Firebase).
