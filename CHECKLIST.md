# 🎬 Short Video Assistant — Checklist de Desenvolvimento

Checklist geral para acompanhamento do desenvolvimento do **Short Video Assistant**.

---

# 📋 1. Planejamento e Arquitetura

* [ ] Definir arquitetura geral do sistema
* [ ] Definir tecnologias utilizadas
* [ ] Definir estrutura de pastas
* [ ] Definir fluxo de dados
* [ ] Definir modelo de usuários
* [ ] Definir modelo de vídeos
* [ ] Definir modelo de processamento
* [ ] Definir modelo de versões
* [ ] Definir modelo de agendamentos
* [ ] Definir estados do vídeo
* [ ] Definir estratégia de armazenamento
* [ ] Definir sistema de filas
* [ ] Definir estratégia de notificações

---

# 🎨 2. Frontend

## Upload

* [ ] Criar tela de upload
* [ ] Seleção de arquivo
* [ ] Drag & Drop
* [ ] Validação de formato
* [ ] Validação de tamanho
* [ ] Exibir informações do arquivo
* [ ] Iniciar upload
* [ ] Exibir progresso do upload
* [ ] Tratar erros de upload

## Preview do vídeo original

* [ ] Exibir player de vídeo
* [ ] Controles de reprodução
* [ ] Exibir duração
* [ ] Exibir resolução
* [ ] Exibir tamanho do arquivo
* [ ] Permitir substituir o vídeo
* [ ] Botão "Confirmar vídeo"

## Processamento

* [ ] Tela de processamento
* [ ] Exibir status atual
* [ ] Exibir progresso
* [ ] Informar que o processamento ocorre no backend
* [ ] Atualizar status em tempo real
* [ ] Tratar erro de processamento

## Revisão

* [ ] Notificar quando o vídeo estiver pronto
* [ ] Exibir vídeo processado
* [ ] Comparação original × processado
* [ ] Botão "Aprovar"
* [ ] Botão "Solicitar alterações"
* [ ] Campo para descrever alterações
* [ ] Enviar solicitação de alteração
* [ ] Exibir histórico de versões

---

# 🔌 3. Backend / API

## Estrutura

* [ ] Criar servidor
* [ ] Configurar API
* [ ] Configurar variáveis de ambiente
* [ ] Configurar CORS
* [ ] Configurar tratamento global de erros
* [ ] Configurar logs

## Usuários

* [ ] Criar autenticação
* [ ] Login
* [ ] Cadastro
* [ ] Logout
* [ ] Recuperação de acesso
* [ ] Controle de permissões

## Vídeos

* [ ] Endpoint para upload
* [ ] Criar registro do vídeo
* [ ] Gerar ID do vídeo
* [ ] Associar vídeo ao usuário
* [ ] Consultar vídeo
* [ ] Listar vídeos
* [ ] Excluir vídeo
* [ ] Consultar status

## Processamento

* [ ] Endpoint para confirmar vídeo
* [ ] Criar tarefa de processamento
* [ ] Enviar tarefa para fila
* [ ] Consultar progresso
* [ ] Atualizar status
* [ ] Registrar erros
* [ ] Endpoint para solicitar alterações
* [ ] Endpoint para aprovar vídeo

---

# ⚙️ 4. Worker de Processamento

O Worker será responsável pelas tarefas pesadas de processamento.

* [ ] Criar Worker
* [ ] Conectar Worker à fila
* [ ] Receber tarefas
* [ ] Validar tarefa
* [ ] Baixar/acessar vídeo original
* [ ] Analisar vídeo
* [ ] Detectar trechos relevantes
* [ ] Realizar cortes
* [ ] Redimensionar vídeo
* [ ] Alterar proporção
* [ ] Adicionar legendas
* [ ] Adicionar elementos gráficos
* [ ] Aplicar outras modificações
* [ ] Processar com FFmpeg
* [ ] Integrar IA, se necessário
* [ ] Gerar vídeo final
* [ ] Salvar resultado
* [ ] Atualizar progresso
* [ ] Atualizar status
* [ ] Registrar logs
* [ ] Tratar falhas
* [ ] Implementar retry
* [ ] Limpar arquivos temporários

---

# 📨 5. Sistema de Filas

* [ ] Escolher tecnologia de fila
* [ ] Configurar fila
* [ ] Criar jobs
* [ ] Definir payload dos jobs
* [ ] Worker consumir jobs
* [ ] Controle de jobs duplicados
* [ ] Retry automático
* [ ] Limite de tentativas
* [ ] Timeout de processamento
* [ ] Controle de prioridade
* [ ] Monitoramento da fila

