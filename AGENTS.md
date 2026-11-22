# Agente de desenvolvimento orientado por especificação — Devin CLI

## Propósito

Conduza atividades de desenvolvimento em projetos novos ou existentes por quatro etapas: **especificar → planejar → implementar → avaliar**. Use os artefatos produzidos em uma etapa como entrada da próxima. Registre decisões, evidências e pendências em arquivos do projeto, para que outra sessão consiga retomar o trabalho sem depender da conversa.

Este arquivo contém as instruções operacionais do agente. Ao adaptar o processo, altere primeiro a tabela **Catálogo de skills**; as etapas abaixo referenciam os nomes da tabela.

## Catálogo de skills

| Etapa | Skill | Documentação | Instalação, se ausente |
| --- | --- | --- | --- |
| 1. Especificação | `tlc-spec-lean` | https://agent-skills.techleads.club/skills/tlc-spec-lean/ | `npx @tech-leads-club/agent-skills install --skill tlc-spec-lean` |
| 2. Plano | `tlc-plan` | https://agent-skills.techleads.club/skills/tlc-plan/ | `npx @tech-leads-club/agent-skills install --skill tlc-plan` |
| 3. Implementação | `tlc-implement` | https://agent-skills.techleads.club/skills/tlc-implement/ | `npx @tech-leads-club/agent-skills install --skill tlc-implement` |
| 4. Avaliação | `spec-driven-eval` | https://agent-skills.techleads.club/skills/spec-driven-eval/ | `npx @tech-leads-club/agent-skills install --skill spec-driven-eval` |

Antes de cada etapa, verifique se a skill está disponível no ambiente do Devin CLI. Se não estiver, execute o comando correspondente da tabela, leia o `SKILL.md` instalado e confira o resultado. Se a instalação falhar, informe o erro e interrompa a etapa dependente; não simule a execução da skill. Respeite os validadores e formatos exigidos pela versão instalada. Nunca substitua uma aprovação humana exigida pela skill por uma aprovação presumida.

## Entrada obrigatória e descoberta dos projetos

1. Registre a solicitação original, o identificador do ticket do iuclick (quando houver), o objetivo, o comportamento esperado, as restrições e os critérios de aceite informados. Preserve o texto original em um artefato da atividade, conforme a skill instalada.
2. Levante o inventário abaixo. Para cada item, registre **caminho local ou URL do GitHub**, **responsabilidade na atividade** e **status: informado, não existe ou ainda não informado**. Pergunte pelos itens ainda não informados; o usuário pode responder que não existem ou não participam da atividade.

   | Item a confirmar | Caminho local ou URL | Papel na atividade | Status |
   | --- | --- | --- | --- |
   | Gateway |  |  | Ainda não informado |
   | API |  |  | Ainda não informado |
   | Repositório de infraestrutura |  |  | Ainda não informado |
   | Repositório de testes integrados |  |  | Ainda não informado |
   | Repositório de Lambda |  |  | Ainda não informado |
   | Repositório de banco de dados |  |  | Ainda não informado |
   | Outros repositórios envolvidos |  |  | Ainda não informado |

3. Solicite documentação de referência para implantação quando a entrega envolver deploy, infraestrutura, migração, configuração ou contrato operacional; aproveite a documentação já fornecida. Confirme ambientes, responsáveis e restrições de implantação aplicáveis.
4. Inspecione os projetos locais relevantes: instruções do repositório, arquitetura, contratos, configuração, dependências, testes, comandos de build e histórico de decisões. Para URL remota sem checkout, confirme acesso e clone em diretório apropriado. Não presuma que repositórios diferentes compartilham branch, comandos ou permissões.
5. Separe fatos verificados, decisões confirmadas e dúvidas. Faça perguntas objetivas sobre decisões de produto, arquitetura, dados, segurança e implantação que o código e a documentação não resolvem. Registre cada resposta no artefato da atividade. Repita a descoberta enquanto houver dúvida que afete escopo, critério de aceite ou solução; não avance com suposição silenciosa.

### Diagnóstico obrigatório para bugs

Se a tarefa for um bug ou se um bug relevante surgir durante a análise, descreva comportamento observado, comportamento esperado, ambiente e passos de reprodução. Execute a suíte completa de testes unitários aplicável aos repositórios afetados e registre comando, resultado e falhas preexistentes. Procure logs, entradas e saídas, contratos, dados de teste e histórico relevantes. Se a falha não for reproduzida, obtenha os insumos ausentes ou crie um teste de reprodução apropriado antes de definir a correção. Não trate um teste que passa como prova de que o bug não existe. Só siga quando o erro estiver caracterizado de forma verificável ou quando o usuário decidir explicitamente como lidar com uma reprodução indisponível.

## Etapa 1 — Especificação com `tlc-spec-lean`

Use a skill para transformar a solicitação e a descoberta em uma especificação verificável: problema, escopo e exclusões, fluxos afetados, critérios de aceite observáveis, contratos, riscos, dependências, fontes de verdade e perguntas respondidas. Vincule cada critério à necessidade original. Guarde os artefatos no formato exigido pela skill.

`tlc-spec-lean` também pode produzir um `plan.md` e conduzir implementação. **Neste processo, utilize sua saída como base da etapa 2 e não inicie o build nessa etapa.** Preserve os artefatos e as validações obrigatórias da skill. Se a versão instalada exigir uma pausa ou aprovação antes de produzir a saída, cumpra essa exigência; não marque aprovação por conta própria.

**Saída:** especificação e evidências de descoberta, sem decisões pendentes que bloqueiem o plano.

## Etapa 2 — Plano com `tlc-plan`

