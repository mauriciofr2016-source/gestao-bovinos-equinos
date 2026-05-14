# 🌿 Fazenda Manager — Setup Completo

## O que é esse app

PWA (Progressive Web App) para gestão completa de animais de fazenda.
Funciona como app instalado no celular, sincroniza com Firebase para acesso em qualquer aparelho.

---

## PASSO 1 — Criar projeto no Firebase

1. Acesse https://console.firebase.google.com
2. Clique em **"Criar projeto"**
3. Nome: `fazenda-manager` (ou o que preferir)
4. Desative Google Analytics (não precisa)
5. Clique em **Criar projeto**

---

## PASSO 2 — Ativar Firestore

1. No menu lateral, clique em **Firestore Database**
2. Clique em **Criar banco de dados**
3. Escolha **Modo de produção** → Avançar
4. Escolha a região (ex: `southamerica-east1` para Brasil) → Concluir

### Regras do Firestore (acesso livre — só você usa):

No Firestore → aba **Regras**, substitua por:
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```
Clique em **Publicar**.

---

## PASSO 3 — Obter as credenciais

1. No painel do Firebase, clique na engrenagem ⚙️ → **Configurações do projeto**
2. Em **Seus apps**, clique em `</>` (Web)
3. Nome do app: `fazenda` → **Registrar app**
4. Copie o objeto `firebaseConfig` que aparecer

---

## PASSO 4 — Colar as credenciais no app

Abra o arquivo `index.html` e localize esta parte (por volta da linha 560):

```javascript
const firebaseConfig = {
  apiKey: "COLOQUE_SUA_API_KEY",
  authDomain: "COLOQUE_SEU_AUTH_DOMAIN",
  projectId: "COLOQUE_SEU_PROJECT_ID",
  ...
};
```

Substitua pelos valores reais que você copiou do Firebase.

---

## PASSO 5 — Publicar no GitHub Pages

1. Crie um repositório no GitHub (ex: `fazenda-app`)
2. Envie todos os arquivos desta pasta para o repositório
3. Vá em **Settings → Pages**
4. Em **Source**, selecione `main` branch → `/root`
5. Clique em **Save**
6. Aguarde 1-2 minutos e acesse o link gerado (ex: `https://seuusuario.github.io/fazenda-app`)

---

## PASSO 6 — Instalar no celular como app

### Android (Chrome):
1. Abra o link no Chrome
2. Toque nos 3 pontinhos ⋮ → **"Adicionar à tela inicial"**
3. Confirme — o app aparecerá com ícone na tela inicial

### iOS (Safari):
1. Abra o link no Safari
2. Toque em **Compartilhar** → **"Adicionar à tela de início"**
3. Confirme

---

## PASSO 7 (Opcional) — Gerar ícones

Acesse https://www.pwabuilder.com ou https://favicon.io
Gere ícones 192x192 e 512x512 e coloque na pasta `icons/`

---

## Funcionalidades do app

### Animais
- Cadastro com: nome, espécie, raça, sexo, data entrada, valor compra, peso, observações
- Ficha individual: histórico completo de trato, saúde, prenhez e custos
- Botão Vender: calcula lucro/prejuízo, arquiva em "Vendidos" com ficha completa
- Exclusão com confirmação em qualquer área

### Trato / Alimentação
- Selecionar animal + múltiplos insumos na mesma sessão
- Cálculo automático do custo por kg (baseado no preço da compra do estoque)
- Debita automaticamente do estoque
- Lança automaticamente no financeiro
- Histórico completo com exclusão

### Saúde / Veterinário
- Registro de vacinas, medicamentos, exames, procedimentos
- Programação de próxima dose com alerta automático
- Badge de alertas no menu quando há doses vencidas
- Histórico completo por animal

### Calendário Inteligente
- Calendário visual com marcadores de eventos
- Prenhez: calcula previsão de parto automaticamente
  - Vacas/bois: 283 dias de gestação
  - Éguas: 340 dias de gestação
- Barra de progresso da gestação
- Eventos de saúde (próximas doses) aparecem no calendário
- Ao vender animal: prenhez arquivada automaticamente
- Ver eventos por dia (toque no dia marcado)

### Estoque
- Cadastro de insumos (ração, silagem, feno, sal, suplemento)
- Cálculo automático do custo por kg
- Saldo atualizado automaticamente pelo trato
- Alerta visual de estoque baixo
- Valor total em estoque

### Financeiro
- Lançamento automático de: compra de animal, trato, vacinas/saúde, venda
- Receita automática ao registrar venda
- Resumo por animal (custo vs receita)
- Lucro líquido e margem calculados
- Exclusão de lançamentos com confirmação

---

## Sincronização

Todos os dados são salvos no Firestore em tempo real.
Funciona em qualquer aparelho que acessar o mesmo link com as mesmas configurações do Firebase.
Funciona offline — sincroniza quando voltar a internet.

---

## Estrutura dos arquivos

```
fazenda-app/
├── index.html          ← App completo (HTML + CSS + JS)
├── sw.js               ← Service Worker (PWA offline)
├── manifest.json       ← Configuração do PWA
├── firebase-config.js  ← Referência (credenciais vão no index.html)
├── icons/
│   ├── icon-192.png    ← Ícone do app (gerar separadamente)
│   └── icon-512.png    ← Ícone splash (gerar separadamente)
└── README.md           ← Este arquivo
```


---

## Atualização de segurança aplicada

Esta versão foi ajustada para uso com Firebase Authentication.
O banco agora deve ser usado em caminho isolado por usuário:

```text
users/{uid}/animais
users/{uid}/tratos
users/{uid}/saude
users/{uid}/prenhez
users/{uid}/estoque
users/{uid}/financeiro
```

### Regras recomendadas do Firestore

Use estas regras no Firebase Console em Firestore Database > Rules:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

Não use `allow read, write: if true;` em produção.

### Login

Crie um usuário em Firebase Authentication > Users.
Depois entre no aplicativo usando o e-mail e senha criados.

### PWA/cache

O cache foi atualizado para `gestao-fazenda-v2.0`.
Em próximas atualizações importantes, altere esse nome no `sw.js` para forçar o celular a baixar a versão nova.
