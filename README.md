# claude-rules

Configuração global do [Claude Code](https://claude.com/claude-code) que uso em todos os meus projetos, mais o padrão de organização de pastas que sustenta essas regras.

## Estrutura de pastas

```
Data/                           # raiz — NAO e repositorio git
├── Cofre.md                    # fonte unica de credenciais de TODOS os projetos — nunca versionado
│
├── Projeto-A/                  # cada projeto e um repo git independente
│   ├── .git/
│   ├── .gitignore              # ignora Senhas.md, .env, Cofre.md
│   ├── Brain.md                # documentacao viva do projeto — versionado, sem segredos
│   ├── Senhas.md                # espelho local das credenciais do projeto — gitignored
│   ├── .env / .env.example
│   └── ...codigo do projeto...
│
├── Projeto-B/
│   └── (mesma estrutura acima)
│
└── Projeto-N/
    └── (mesma estrutura acima)
```

## Ideia central

- **Um cofre, muitos projetos.** Toda credencial de todo projeto mora em um único `Cofre.md`, fora de qualquer repositório git (a raiz `Data` não é versionada). Cada projeto tem seu próprio `.env`/`Senhas.md` local (que a aplicação lê), mas em caso de divergência o `Cofre.md` manda.
- **Segredo nunca entra em commit.** `.gitignore` bloqueia `Senhas.md`, `.env` e qualquer cópia de `Cofre.md` que acabe dentro de um projeto.
- **Acesso remoto sem fricção, sem eu nunca ver a senha.** Para serviços acessados com frequência (SSH, SMB, etc), a credencial sem senha (chave SSH, credencial salva do SO) é criada pelo usuário uma única vez — nunca pela IA usando a senha diretamente, mesmo que seja fornecida no chat. Depois de criada, é reaproveitada livremente nas próximas sessões.
- **`Brain.md` como memória viva do projeto.** Cada projeto mantém um `Brain.md` com o resumo completo (conexões-chave, lógica, scripts, casos de uso) — atualizado a cada commit relevante, sem nunca conter valores de segredo.

## Arquivo

- [`CLAUDE.md`](./CLAUDE.md) — a configuração global completa.
