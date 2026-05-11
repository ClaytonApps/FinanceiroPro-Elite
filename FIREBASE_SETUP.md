# 🔥 Configuração do Firebase — Passo a Passo

Este guia te leva do zero ao app rodando no Firebase com login Google e sincronização na nuvem em ~10 minutos. Tudo gratuito.

---

## 📋 Pré-requisitos

- Conta Google ativa (qualquer Gmail)
- Node.js instalado (https://nodejs.org)
- Pasta do projeto baixada localmente

---

## Etapa 1 — Criar o projeto no Firebase Console (3 min)

### 1.1. Acesse o console

https://console.firebase.google.com

### 1.2. Criar projeto

1. Clique em **"Adicionar projeto"** (ou "Add project")
2. **Nome do projeto**: `financeiropro-elite` (pode ser outro)
3. Continue. Se aparecer "Google Analytics" → você pode **desativar** (não precisamos)
4. Aguarde a criação. Clique em **Continuar**

### 1.3. Anotar o Project ID

Após criar, vá em **⚙️ Configurações do projeto** (engrenagem ao lado de "Visão geral").

Anote o **ID do projeto** (algo como `financeiropro-elite-abc12`). Você vai precisar dele.

---

## Etapa 2 — Habilitar Authentication (Login Google) (2 min)

### 2.1. Abrir Authentication

No menu lateral esquerdo do console: **Build → Authentication**

### 2.2. Ativar o serviço

1. Clique em **"Começar"** (ou "Get started")
2. Aba **"Sign-in method"**
3. Clique em **"Google"** na lista
4. Ative o **toggle "Habilitar"**
5. **Email de suporte**: escolha o seu email
6. **Salvar**

---

## Etapa 3 — Habilitar Firestore (banco de dados) (2 min)

### 3.1. Abrir Firestore

No menu lateral: **Build → Firestore Database**

### 3.2. Criar banco

1. Clique em **"Criar banco de dados"**
2. **Localização**: escolha **`southamerica-east1` (São Paulo)** — mais rápido no Brasil
3. **Modo**: escolha **"Iniciar em modo de produção"** (regras vão ser configuradas pelo nosso arquivo)
4. **Habilitar**

### 3.3. Regras de segurança

Aba **"Regras"** dentro do Firestore. Cole o conteúdo do arquivo `firestore.rules` do projeto:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
      match /{document=**} {
        allow read, write: if request.auth != null && request.auth.uid == userId;
      }
    }
  }
}
```

Clique em **Publicar**.

> Isso garante que cada usuário só pode ler/escrever os próprios dados.

---

## Etapa 4 — Obter a configuração da Web App (2 min)

### 4.1. Adicionar app Web

1. Volte em **⚙️ Configurações do projeto**
2. Aba **"Geral"** → role até **"Seus apps"**
3. Clique no ícone **`</>`** (Web)
4. **Apelido do app**: `FinanceiroPro Web`
5. ✅ Marque **"Configurar o Firebase Hosting"** (opcional, mas ajuda)
6. **Registrar app**

### 4.2. Copiar a config

Vai aparecer um código tipo:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSyAB123...",
  authDomain: "financeiropro-elite.firebaseapp.com",
  projectId: "financeiropro-elite-abc12",
  storageBucket: "financeiropro-elite.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123def456"
};
```

**Copie esses valores.** Você vai colar no `index.html` na próxima etapa.

---

## Etapa 5 — Colar a configuração no app (1 min)

### 5.1. Abrir `index.html`

Procure por:

```javascript
window.FIREBASE_CONFIG = {
  apiKey: "PLACEHOLDER",
  authDomain: "",
  projectId: "",
  storageBucket: "",
  messagingSenderId: "",
  appId: ""
};
```

### 5.2. Substituir pelos seus valores

Cole os valores que copiou da Etapa 4.2 no lugar dos placeholders. Salve.

---

## Etapa 6 — Atualizar `.firebaserc` (30 segundos)

Abra `.firebaserc` e substitua `SEU-PROJECT-ID-AQUI` pelo seu Project ID real:

```json
{
  "projects": {
    "default": "financeiropro-elite-abc12"
  }
}
```

---

## Etapa 7 — Instalar Firebase CLI e fazer deploy (3 min)

### 7.1. Instalar a CLI

Abra o terminal (PowerShell ou CMD) na pasta do projeto:

```bash
npm install -g firebase-tools
```

### 7.2. Login

```bash
firebase login
```

Abre o navegador, você loga com a mesma conta Google do projeto.

### 7.3. Deploy

```bash
firebase deploy
```

Em ~30 segundos, ele retorna duas URLs:

```
Hosting URL: https://financeiropro-elite-abc12.web.app
            https://financeiropro-elite-abc12.firebaseapp.com
```

**Pronto! App no ar com sincronização na nuvem.** 🎉

---

## ✅ Como testar

1. Acesse a URL `.web.app` no navegador
2. Clique em **"Entrar com Google"** no canto superior direito
3. Autorize o login
4. Lance algumas transações
5. **Teste fundamental**: limpe o cache do navegador (ou abra em outro dispositivo) e faça login novamente. Suas transações vão estar lá. ✅

---

## 🔄 Deploys futuros

Depois de qualquer mudança no `index.html`:

```bash
firebase deploy --only hosting
```

Se mudar as regras do Firestore:

```bash
firebase deploy --only firestore:rules
```

---

## 💡 Dicas e truques

### Domínio próprio (opcional)

No console Firebase → **Hosting** → **Adicionar domínio personalizado**. Suporta `seudominio.com.br`.

### Preview channels (testar antes de publicar)

```bash
firebase hosting:channel:deploy preview
```

Gera uma URL temporária pra testar sem afetar produção.

### Ver uso do plano grátis

Console Firebase → **Uso e faturamento**. Mostra quanto você consumiu (vai ser ~0% para uso pessoal).

### Reverter deploy

Console → **Hosting** → aba "Histórico" → clique em "Voltar" em qualquer versão anterior.

---

## ⚠️ Problemas comuns

### "Permission denied" no Firestore

→ As regras não foram publicadas. Refaça a Etapa 3.3.

### "Login não funciona"

→ Authentication não foi ativada com provider Google. Refaça a Etapa 2.

### "Domínio não autorizado" no login Google

→ No console → Authentication → Settings → Authorized domains: adicione seu domínio (`.web.app` já está autorizado por padrão).

### Quota exceeded

→ Você passou do plano grátis (improvável). Veja em **Uso e faturamento**.

---

## 🛡️ Segurança — bom saber

- A `apiKey` do Firebase **não é secreta**. Ela identifica o projeto, não autoriza acesso. As regras do Firestore (Etapa 3.3) é que impedem acesso indevido.
- Pode commitar a config no GitHub sem problema.
- Cada usuário vê apenas os próprios dados, graças à regra `request.auth.uid == userId`.

---

## 📞 Suporte

Encontrou problema? Abra uma issue no repo: https://github.com/ClaytonApps/FinanceiroPro-Elite/issues
