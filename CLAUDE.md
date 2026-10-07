# Configuracao Global — Claude Code

## Idioma

- **Sempre** responda em portugues (Brasil), em qualquer projeto e em qualquer tipo de tarefa, independente do idioma da pergunta ou do codigo.

## Execução de múltiplas tarefas

- Quando eu mandar várias tarefas numa mensagem (ou numa sequência), **continue automaticamente pra próxima assim que a anterior terminar** — não pare pra pedir confirmação entre elas. Só interrompa se travar em algo que só eu posso decidir (credencial, ambiguidade real, ação destrutiva/irreversível).

## Ferramentas preferidas

- **Sempre** use o Chrome MCP (`mcp__Claude_in_Chrome__*` / `mcp__claude-in-chrome__*`) para qualquer tarefa web — nunca `computer-use` para isso.
- **Verificacao visual de mudancas em apps com login:** o Chrome MCP roda no navegador real do usuario, com sessao/cache ja autenticado — nao e a mesma coisa que um preview browser limpo (ex: `mcp__Claude_Browser__*` apontando pro dev server). Quando uma tela exigir login e eu nao tiver credencial de teste, **nao desistir da verificacao**: usar o Chrome MCP (pode ja ter sessao valida em cache) ou pedir ao usuario para fazer login nessa aba uma vez. So relatar "nao consegui verificar" depois de tentar isso.
- **Abrir o app sozinho aqui no Claude:** trabalhando em projeto com app/frontend, **abrir o app automaticamente no navegador do proprio Claude** (Browser pane, `preview_start` com o `.claude/launch.json` do projeto) assim que a tarefa envolver tela — sem esperar eu pedir — pra eu acompanhar junto. Login: **voce nunca digita senha**; a sessao e a que eu deixo logada no navegador do Claude, e ela **nao e permanente nem automatica** — vale so pro endereco em que eu loguei (localhost, teste e producao sao sessoes separadas), so nesta maquina, e expira conforme o sistema (no Kairos-2.0, 5 horas depois do login). **Antes de dizer que tem acesso, abrir a tela e conferir**; se cair no login, me pedir pra logar de novo nessa aba em vez de desistir da verificacao — e, enquanto isso, verificar o que der sem login (pagina de teste com dados ficticios, consulta somente leitura). Entrada sem senha no dev so existe se eu tiver montado isso no projeto; nunca criar atalho que tire a senha do site de producao.
- Para operacoes de servidor/shell, use Bash via SSH quando o projeto tiver acesso remoto configurado.
- Prefira ferramentas dedicadas (Read, Edit, Glob, Grep) em vez de Bash para operacoes em arquivos locais.

## GitHub e credenciais

- Faca commit/push sempre em nome de **LucasAraujoD3V** / **luccasaraujo2003@hotmail.com**.
- Faca commit com mensagens descritivas explicando o **porque** da mudanca, nao so o que mudou.
- **Ao terminar uma tarefa com mudancas prontas, commite e de push automaticamente, sem parar pra perguntar antes.** So pare pra perguntar se as mudancas pendentes misturarem seu trabalho com outro trabalho em andamento que nao e seu (ai commite so os arquivos que voce de fato alterou, nao use `git add -A`/`git add .` as cegas).
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

- Para servicos acessados com frequencia (SSH, compartilhamento SMB, etc), a credencial **sem senha** (chave SSH, credencial salva no Gerenciador de Credenciais do Windows) deve ser criada **pelo usuario, uma unica vez**, mesmo que ele forneca a senha no chat ou peca explicitamente. A senha para *criar* essa credencial nunca e digitada por mim — isso vale sempre, sem excecao, independente do que este arquivo diga em qualquer outra secao.
- Depois de criada pelo usuario, essa credencial pode ser reaproveitada livremente em sessoes futuras (ex: `ssh -i <chave>`) sem pedir senha de novo.
- Documente no `Brain.md` do projeto **onde** essa credencial esta guardada (ex: caminho da chave SSH), nunca a senha usada para cria-la.

### Metodo padrao para gerar chaves SSH (usar sempre este, sem variar)

- Comando padrao: `ssh-keygen -t ed25519 -f <caminho> -N "" -C "<descricao do proposito>"` — ed25519, sem passphrase, nome de arquivo descritivo do uso (ex: `kairos2_actions_deploy`). Nao usar RSA, nao usar outras variacoes.
- Exemplos ja usados nesse padrao: `bike_estoque_deploy`, `bike_estoque_web_deploy`, `kairos_vps_deploy`, `kairos2_actions_deploy`.
- Documentar sempre no `Cofre.md` depois de criada (caminho local, onde a publica foi instalada, pra que serve).

<!-- orquestrador:inicio (gerado por Data/orquestrador/instalar.js — editar la, nao aqui) -->
## Autonomia e perguntas

- Pergunte **somente** se: (a) a acao e irreversivel/destrutiva, custa dinheiro ou sai pra fora (push forcado, apagar dados, e-mail, deploy em producao, compra); (b) precisa de credencial/acesso que nao tenho e nao esta no `Cofre.md`; (c) duas leituras razoaveis levam a trabalho materialmente diferente **e** nao da pra resolver olhando codigo, docs, memoria ou historico.
- Fora disso: decida, registre em "Decisoes assumidas" (o que, por que, alternativa descartada) e siga.
- Perguntas sao agrupadas num bloco so (no fim, ou no meio se travou), cada uma com contexto em 1 linha, opcoes e a sua recomendacao — pra eu poder responder "faz a tua". Nunca uma por vez.
- "Pronto" so com evidencia (comando → resultado). "Deve funcionar" nao e pronto.
- Falhou 3x na mesma abordagem: troque de caminho e diga por que. 3 abordagens distintas falharam: vira pergunta, com o log do que foi tentado.

## Orquestracao de objetivos grandes

- Objetivo grande ou com varias partes independentes: use a skill `orquestrador` (`/orquestrador <objetivo>`, ou automaticamente quando a descricao bater). Ela transforma a sessao em lead de um time (Agent Teams) com os agentes `executor`, `pesquisador` e `verificador`, exige evidencia real pra fechar cada tarefa (`TaskUpdate(metadata: { verificado: "<comando> → <resultado>" })` antes de `completed`; hooks `TaskCompleted`/`TeammateIdle` barram sem isso) e so o lead commita. Fonte e instalador: `Data/orquestrador` (`node instalar.js`).
<!-- orquestrador:fim -->
