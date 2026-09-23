# Controle Financeiro · CD 1 (501) / CD 2 (507)

**Acessar a aplicação:** https://cpdnagumocd.github.io/Controle-financeiro/

Registro de pagamentos de descarga (NFS-e / RPS), filtros, fluxo de caixa diário e mensal e controle de usuários por CD.
Os dados ficam no **Firebase** (Authentication + Cloud Firestore) e a página é publicada no **GitHub Pages**.

| Arquivo | Para que serve |
|---|---|
| `index.html` | A aplicação completa (telas, logos, lógica). |
| `firebase-config.js` | As chaves do **seu** projeto Firebase — é o único arquivo que você edita. |
| `firestore.rules` | Regras de segurança do banco (quem pode ler/gravar cada CD). |

---

## 1. Criar o projeto no Firebase (uma vez só)

1. Acesse **https://console.firebase.google.com** com a conta Google da empresa e clique em **Adicionar projeto**.
   Nome sugerido: `controle-financeiro-nagumo`. O Google Analytics pode ficar **desativado**. Clique em **Criar projeto**.
2. **Login dos usuários** — menu *Criação* > **Authentication** > **Vamos começar** > **E-mail/senha** >
   ative apenas a primeira opção (**E-mail/senha**) > **Salvar**.
3. **Banco de dados** — menu *Criação* > **Firestore Database** > **Criar banco de dados** >
   local **southamerica-east1 (São Paulo)** > **Iniciar no modo de produção** > **Criar**.
4. **Regras de segurança** — ainda no Firestore, aba **Regras**: apague todo o texto, cole o conteúdo do arquivo
   `firestore.rules` e clique em **Publicar**.
5. **Chaves do app** — clique na engrenagem ⚙ > **Configurações do projeto** > em *Seus apps* clique no ícone **`</>`** (Web) >
   apelido `controle-financeiro` > **Registrar app** (não precisa marcar Hosting).
   Aparece um bloco `const firebaseConfig = { apiKey: "...", authDomain: "...", ... }`.
   Copie cada valor para o campo correspondente em **`firebase-config.js`** (troque os textos `COLE_AQUI_...`, mantendo as aspas).

## 2. Publicar no GitHub Pages

1. Em **https://github.com** clique em **New repository**. Nome: `controle-financeiro`. Visibilidade: **Public**. **Create repository**.
2. Clique em **uploading an existing file**, arraste `index.html`, `firebase-config.js` (já preenchido), `firestore.rules` e `README.md`
   e clique em **Commit changes**.
3. No repositório: **Settings** > **Pages** > *Source*: **Deploy from a branch** > Branch **main** e pasta **/ (root)** > **Save**.
4. Em 1–2 minutos o link fica pronto no topo dessa página:
   `https://SEU-USUARIO.github.io/controle-financeiro/`
5. No Firebase: **Authentication** > **Configurações** > **Domínios autorizados** > **Adicionar domínio** > `SEU-USUARIO.github.io`.

> Para atualizar a aplicação no futuro, basta enviar o novo `index.html` pelo mesmo caminho (**Add file** > **Upload files**).
> O `firebase-config.js` não precisa ser enviado de novo.

## 3. Primeiro acesso

1. Abra o link. Aparece **Configuração inicial**: crie o usuário **administrador** (nome, login e senha).
2. **Trazer o histórico da planilha** (opcional, uma vez): aba **Usuários** > **Restaurar backup** > escolha o arquivo
   `historico_cd2_para_importar.json` (fica na pasta *Projeto financeiro* do computador — **não** suba esse arquivo no GitHub) > **Adicionar**.
3. Se você já usou a versão *arquivo único* (`Controle Financeiro.html`), baixe o backup nela e restaure aqui com **Adicionar**.
4. Crie os operadores na aba **Usuários**:
   - **Administrador** — acesso total aos dois CDs, cria/exclui usuários e exclui lançamentos.
   - **Perfil CD** — lança, edita e consulta somente nos CDs marcados (CD 1 · 501 e/ou CD 2 · 507).

## 4. Backup

Aba **Usuários** > **Baixar backup**: baixa um arquivo `.json` com **todos os lançamentos dos dois CDs** e a lista de usuários.
Guarde numa pasta segura (sugestão: toda semana).
**Restaurar backup** oferece duas opções: **Adicionar** (junta ao que existe) ou **Substituir tudo** (volta exatamente ao backup).
Usuários e senhas não são alterados por um restauro.

## Bom saber

- **Senhas**: cada usuário troca a própria senha no menu com o seu nome > *Alterar minha senha*.
  Se alguém esquecer, o administrador exclui o usuário e cria um login novo (ex.: `joao.silva2`), ou apaga a conta antiga em
  Firebase > Authentication e cria de novo com o mesmo login.
- **O login não pode ser renomeado** depois de criado (crie um novo, se precisar).
- **Sessão**: ao fechar o navegador é preciso entrar de novo.
- **Tempo real**: quando alguém lança um pagamento, a lista e o fluxo abertos nos outros computadores se atualizam sozinhos.
- **Segurança**: as chaves do `firebase-config.js` são públicas por natureza (ficam visíveis no navegador); quem protege os dados são
  as **regras** do `firestore.rules` — sem login ativo e cadastrado, ninguém lê nem grava nada, e cada Perfil CD só acessa o seu CD.
- **Custo**: o plano gratuito do Firebase (Spark) é suficiente — cada mês de lançamentos é um único documento, então abrir o fluxo
  de um mês consome 1 leitura (limite gratuito: 50 mil leituras e 20 mil gravações por dia).