---

# 🗄️ 6. Banco de Dados

## Usuários

* [ ] Criar estrutura de usuários
* [ ] ID
* [ ] Nome
* [ ] E-mail
* [ ] Senha/autenticação
* [ ] Data de criação

## Vídeos

* [ ] Criar estrutura de vídeos
* [ ] ID
* [ ] Usuário
* [ ] Nome
* [ ] Status
* [ ] URL original
* [ ] Versão atual
* [ ] Duração
* [ ] Resolução
* [ ] Tamanho
* [ ] Data de criação
* [ ] Data de atualização

## Processamentos

* [ ] Criar estrutura de processamentos
* [ ] ID
* [ ] ID do vídeo
* [ ] Versão
* [ ] Status
* [ ] Progresso
* [ ] Erro
* [ ] Data de início
* [ ] Data de conclusão

## Versões

* [ ] Criar estrutura de versões
* [ ] ID
* [ ] ID do vídeo
* [ ] Número da versão
* [ ] URL do arquivo
* [ ] Alterações realizadas
* [ ] Data de criação

## Solicitações de alteração

* [ ] Criar estrutura
* [ ] ID
* [ ] ID do vídeo
* [ ] Versão
* [ ] Descrição
* [ ] Status
* [ ] Data da solicitação

---

# 📦 7. Storage

* [ ] Escolher serviço de armazenamento
* [ ] Configurar Storage
* [ ] Upload do vídeo original
* [ ] Armazenar vídeos processados
* [ ] Separar arquivos por usuário
* [ ] Separar arquivos por vídeo
* [ ] Não sobrescrever o original
* [ ] Manter versões anteriores
* [ ] Gerar URLs seguras
* [ ] Controlar acesso aos arquivos
* [ ] Limpar arquivos temporários
* [ ] Definir política de retenção

### Estrutura sugerida

```text
/videos/
└── {user_id}/
    └── {video_id}/
        ├── original.mp4
        ├── processed-v1.mp4
        ├── processed-v2.mp4
        └── processed-v3.mp4
```

---

# 🔄 8. Estados do Vídeo

Fluxo principal:

```text
UPLOADED
    ↓
WAITING_CONFIRMATION
    ↓
WAITING_ANALYSIS
    ↓
PROCESSING
    ↓
READY_FOR_REVIEW
    ↓
APPROVED
```

Caso sejam solicitadas alterações:

```text
READY_FOR_REVIEW
    ↓
CHANGES_REQUESTED
    ↓
PROCESSING
    ↓
READY_FOR_REVIEW
```

Após aprovação:

```text
APPROVED
    ↓
READY_TO_PUBLISH
    ↓
SCHEDULED
    ↓
PUBLISHED
```

---

# 🔔 9. Notificações

## Web Push

* [ ] Configurar Web Push
* [ ] Solicitar permissão ao usuário
* [ ] Registrar subscription
* [ ] Armazenar subscription
* [ ] Criar serviço de notificações
* [ ] Enviar notificação de processamento iniciado
* [ ] Enviar notificação de processamento concluído
* [ ] Enviar notificação de erro
* [ ] Enviar notificação de vídeo pronto para revisão
* [ ] Enviar notificação de alterações solicitadas
* [ ] Enviar notificação de aprovação
* [ ] Enviar notificação de publicação

## Atualização em tempo real

* [ ] Definir WebSocket ou SSE
* [ ] Atualizar status no frontend
* [ ] Atualizar progresso
* [ ] Reconectar automaticamente
* [ ] Sincronizar status ao retornar à página

---

# ✂️ 10. Processamento de Vídeo

* [ ] Instalar/configurar FFmpeg
* [ ] Conversão de formatos
* [ ] Corte de vídeo
* [ ] Redimensionamento
* [ ] Alteração de proporção
* [ ] Conversão para formato vertical
* [ ] Controle de qualidade
* [ ] Controle de bitrate
* [ ] Controle de FPS
* [ ] Extração de áudio
* [ ] Processamento de áudio
* [ ] Inserção de legendas
* [ ] Inserção de textos
* [ ] Inserção de elementos visuais
* [ ] Geração da versão final

---

# 🤖 11. Análise / IA

* [ ] Definir funcionalidades de IA
* [ ] Análise automática do vídeo
* [ ] Identificação de trechos relevantes
* [ ] Detecção de pausas
* [ ] Detecção de cortes
* [ ] Transcrição de áudio
* [ ] Geração de legendas
* [ ] Identificação de momentos importantes
* [ ] Sugestão de cortes
* [ ] Definir integração com modelo de IA
* [ ] Processar resultado da IA
* [ ] Enviar instruções para o Worker

