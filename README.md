# 🎬 Short Video Assistant

## 🎯 Objetivo do Projeto

O **Short Video Assistant** tem como objetivo simplificar e otimizar a rotina de criadores de conteúdo que trabalham com formatos de vídeo curto, como **Reels, TikTok e Shorts**.

A proposta do sistema é oferecer uma solução intuitiva para **upload, análise, corte, processamento, organização, revisão e preparação de vídeos**, utilizando processamento no backend para executar tarefas que exigem mais recursos.

O fluxo principal será:

```text
Upload
   ↓
Preview do vídeo original
   ↓
Confirmação
   ↓
Análise / Processamento
   ↓
Vídeo pronto para revisão
   ↓
Preview do resultado
   ↓
Aprovação ou solicitação de alterações
   ↓
Versão final
```

O sistema também contará com **Web Push Notifications** para informar o usuário quando uma etapa do processamento for concluída e quando o conteúdo estiver pronto para revisão ou publicação.

---

## 📌 Acompanhe o Progresso

Para visualizar todas as etapas de desenvolvimento, tarefas pendentes e o roteiro completo de implementação:

👉 **[Consulte o Checklist de Desenvolvimento](./CHECKLIST.md)**

---

## 🏗️ Arquitetura

O processamento pesado dos vídeos será realizado no **backend/worker**, evitando sobrecarregar o navegador do usuário.

```text
┌──────────────┐
│   Frontend   │
│              │
│ Upload       │
│ Preview      │
│ Revisão      │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│   Backend    │
│     API      │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│     Fila     │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│    Worker    │
│              │
│ FFmpeg       │
│ Análise      │
│ Processamento│
└──────┬───────┘
       │
       ▼
┌──────────────┐
│    Storage   │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│   Revisão    │
└──────────────┘
```

---

## 🚧 Status do Projeto

**Em desenvolvimento 🚀**

O projeto está sendo desenvolvido de forma incremental, começando pela estrutura principal, upload e gerenciamento dos vídeos, seguido pelo sistema de processamento e revisão.

---

## 👨‍💻 Autor

Desenvolvido por **Bruno Marques**.

* 🌐 **Website / Portfólio:** [bruno-marques.vercel.app](https://bruno-marques.vercel.app/)
* 💼 **LinkedIn:** [Bruno Marques](https://www.linkedin.com/in/bruno-marques-desenvolvedor/)

---

## 📄 Licença

Este projeto está sob a licença **MIT**.