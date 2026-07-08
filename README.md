# Como deixar o Controle de Gastos salvando na nuvem e acessivel pela internet

Isso é feito em duas partes:

1. **Supabase** — onde os dados ficam guardados de verdade (para nao depender so deste computador).
2. **GitHub Pages** — onde o site fica publicado, com um link que voce pode acessar de qualquer lugar.

Leva uns 10 a 15 minutos, seguindo os passos abaixo com calma.

---

## Parte 1 — Criar o banco de dados no Supabase

1. Acesse **supabase.com** e crie uma conta gratuita (pode entrar com Google ou GitHub).
2. Clique em **New project**.
   - Escolha um nome, por exemplo `controle-gastos`.
   - Crie uma senha para o banco (guarde-a em algum lugar, mas voce nao vai precisar dela no dia a dia).
   - Escolha a regiao mais proxima do Brasil (ex: South America).
   - Clique em **Create new project** e espere 1-2 minutos ele terminar de preparar.
3. No menu do lado esquerdo, clique em **SQL Editor**.
4. Clique em **New query**.
5. Abra o arquivo **supabase-setup.sql** (que veio junto com este guia), copie todo o conteudo e cole na tela do SQL Editor.
6. Clique no botao **RUN** (ou aperte Ctrl+Enter). Deve aparecer "Success. No rows returned".
   - Isso cria a tabela `contas`, que é onde cada conta cadastrada vai ficar guardada.

### Pegar a URL e a chave do projeto

1. No menu esquerdo, clique em **Project Settings** (icone de engrenagem) e depois em **API** (ou **Data API**, dependendo da versao).
2. Copie dois valores:
   - **Project URL** (algo como `https://xxxxxxxx.supabase.co`)
   - **anon public** key (uma chave longa de letras e numeros)
3. Guarde os dois em algum lugar, voce vai usar no proximo passo.

---

## Parte 2 — Colar a configuracao no arquivo do site

1. Abra o arquivo **controle-gastos.html** com o Bloco de Notas (ou qualquer editor de texto simples).
2. Use Ctrl+F para procurar por: `COLE_AQUI_A_URL_DO_SEU_PROJETO_SUPABASE`
3. Troque o texto entre aspas pela **Project URL** que voce copiou. Deve ficar assim, por exemplo:
   ```
   var SUPABASE_URL = "https://xxxxxxxx.supabase.co";
   ```
4. Procure por `COLE_AQUI_A_CHAVE_ANON_PUBLIC` e troque pela chave **anon public**:
   ```
   var SUPABASE_ANON_KEY = "eyJhbGciOि...(a chave inteira aqui)";
   ```
5. Salve o arquivo.

A partir de agora, ao abrir o site, ele vai salvar e ler as contas direto do Supabase — de qualquer computador que acessar o mesmo site, os dados serao os mesmos.

> Dica: se voce quiser, pode testar abrindo o arquivo `controle-gastos.html` direto no seu computador (duplo clique) antes mesmo de subir para o GitHub, so para conferir se esta tudo funcionando com o Supabase.

---

## Parte 3 — Publicar no GitHub Pages

1. Acesse **github.com** e crie uma conta gratuita, se ainda nao tiver.
2. Clique no botao **+** no canto superior direito e em **New repository**.
   - De um nome, por exemplo `controle-gastos`.
   - Deixe marcado como **Public**.
   - Clique em **Create repository**.
3. Na tela do repositorio recem-criado, clique em **uploading an existing file** (ou **Add file > Upload files**).
4. Arraste o arquivo **controle-gastos.html** (ja com a URL e a chave preenchidas) para a area de upload.
5. **Importante:** renomeie o arquivo para **index.html** antes de confirmar o envio (clique no nome do arquivo na tela de upload para editar). Isso faz o GitHub Pages abrir ele automaticamente.
6. Clique em **Commit changes** (pode manter as opcoes padrao).

### Ativar o GitHub Pages

1. Dentro do repositorio, clique em **Settings** (no menu de cima).
2. No menu esquerdo, clique em **Pages**.
3. Em **Build and deployment > Source**, escolha **Deploy from a branch**.
4. Em **Branch**, escolha **main** e a pasta **/ (root)**. Clique em **Save**.
5. Espere 1 a 2 minutos e atualize a pagina. Vai aparecer uma mensagem: "Your site is live at https://seu-usuario.github.io/controle-gastos/".
6. Esse é o link do seu site! Pode salvar como favorito no navegador ou na tela inicial do celular.

---

## Aviso importante sobre seguranca

Esse jeito de configurar é simples e funciona bem para uso pessoal, mas é bom saber:

- A chave "anon public" do Supabase fica visivel para qualquer pessoa que olhar o codigo do site (é assim mesmo que o Supabase funciona para sites simples como este).
- Com a configuracao do arquivo `supabase-setup.sql`, **qualquer pessoa que tiver o link do seu site** conseguiria, em teoria, ler ou alterar as contas.
- Para um controle de gastos pessoal, isso normalmente nao é um problema (nao ha dados como senhas ou numeros de cartao), mas evite compartilhar o link publicamente (ex: redes sociais).
- Se no futuro voce quiser mais seguranca (por exemplo, pedir login e senha para abrir o site), e possivel evoluir para isso usando o recurso de autenticacao do Supabase — so avisar que se pode ajudar a configurar.

---

## Resumo rapido

| Passo | Onde |
|---|---|
| Criar projeto e tabela | Supabase |
| Copiar URL + chave anon | Supabase > Project Settings > API |
| Colar URL + chave no HTML | Editor de texto no seu computador |
| Subir o arquivo como `index.html` | GitHub (repositorio novo) |
| Ativar o site | GitHub > Settings > Pages |
| Acessar de qualquer lugar | Link `https://seu-usuario.github.io/nome-do-repositorio/` |