---

# 📱 12. Organização dos Vídeos

* [ ] Dashboard
* [ ] Listagem de vídeos
* [ ] Filtros
* [ ] Pesquisa
* [ ] Ordenação
* [ ] Status do vídeo
* [ ] Visualização por projeto
* [ ] Histórico de processamento
* [ ] Histórico de versões
* [ ] Exclusão de vídeos
* [ ] Organização por categorias/tags

---

# 📅 13. Agendamento

* [ ] Criar sistema de agendamento
* [ ] Selecionar data
* [ ] Selecionar horário
* [ ] Definir plataforma
* [ ] Criar publicação
* [ ] Listar agendamentos
* [ ] Editar agendamento
* [ ] Cancelar agendamento
* [ ] Status do agendamento
* [ ] Notificar usuário próximo à publicação

---

# 📲 14. Plataformas

## Instagram / Reels

* [ ] Estudar integração
* [ ] Autenticação
* [ ] Configurar API
* [ ] Preparar publicação
* [ ] Publicação
* [ ] Verificar retorno da API

## TikTok

* [ ] Estudar integração
* [ ] Autenticação
* [ ] Configurar API
* [ ] Preparar publicação
* [ ] Publicação
* [ ] Verificar retorno da API

## YouTube / Shorts

* [ ] Estudar integração
* [ ] Autenticação
* [ ] Configurar API
* [ ] Upload
* [ ] Configurar título
* [ ] Configurar descrição
* [ ] Configurar publicação

---

# 🧪 15. Testes

## Upload

* [ ] Arquivo válido
* [ ] Arquivo inválido
* [ ] Arquivo muito grande
* [ ] Formato não suportado
* [ ] Upload interrompido
* [ ] Upload duplicado

## Processamento

* [ ] Processamento normal
* [ ] Processamento demorado
* [ ] Falha no FFmpeg
* [ ] Falha na IA
* [ ] Worker desligado
* [ ] Retry
* [ ] Jobs simultâneos
* [ ] Job duplicado

## Revisão

* [ ] Vídeo processado disponível
* [ ] Preview funcionando
* [ ] Aprovação
* [ ] Solicitação de alteração
* [ ] Nova versão
* [ ] Histórico de versões

## Notificações

* [ ] Permissão Web Push
* [ ] Notificação recebida
* [ ] Notificação com navegador fechado
* [ ] Clique na notificação
* [ ] Redirecionamento correto

---

# 🔐 16. Segurança

* [ ] Autenticação
* [ ] Autorização
* [ ] Validação de arquivos
* [ ] Limite de tamanho
* [ ] Validação MIME type
* [ ] Sanitização de dados
* [ ] Proteção dos endpoints
* [ ] URLs privadas para vídeos
* [ ] Controle de acesso ao Storage
* [ ] Rate limiting
* [ ] Proteção contra uploads maliciosos
* [ ] Variáveis sensíveis em `.env`
* [ ] Nunca armazenar secrets no Git

---

# 🚀 17. Infraestrutura

* [ ] Configurar ambiente de desenvolvimento
* [ ] Configurar ambiente de produção
* [ ] Frontend
* [ ] Backend
* [ ] Worker
* [ ] Banco de dados
* [ ] Storage
* [ ] Queue
* [ ] FFmpeg
* [ ] Web Push
* [ ] Domínio
* [ ] HTTPS
* [ ] Variáveis de ambiente
* [ ] Logs
* [ ] Monitoramento
* [ ] Backup
* [ ] Deploy
* [ ] Escalonamento dos Workers

---

# 📊 18. Monitoramento

* [ ] Logs do backend
* [ ] Logs do Worker
* [ ] Logs de processamento
* [ ] Monitorar fila
* [ ] Monitorar CPU
* [ ] Monitorar RAM
* [ ] Monitorar armazenamento
* [ ] Monitorar tempo de processamento
* [ ] Monitorar erros
* [ ] Alertas de falha
* [ ] Dashboard de métricas

---

# 🧹 19. Otimização

* [ ] Otimizar upload
* [ ] Upload multipart/chunked, se necessário
* [ ] Compressão
* [ ] Processamento assíncrono
* [ ] Otimizar FFmpeg
* [ ] Limitar recursos por Worker
* [ ] Paralelizar processamento quando possível
* [ ] Cache
* [ ] Limpeza automática
* [ ] Otimizar consultas ao banco
* [ ] Otimizar consumo de Storage

