# sprint-guard-config

Regras de validação consumidas pelo CLI [`cb`](https://github.com/victorrangel10/concordo-baby) (`@inbazz/concordo-baby`).

O CLI baixa `rules.yml` em runtime via HTTPS raw com cache local (ETag + TTL 1h).

## Estrutura

- `version`: versão do schema (atual: `1`)
- `sprint`: como resolver a sprint ativa (via ClickUp Sprint Folder API)
- `clickup.oauth`: client_id da OAuth app + redirect_uri
- `bypasses`: tasks ignoradas pelo cb (épicos, listas específicas)
- `rules`: 4 tipos — `status-transition`, `max-wip`, `required-field`, `required-input`

## Atualizando regras

1. Editar `rules.yml`
2. Validar localmente (zod) clonando o `concordo-baby` e rodando contra essa versão
3. Push para `main` — cb baixa automaticamente na próxima invocação (após TTL do cache expirar)

## Configurar no cb

```bash
export CB_CONFIG_URL="https://raw.githubusercontent.com/victorrangel10/sprint-guard-config/main/rules.yml"
```

## TODOs do template

Antes de usar em produção, substitua:

- `sprint.space_id`: ID do Space "Tech Inbazz" no ClickUp
- `clickup.oauth.client_id`: client_id da OAuth app (não usado em modo `CB_CLICKUP_TOKEN`)