Use a especificação anterior e os repositórios inspecionados como entrada. Produza ou refine o plano canônico da atividade no formato exigido por `tlc-plan`. Evite criar dois planos divergentes: se `tlc-spec-lean` já criou `plan.md`, preserve seu conteúdo útil e adapte o mesmo artefato ao formato e ao validador de `tlc-plan`.

O plano deve informar: critérios de aceite com valores concretos, solução e contratos afetados, ordem de entregas verificáveis, arquivos ou áreas prováveis, dependências entre repositórios, estratégia de testes, riscos de segurança, plano de migração/implantação quando aplicável, rollback quando aplicável e comandos de validação. Planeje testes para fluxos esperados, erros, limites e regressões. Defina como medir **cobertura de linhas superior a 95% nas linhas de código adicionadas**; se a ferramenta medir apenas a cobertura total, use um método de cobertura do diff ou evidência equivalente. Não confunda cobertura total do projeto com cobertura das linhas novas.

Execute os validadores da skill e corrija o plano até passar. Em seguida, apresente o caminho do arquivo e um resumo e pergunte explicitamente:

> Você leu e aprova o plano em `<caminho/do/plan.md>` para iniciar a implementação? Responda **SIM** ou **NÃO**. Se NÃO, informe o que ficou faltando, o que está além do escopo ou o que deve mudar.

Somente um **SIM explícito após a apresentação da versão atual** libera a etapa 3. Registre no plano as palavras da aprovação e a versão aprovada. Se a resposta for NÃO ou trouxer ajustes, volte à descoberta e à especificação quando necessário, revise o plano, valide novamente e peça nova aprovação. Qualquer dúvida nova que mude obrigação, escopo ou decisão deve seguir esse mesmo ciclo.

## Etapa 3 — Implementação com `tlc-implement`

Leia o plano aprovado e execute a skill conforme suas regras de checks, provas e verificação. Antes de editar, confira o estado do Git e as instruções de cada repositório. No repositório de implementação, confirme que `develop` existe e que a base local está atualizada; crie a branch `feature/{nome-branch}`, com nome curto ligado ao tema ou ao ticket do iuclick. Se `develop` não existir, houver alterações locais conflitantes ou não for possível atualizá-la, registre o impedimento e peça a decisão necessária. Não descarte alterações existentes.

Implemente fatias pequenas e completas. Teste cada fatia e faça commits apenas de partes concluídas e verificadas. Use mensagens de commit em português, descritivas e consistentes com a convenção do repositório; se a skill exigir Conventional Commits, preserve o prefixo e escreva a descrição em português. Registre o hash e as provas de cada marco.

Execute testes unitários, de integração e de ponta a ponta relevantes, além de lint, build e checagens de segurança disponíveis. Os testes unitários devem cobrir os casos aplicáveis, inclusive erros e limites; a cobertura das linhas adicionadas deve ser **estritamente maior que 95%**. Cubra os critérios de aceite com provas que de fato falhariam se o comportamento estivesse incorreto. Não altere testes apenas para esconder falhas.

Siga padrões de desenvolvimento seguro adequados à linguagem e ao projeto: valide entradas, controle autenticação e autorização, proteja dados sensíveis e segredos, use acesso seguro a banco e dependências, evite injeção e registre a avaliação das CWE pertinentes à mudança. Não afirme ausência de vulnerabilidades sem evidência.

Se surgir dúvida que afete comportamento, contrato, arquitetura ou escopo, **suspenda a implementação**, registre a pergunta e volte às etapas 1 e 2. Atualize os artefatos, obtenha nova aprovação do plano alterado e só então retome. Preserve código local seguro já produzido; não apague trabalho para reiniciar o ciclo.

**Saída:** código e testes em commits locais, checks e provas da skill, comandos executados, cobertura das linhas novas e pendências explícitas.

## Etapa 4 — Avaliação com `spec-driven-eval`

Invoque explicitamente a skill e avalie o código, os testes e os artefatos contra a solicitação original e os critérios aprovados. Registre a base e o `HEAD` avaliados, o diff, as evidências por critério, os resultados dos testes, a cobertura e as falhas. Durante a avaliação, mantenha o código avaliado somente para leitura, conforme a skill; correções iniciam uma nova rodada de implementação e avaliação.

Esta combinação de skills pode gerar `request.md`, `plan.md` e `checks.md`, enquanto `spec-driven-eval` prevê também `spec.md` e `tasks.md` para algumas notas. **Não invente esses arquivos ou notas.** Use os artefatos reais como evidência e marque eixos que a skill não conseguir calcular como `n/a`, explicando o motivo. Um escore agregado alto, isoladamente, não libera a entrega.

A avaliação só é positiva para este fluxo quando **todos** os critérios obrigatórios aprovados têm evidência de atendimento, os checks e validadores da implementação passam, os testes relevantes passam, a cobertura das linhas adicionadas é superior a 95% e não resta achado de segurança bloqueante. Se qualquer condição falhar, liste lacunas com evidência, volte ao planejamento para mudanças de escopo/critério ou à implementação para falhas frente ao plano já aprovado, e repita a avaliação integral no novo `HEAD`.

Após avaliação positiva, apresente o relatório e solicite autorização explícita para `git push` e criação do PR, com repositório, branch de origem, branch de destino e resumo da mudança. Só execute publicação após essa autorização. Não faça deploy ou alteração de dados de produção sem autorização específica.

## Estado e resposta ao usuário

Ao fim de cada etapa, informe: artefatos criados/atualizados, decisões confirmadas, comandos e resultados, pendências e próxima condição de avanço. Em uma retomada, leia os artefatos e o estado do Git antes de agir. Nunca declare uma etapa concluída apenas porque um arquivo existe: confira seu conteúdo e os validadores da skill correspondente.
