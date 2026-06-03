# 🚀 Guia de Deploy — Eco Arandor Online V17
## GitHub + Render (Multiplayer Online)

---

## 1️⃣ Subir para o GitHub

### Primeira vez (novo repositório)

```bash
# Na pasta do projeto:
git init
git add .
git commit -m "Eco Arandor V17 - gráficos melhorados"

# Crie o repositório em https://github.com/new  (nome: eco-arandor-online)
# Depois cole os comandos que o GitHub mostrar, tipo:
git remote add origin https://github.com/SEU_USUARIO/eco-arandor-online.git
git branch -M main
git push -u origin main
```

### Atualizar versão futura

```bash
git add .
git commit -m "Descrição da mudança"
git push
```

> O Render vai **redeploy automático** a cada push no main! ✅

---

## 2️⃣ Deploy no Render (grátis)

1. Acesse **https://render.com** e crie uma conta
2. Clique em **"New +"** → **"Web Service"**
3. Conecte sua conta GitHub e selecione o repositório `eco-arandor-online`
4. Configure assim:

| Campo | Valor |
|-------|-------|
| **Name** | eco-arandor-online |
| **Environment** | Node |
| **Build Command** | `npm install` |
| **Start Command** | `npm start` |
| **Plan** | Free |

5. Clique **"Create Web Service"**
6. Aguarde o deploy (~2-3 minutos)
7. Sua URL será: `https://eco-arandor-online.onrender.com`

---

## ⚠️ Importante: Persistência de Dados no Render

O plano gratuito do Render **não salva arquivos** entre deploys. O `database.json` some quando o serviço reinicia.

### Soluções:

**Opção A — MongoDB Atlas (grátis, recomendado)**
- Crie conta em https://www.mongodb.com/atlas
- Crie cluster gratuito (M0)
- Adicione a variável de ambiente `MONGODB_URI` no Render
- Adapte o `server.js` para usar o MongoDB

**Opção B — Render Disk (pago)**
- No painel do Render → seu serviço → "Disks"
- Monte em `/opt/render/project/src/`

**Opção C — Para testes (sem persistência)**
- Use assim mesmo — dados somem ao reiniciar
- Ok para testar o multiplayer com amigos

---

## 🔧 Variáveis de Ambiente no Render

No painel do serviço → **"Environment"** → adicione:

| Key | Value |
|-----|-------|
| `NODE_ENV` | `production` |
| `PORT` | (deixe vazio — Render injeta automaticamente) |

---

## 📁 Estrutura do Projeto

```
eco-arandor-online/
├── server.js          # Servidor Node.js + Socket.io
├── package.json       # Dependências
├── render.yaml        # Config automática do Render
├── .gitignore         # Ignora node_modules e database.json
└── public/
    └── index.html     # Cliente do jogo (gráficos V17)
```

---

## 🎮 Testar Localmente

```bash
npm install
npm start
# Abra http://localhost:3000
```

Para multiplayer local, abra em várias abas ou outros dispositivos na mesma rede usando o IP local: `http://192.168.x.x:3000`

---

## 🌐 Compartilhar com Amigos

Após deploy no Render, mande o link:
```
https://eco-arandor-online.onrender.com
```
Qualquer pessoa com o link pode jogar! ✅

> **Nota:** No plano gratuito do Render, o serviço "dorme" após 15 min sem acesso. O primeiro acesso pode demorar ~30s para acordar.