---

# 📌 20. Ordem de Implementação

### Fase 1 — Fundação

* [ ] Estrutura do projeto
* [ ] Banco de dados
* [ ] Storage
* [ ] Backend
* [ ] Frontend
* [ ] Autenticação

### Fase 2 — Upload

* [ ] Upload
* [ ] Validação
* [ ] Storage
* [ ] Preview
* [ ] Confirmação

### Fase 3 — Processamento

* [ ] Queue
* [ ] Worker
* [ ] FFmpeg
* [ ] Processamento
* [ ] Salvamento do resultado

### Fase 4 — Acompanhamento

* [ ] Status
* [ ] Progresso
* [ ] WebSocket/SSE
* [ ] Web Push
* [ ] Tratamento de erros

### Fase 5 — Revisão

* [ ] Preview processado
* [ ] Aprovação
* [ ] Solicitação de alterações
* [ ] Versionamento
* [ ] Reprocessamento

### Fase 6 — Organização

* [ ] Dashboard
* [ ] Filtros
* [ ] Pesquisa
* [ ] Categorias
* [ ] Histórico

### Fase 7 — Publicação

* [ ] Agendamento
* [ ] Integração com plataformas
* [ ] Publicação
* [ ] Notificações

### Fase 8 — Produção

* [ ] Testes
* [ ] Segurança
* [ ] Logs
* [ ] Monitoramento
* [ ] Backup
* [ ] Deploy
* [ ] Otimização

---

# 🎯 Fluxo Final do Sistema

```text
                    ┌──────────────┐
                    │    USUÁRIO   │
                    └──────┬───────┘
                           │
                           ▼
                    ┌──────────────┐
                    │    UPLOAD    │
                    └──────┬───────┘
                           │
                           ▼
                    ┌──────────────┐
                    │    PREVIEW   │
                    │    ORIGINAL  │
                    └──────┬───────┘
                           │
                      CONFIRMAR
                           │
                           ▼
                    ┌──────────────┐
                    │   BACKEND    │
                    └──────┬───────┘
                           │
                           ▼
                    ┌──────────────┐
                    │     FILA     │
                    └──────┬───────┘
                           │
                           ▼
                    ┌──────────────┐
                    │    WORKER    │
                    │              │
                    │   Análise    │
                    │    IA        │
                    │   FFmpeg     │
                    │ Processamento│
                    └──────┬───────┘
                           │
                           ▼
                    ┌──────────────┐
                    │    STORAGE   │
                    └──────┬───────┘
                           │
                           ▼
                 ┌────────────────────┐
                 │  PRONTO PARA       │
                 │     REVISÃO        │
                 └─────────┬──────────┘
                           │
                           ▼
                    ┌──────────────┐
                    │    PREVIEW   │
                    │   PROCESSADO │
                    └──────┬───────┘
                           │
                  ┌────────┴────────┐
                  │                 │
                  ▼                 ▼
              APROVAR          ALTERAR
                  │                 │
                  │                 ▼
                  │             ┌───────┐
                  │             │  FILA │
                  │             └───┬───┘
                  │                 │
                  │                 ▼
                  │              WORKER
                  │                 │
                  │                 ▼
                  │           NOVA VERSÃO
                  │                 │
                  │                 └──────► REVISÃO
                  │
                  ▼
             APROVADO
                  │
                  ▼
          PRONTO PARA PUBLICAR
                  │
                  ▼
             AGENDAMENTO
                  │
                  ▼
              PUBLICAÇÃO
                  │
                  ▼
              NOTIFICAÇÃO
```

---

# 🏁 Objetivo da V1

A primeira versão funcional deverá permitir:

* [ ] Usuário fazer login
* [ ] Usuário enviar um vídeo
* [ ] Usuário visualizar o vídeo original
* [ ] Usuário confirmar o vídeo
* [ ] Backend criar processamento
* [ ] Worker processar o vídeo
* [ ] Resultado ser salvo no Storage
* [ ] Usuário receber notificação
* [ ] Usuário visualizar o vídeo processado
* [ ] Usuário aprovar ou solicitar alteração
* [ ] Sistema gerar novas versões
* [ ] Usuário finalizar o vídeo

> **Importante:** o processamento pesado deve permanecer fora da requisição HTTP principal. O Backend gerencia as tarefas e o Worker executa o processamento, permitindo que o sistema continue responsivo mesmo com vídeos grandes ou processamentos demorados.
