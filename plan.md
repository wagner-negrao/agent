
Irei Executar o processo de criar um agente no Devin CLI, quero deixar de forma estruturada minhas necessidades e comandos para que quando eu for executar dentro do devin ele consiga extrair o melhor pois está de forma organizada. 

Devido a isso quero que fique de forma estruturada esse documento sendo possivel trocar os links e comandos para download

Caso queira aprimorar algo mais faça perguntas!


Quero construir um agente no para ser utilizados em projetos de desenvolvimento tanto projetos grandes como projetos que estão sendo iniciados.

Irei criar o agente no DEVIN CLI para utilizar seus recursos.

Quero construir um processo de planejamento da atividade e sua especificação, criar um plano, ir para parte de implementação com base no plano, por fim revisar o que foi especificado para o que foi implementado.



Para parte de plano e especificação quero utilizar o https://agent-skills.techleads.club/skills/tlc-spec-lean/ e caso não possua na maquina de quem estiver executando possa baixar com o seguinte comando npx @tech-leads-club/agent-skills install --skill tlc-spec-lean desta forma sendo possível planejar e especificar de forma estruturada utilizando essa skill, com o resultado dela será feito de input para próxima etapa, caso exista duvidas devem obrigatoriamente ser feitas para que não seja tomada nenhuma decisão sem afirmações. Sempre solicitar que sejam informados o Gateway, API, repositório de infra, repositório de teste integrado, repositório de lambda, repositório de banco de dados, caso existam cada um desses e se não foram passados no input inicial, solicitar o path do repositório local ou link do GitHub para que seja feito o clone, com a informação local valide o projeto os projetos para contribuir com as informações e construir um melhor solução. Solicitar documentação de referencia para implantação caso seja necessário ou se já exista no input inicial. Caso existam duvidas fazer um loop até chegar em um ponto que não existam duvidas, só deve seguir para a próxima parte caso todas as duvidas sejam resolvidas. Se for identificado um BUG ou se atividade for BUG então deve-se executar todos os teste unitários verificar se algum falha caso não seja possivel identificar deve-se gerar mais insumos para que seja possivel identificar e então seguir o fluxo, a ideia é conseguir ter de forma clara o erro.







Na segunda etapa com o impute anterior deve-se utilizar a skill https://agent-skills.techleads.club/skills/tlc-plan/ e caso necessário baixar npx @tech-leads-club/agent-skills install --skill tlc-plan nela teremos o planejamento do que será feito, como será, em que ordem e demais atividades, nessa etapa deve ter um pergunta de forma explicita solicitando ler o arquivo e plano para que possa seguir para etapa seguinte, caso seja um SIM deve seguir caso seja um NAO deve validar o que ficou fora do plano ou o que está além do plano. Todos os testes unitários devem cobrir as possíveis casos do código, todo código produzido deve ter mais de 95% de cobertura para as linhas que foram adicionadas. O processo de desenvolvimento deve seguir as boas praticas de commit, os commits devem ser em português, sempre deve olhar partir da branch develop e criar um branch com o seguinte padrão feature/{nome-branch} o nome deve ser relacionado ao tema ou deve ter o nome do ticket do iuclick. Sempre faça commits de partes concluídas e testadas, faça commits em blocos para ter melhor rastreabilidade. Caso existam duvidas deve-se OBRIGATORIAMENTE fazer um loop indo para o inicio do processo para ter claro tudo que está sendo planejado.







Na terceira etapa iremos fazer a parte de implementação com a skill https://agent-skills.techleads.club/skills/tlc-implement/ nele iremos utilizar o principais recursos da linguagem e processo de desenvolvimento que foram definidos para implantar, caso existam duvidas nessa etapa deve ser cancelado o processo de desenvolvimento de retornar para o processo de planejamento com as duvidas que foram apresentadas pois nesse momento deve ter claro as implementações que devem ser feitas, desta forma enquanto houver duvidas repita o processo até não haver duvidas, caso necessário baixe a skill npx @tech-leads-club/agent-skills install --skill tlc-implement. Nodesenvolvimento é extremamente importante seguir os critérios de desenvolvimento seguro para não cair em problemas de segurança e CWE.





Na quarta etapa iremos fazer a parte de validação do que foi definido https://agent-skills.techleads.club/skills/spec-driven-eval/ caso não exista local baixar com o comando npx @tech-leads-club/agent-skills install --skill spec-driven-eval Nessa etapa iremos validar se o que foi especificado foi entregue na solução antes de gerar de fazer o Push e gerar o PR, esse processo e muito importante pois garante a qualidade da entrega caso o a avaliação seja positiva então pode ser feito o push caso não deve-se definir o que não foi feito e pedir para ir para o processo de planejamento e posteriormente ir para implementação e cair no processo de validação, esse loop deve ocorrer para implemtações que não conseguiram ser aprovadas.





