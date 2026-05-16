# AI_CONTEXT.md

# CONTEXTO GERAL

Este é um projeto real em desenvolvimento contínuo.
Sempre trabalhar em cima da estrutura existente.

O objetivo principal é:
- estabilidade;
- segurança;
- persistência correta;
- compatibilidade futura;
- funcionamento real em produção.

Evitar mudanças agressivas ou desnecessárias.

---

# REGRA PRINCIPAL

NUNCA:
- recriar o projeto do zero;
- substituir arquitetura inteira sem necessidade;
- remover funcionalidades existentes;
- simplificar funcionalidades importantes;
- alterar design aprovado drasticamente;
- mover arquivos desnecessariamente;
- quebrar compatibilidade existente.

Sempre preservar a base atual do projeto.

---

# IMPLEMENTAÇÃO

Preferência por:
- mudanças pequenas;
- melhorias incrementais;
- módulos isolados;
- integração segura;
- compatibilidade com funcionalidades existentes.

Evitar:
- grandes refatorações;
- reorganizações massivas;
- alterações desnecessárias.

---

# FIREBASE / FIRESTORE

Se o projeto usar Firebase:
- manter Firestore como fonte principal;
- manter persistência correta;
- manter separação por usuário autenticado;
- nunca misturar dados entre usuários;
- não substituir Firestore por localStorage;
- não alterar autenticação sem necessidade;
- não alterar Firebase config sem necessidade.

Sempre priorizar segurança e integridade dos dados.

---

# PWA / CACHE / SERVICE WORKER

Se existir PWA:
- atualizar sempre a versão do CACHE_NAME no sw.js;
- evitar cache antigo;
- manter funcionamento offline/online;
- manter compatibilidade mobile.

Sempre revisar:
- service worker;
- manifest;
- cache;
- atualização do PWA.

---

# UX / BOTÕES

Todos os salvamentos importantes devem:
- evitar clique duplo;
- mostrar feedback visual;
- mostrar mensagens claras:
  - Salvando...
  - Salvo com sucesso
  - Erro ao salvar

Evitar ações silenciosas.

---

# MOBILE

Sempre considerar uso mobile.

Revisar:
- responsividade;
- elementos cortados;
- usabilidade;
- botões;
- formulários;
- teclado mobile.

Mudanças visuais devem ser discretas e compatíveis com o design atual.

---

# TESTES OBRIGATÓRIOS

Antes de finalizar:
- revisar console;
- revisar persistência;
- revisar reload da página;
- revisar aba anônima;
- revisar login persistente;
- revisar mobile;
- revisar offline/online;
- revisar possíveis erros silenciosos;
- revisar salvamento;
- revisar integração entre módulos.

---

# GIT / VERSIONAMENTO

Preservar compatibilidade com:
- Git;
- GitHub;
- GitHub Desktop;
- VS Code;
- Codex;
- deploy existente.

Nunca apagar:
- .git
- arquivos essenciais do projeto

---

# SEGURANÇA

Evitar:
- perda de dados;
- duplicações;
- loops de salvamento;
- caminhos inseguros;
- sobrescritas incorretas;
- conflitos de autenticação;
- exposição de dados sensíveis.

Prioridade máxima:
- estabilidade;
- persistência;
- segurança;
- compatibilidade futura.

---

# ESTILO DE TRABALHO

Sempre:
- explicar alterações importantes;
- trabalhar em cima da base existente;
- preservar compatibilidade;
- corrigir sem quebrar o restante;
- manter arquitetura consistente.

Evitar:
- mudanças excessivas;
- comportamento imprevisível;
- alterações fora do escopo solicitado.

---

# PRIORIDADE DO PROJETO

Mais importante:
- funcionamento real;
- estabilidade;
- persistência;
- segurança;
- compatibilidade.

Menos importante:
- animações;
- efeitos visuais;
- refatorações estéticas;
- mudanças cosméticas desnecessárias.
