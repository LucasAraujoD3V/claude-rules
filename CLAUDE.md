# Configuracao Global — Claude Code

## Idioma

- **Sempre** responda em portugues (Brasil), em qualquer projeto e em qualquer tipo de tarefa, independente do idioma da pergunta ou do codigo.

## Ferramentas preferidas

- **Sempre** use o Chrome MCP (`mcp__Claude_in_Chrome__*` / `mcp__claude-in-chrome__*`) para qualquer tarefa web — nunca `computer-use` para isso.
- **Verificacao visual de mudancas em apps com login:** o Chrome MCP roda no navegador real do usuario, com sessao/cache ja autenticado — nao e a mesma coisa que um preview browser limpo (ex: `mcp__Claude_Browser__*` apontando pro dev server). Quando uma tela exigir login e eu nao tiver credencial de teste, **nao desistir da verificacao**: usar o Chrome MCP (pode ja ter sessao valida em cache) ou pedir ao usuario para fazer login nessa aba uma vez. So relatar "nao consegui verificar" depois de tentar isso.
- Para operacoes de servidor/shell, use Bash via SSH quando o projeto tiver acesso remoto configurado.
- Prefira ferramentas dedicadas (Read, Edit, Glob, Grep) em vez de Bash para operacoes em arquivos locais.

## GitHub e credenciais

- Faca commit/push sempre em nome de **LucasAraujoD3V** / **luccasaraujo2003@hotmail.com**.
- Faca commit com mensagens descritivas explicando o **porque** da mudanca, nao so o que mudou.
- **Antes de commitar, sempre rode `git fetch` e confirme se a branch local esta atualizada com o `origin`** (compare o commit mais recente). Se estiver atrasada, faca `git pull`/reconcilie antes de commitar em cima. Nunca assuma que o estado local e o mais recente sem checar.
- Mantenha um arquivo `Brain.md` na raiz de cada projeto com o resumo completo: conexoes-chave, logica, scripts, casos de uso, usuarios, funcionalidades, telas. Atualize-o junto com cada commit.
- **Nunca** inclua senhas, tokens ou dados sensiveis em commits.

## Credenciais — Cofre central

- **Fonte unica de verdade de TODAS as credenciais de TODOS os projetos:** `C:\Users\lucas\OneDrive\Documentos\Data\Cofre.md`.
- Esse arquivo fica na **raiz da pasta `Data`**, acima de todos os projetos. A raiz `Data` **nao e** repositorio git, entao o `Cofre.md` esta fora de qualquer repo por construcao. `Cofre.md` tambem entra no `.gitignore` de cada projeto como segunda barreira.
- **Nunca** commitar, colar ou espelhar o conteudo do `Cofre.md` em arquivo versionado, issue, PR ou mensagem de commit. **Nunca** criar `Cofre.md` dentro de um projeto.
- Precisa de uma credencial? Leia o `Cofre.md` na raiz `Data`. Criou/rotacionou uma credencial? Atualize o `Cofre.md` **na hora**, dizendo de que projeto e, o que ela faz e onde e usada (nao so o valor).
- Os `.env` e `Senhas.md` de cada projeto continuam existindo (a aplicacao le deles) e continuam gitignorados. Em caso de divergencia, o `Cofre.md` manda.
- No `Brain.md` de cada projeto, sempre incluir uma secao `## Configuracao` dizendo que **todas as credenciais estao no `Cofre.md` na raiz da pasta `Data`, fora do versionamento e nunca postado no git**, e que `.env.example` mostra quais variaveis o projeto precisa. Nessa secao **so o ponteiro**, nenhum valor de segredo.

## Acesso remoto sem pedir senha toda hora (SSH, SMB, etc)

- Para servicos acessados com frequencia (SSH, compartilhamento SMB, etc), a credencial **sem senha** (chave SSH, credencial salva no Gerenciador de Credenciais do Windows) deve ser criada **pelo usuario, uma unica vez**, mesmo que ele forneca a senha no chat ou peca explicitamente.
- Depois de criada pelo usuario, essa credencial pode ser reaproveitada livremente em sessoes futuras (ex: `ssh -i <chave>`) sem pedir senha de novo.
- Documente no `Brain.md` do projeto **onde** essa credencial esta guardada (ex: caminho da chave SSH), nunca a senha usada para cria-la.
