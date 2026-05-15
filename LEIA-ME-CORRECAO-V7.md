# Correcção v7 — Aprovações pendentes

Esta versão corrige o caso em que o Dashboard mostra lançamentos SUBMETIDO, mas a página Aprovações mostra "Sem lançamentos pendentes de aprovação".

Ficheiros alterados:

- apps_script/Approvals.gs
- apps_script/Server_call.gs
- app.js

O que foi corrigido:

1. `Approval_listPending()` passa a reparar automaticamente o fluxo antes de listar pendências.
2. Lançamentos com estado `SUBMETIDO` sem registo correspondente em `APROVACOES` passam a receber aprovação pendente automaticamente.
3. Registos antigos em `APROVACOES` com `perfil_responsavel` vazio, antigo ou errado são normalizados para `TESOUREIRO_DISTRITAL`.
4. Registos com `decisao` vazia passam a ser tratados como `PENDENTE`.
5. Foi adicionada a chamada `Approval_repararPendencias` no dispatcher `Server_call.gs`.
6. `app.js` deixa de cachear `Approval_listPending`, para não esconder reparações recentes.

Aplicação mínima:

- No Apps Script: substituir `Approvals.gs` e `Server_call.gs`.
- No Vercel/GitHub: substituir `app.js`.

Depois de substituir no Apps Script, publicar nova versão do Web App:
Deploy > Manage deployments > Edit > Version > New version > Deploy.
