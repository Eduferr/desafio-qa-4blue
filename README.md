# Teste Técnico - QA Tester - 4blue

## Contexto
Este documento apresenta os resultados dos testes exploratórios realizados em um microssistema composto pelas telas de Login, cadastro e tela de Sucesso, com o objetivo de identificar falhas funcionais, inconsistências de interface e oportunidades de melhoria na aplicação.
Cada ocorrência foi registrada e classificada conforme sua severidade e prioridade.

**Sistema avaliado:** `https://qa-play-sim.lovable.app/`  

---

## Estratégia de análise
A análise considerou os seguintes aspectos do sistema:
- Comportamento funcional das telas de login e cadastro;
- Validação de campos obrigatórios e formato dos dados informados;
- Mensagens de erro e de sucesso apresentadas ao usuário;
- Consistência visual e comportamento em viewport mobile;
- Possíveis riscos básicos relacionados à segurança;
- Aspectos de testabilidade visando uma futura automação de testes.

---

# Bugs encontrados

## Tela de cadastro

### BUG 01 - Ausência total de dados na submissão do cadastro
**Descrição:** Foi realizado o teste de cadastro com todos os campos obrigatórios (nome, telefone, e-mail, senha e confirmação de senha) deixados em branco.

**Passos para reproduzir:**
1. Acessar a tela de cadastro.
2. Deixar todos os campos do formulário em branco.
3. Clicar no botão "Criar Conta".

**Resultado atual:** No cenário testado, o sistema permitiu concluir o cadastro sem nenhum dado preenchido.

**Resultado esperado:** O sistema deve impedir a submissão do formulário quando nenhum dado for preenchido e exibir mensagens de validação para cada campo obrigatório, informando que o preenchimento é necessário. Essa validação é essencial para preservar a integridade dos dados e o funcionamento do sistema de autenticação da aplicação.

**Severidade:** Crítica  
**Prioridade:** Alta

---

### BUG 02 - Ausência parcial de dados na submissão do cadastro
**Descrição:** Foram realizados testes de cadastro com preenchimento parcial dos campos obrigatórios. Em cada execução, um dos campos (nome, telefone, e-mail, senha ou confirmação de senha) foi deixado em branco para verificar a validação individual dos campos obrigatórios.

**Passos para reproduzir:**
1. Acessar a tela de cadastro.
2. Preencher apenas um ou alguns campos do formulário (por exemplo: apenas nome ou apenas e-mail).
3. Deixar os demais campos obrigatórios em branco.
4. Clicar no botão "Criar Conta".

**Resultado atual:** Em todos os cenários testados, o sistema permitiu a conclusão do cadastro mesmo com um dos campos obrigatórios deixado em branco.

**Resultado esperado:** O sistema deve impedir a submissão do formulário quando qualquer campo obrigatório não estiver preenchido e apresentar mensagens de validação específicas para o campo correspondente. Essa validação é necessária para garantir a integridade e consistência dos dados cadastrados, evitando a criação de registros incompletos que possam impactar funcionalidades como autenticação, recuperação de conta, comunicação com o usuário e rastreabilidade das informações.

**Severidade:** Crítica  
**Prioridade:** Alta

---

### BUG 03 - Campo de e-mail não valida formato
**Descrição:** O campo de e-mail apresenta uma máscara que indica um formato específico, porém o sistema não valida corretamente valores inválidos informados no campo.

**Passos para reproduzir:**
1. Acessar a tela de cadastro.
2. Informar um e-mail inválido, como `teste`, `teste@` ou `teste.com`.
3. Preencher os demais campos com dados válidos.
4. Clicar no botão "Criar Conta".

**Resultado atual:** O sistema permite concluir o cadastro mesmo quando o e-mail informado está em formato inválido.

**Resultado esperado:** O sistema deve validar o formato do e-mail e impedir o cadastro enquanto o valor informado estiver fora do padrão esperado. Sem essa validação, usuários com endereços inválidos podem ser cadastrados, o que compromete a integridade da base de dados e dificulta processos que dependem desse contato, como recuperação de senha, envio de notificações e comunicação com o usuário.

**Severidade:** Alta  
**Prioridade:** Alta

---

### BUG 04 - Campo de telefone não valida formato e caracteres numéricos
**Descrição:** Embora exista uma máscara visual para o telefone, não há validação efetiva do conteúdo informado no campo.

**Passos para reproduzir:**
1. Acessar a tela de cadastro.
2. Informar telefone incompleto ou inválido.
3. Preencher os demais campos com dados válidos.
4. Clicar no botão "Criar Conta".

**Resultado atual:** O sistema aceita qualquer tipo de valor no campo de telefone, incluindo números, letras e outros caracteres, sem realizar validação do formato.

**Resultado esperado:** O sistema deve validar a quantidade de dígitos e o formato do telefone antes de permitir a conclusão do cadastro. Sem essa validação, o sistema pode aceitar dados inválidos ou incompletos, o que compromete a qualidade e a confiabilidade das informações armazenadas, podendo gerar inconsistências na base de dados e dificultar processos como contato com o usuário, recuperação de conta, autenticação adicional e outras formas de comunicação.

**Severidade:** Média  
**Prioridade:** Média

---

### BUG 05 - Campos senha e confirmar senha não validam igualdade
**Descrição:** O sistema não verifica se os campos de senha e confirmação possuem exatamente o mesmo valor.

**Passos para reproduzir:**
1. Acessar a tela de cadastro.
2. Preencher o campo senha com um valor.
3. Preencher o campo confirmação de senha com um valor diferente.
4. Preencher os demais campos com dados válidos.
5. Clicar no botão "Criar Conta".

**Resultado atual:** O sistema permite concluir o cadastro mesmo quando os valores de senha e confirmação são diferentes.

**Resultado esperado:** O sistema deve impedir o cadastro e informar que os campos de senha e confirmação precisam possuir o mesmo valor. A ausência dessa validação pode resultar na criação de contas com credenciais diferentes das pretendidas pelo usuário. Esse comportamento pode impedir futuros acessos à conta, gerar frustração durante o login e aumentar a demanda por suporte para recuperação de senha.

**Severidade:** Alta  
**Prioridade:** Alta

---

### BUG 06 - Campo de senha não valida critérios mínimos definidos
**Descrição:** O campo de senha não valida as regras mínimas esperadas, como possuir no mínimo 8 caracteres e ao menos 1 caractere especial.

**Passos para reproduzir:**
1. Acessar a tela de cadastro.
2. Informar senha curta ou sem caractere especial.
3. Confirmar a senha.
4. Preencher os demais campos com dados válidos.
5. Clicar no botão "Criar Conta".

**Resultado atual:** O sistema aceita senhas que não atendem aos critérios mínimos definidos.

**Resultado esperado:** O sistema deve rejeitar senhas que não atendam aos critérios mínimos definidos e exibir uma mensagem clara informando o motivo da rejeição. A ausência dessa validação pode permitir a criação de senhas fracas, o que aumenta o risco de acessos indevidos, ataques de força bruta e comprometimento de contas de usuários, além de indicar falhas nas práticas básicas de segurança da aplicação.

**Severidade:** Alta  
**Prioridade:** Alta

---

### BUG 07 - Campos do formulário ultrapassam o container 
**Descrição:** Na tela de cadastro, alguns campos do formulário, como Telefone e Confirmar senha, excedem os limites visuais do card principal, causando quebra de layout e desalinhamento entre os elementos da interface.

**Passos para reproduzir:**
1. Acessar a tela de cadastro.
2. Observar o posicionamento dos campos no formulário.
3. Verificar o alinhamento visual dos inputs em relação ao container principal.

**Resultado atual:** Alguns campos ultrapassam a área do card, ficando visualmente desalinhados e comprometendo a organização da interface.

**Resultado esperado:** Todos os campos devem permanecer contidos dentro do card, com largura, espaçamento e alinhamento consistentes, preservando a harmonia visual da tela. Quando esse padrão não é mantido, a consistência visual da interface é comprometida, podendo transmitir a sensação de baixa qualidade do produto e prejudicar a experiência do usuário ao dificultar a leitura e o preenchimento dos campos, especialmente em fluxos sensíveis como o cadastro.

**Severidade:** Média  
**Prioridade:** Média

---

### BUG 08 - Sistema permite cadastro com e-mail já existente
**Descrição:** O sistema não valida se o e-mail informado já está cadastrado na base de usuários, permitindo a criação de múltiplas contas com o mesmo endereço de e-mail.

**Passos para reproduzir:** 
1. Acessar a tela de cadastro.
2. Realizar um cadastro com um e-mail válido (exemplo: teste@email.com).
3. Após concluir o cadastro, acessar novamente a tela de cadastro.
4. Tentar cadastrar um novo usuário utilizando o mesmo e-mail.

**Resultado atual:** O sistema permite concluir o cadastro utilizando um e-mail que já existe na base de dados dos usuários.

**Resultado esperado:** O sistema deve impedir o cadastro quando o e-mail informado já estiver registrado e exibir uma mensagem informando que aquele endereço já está cadastrado, orientando o usuário a fazer login ou recuperar a senha. Quando essa validação não existe, o sistema pode permitir a criação de várias contas com o mesmo e-mail, o que compromete a integridade dos dados e pode gerar problemas em funcionalidades como login, recuperação de senha e comunicação com o usuário. Além disso, pode causar conflitos na gestão das contas e dificultar o atendimento em casos de suporte.

**Severidade:** Alta
**Prioridade:** Alta

---

## Tela de Login

### BUG 09 - Sistema permite login com e-mail e senha vazios após cadastro inconsistente
**Descrição:** Após a criação de um usuário com e-mail e senha vazios, o sistema passa a permitir login sem o preenchimento desses campos.

**Passos para reproduzir:**
1. Realizar cadastro com campos email e senha vazios.
2. Acessar a tela de login.
3. Deixar e-mail e senha em branco.
4. Clicar em "Entrar".

**Resultado atual:** O sistema autentica o usuário mesmo com e-mail e senha vazios.

**Resultado esperado:** O sistema deve impedir o login quando os campos de e-mail e senha estiverem vazios e não permitir que registros inválidos sejam utilizados para autenticação. Sem essa validação, o sistema pode permitir acesso sem credenciais válidas, o que representa um risco à segurança, comprometendo o controle de acesso da aplicação e permitindo que usuários não autorizados acessem o sistema. 

**Severidade:** Crítica  
**Prioridade:** Alta

---

### BUG 10 - Mensagem de erro de login é genérica
**Descrição:** Ao tentar fazer login, o sistema exibe apenas a mensagem genérica "Conta não encontrada. Crie uma conta primeiro." Esse tipo de mensagem não deixa claro se o problema está no e-mail informado, na senha incorreta ou em outro motivo.


**Passos para reproduzir:**
1. Acessar a tela de login.
2. Informar credenciais inválidas ou parcialmente incorretas.
3. Clicar em "Entrar".

**Resultado atual:** O sistema exibe uma mensagem genérica, que não ajuda o usuário a entender o motivo da falha no login.

**Resultado esperado:** O sistema deve exibir uma mensagem mais clara para o usuário, indicando o motivo da falha no login. A mensagem atual é muito genérica e dificulta entender se o problema está no e-mail, na senha ou em outra situação. Isso pode gerar tentativas repetidas de acesso, frustração para o usuário e aumento na procura por suporte.

**Severidade:** Média  
**Prioridade:** Média

---

### BUG 11 - Login válido exibe ao mesmo tempo mensagem de sucesso e erro inesperado
**Descrição:** Ao realizar login com credenciais válidas, o sistema mostra a mensagem de sucesso, mas também exibe um alerta de "Erro inesperado".

**Passos para reproduzir:**
1. Cadastrar um usuário válido.
2. Acessar a tela de login.
3. Informar e-mail e senha válidos.
4. Clicar em "Entrar".

**Resultado atual:** O sistema exibe ao mesmo tempo uma mensagem de sucesso e um alerta de erro.

Resultado esperado: Quando o login for realizado com sucesso, apenas a mensagem de sucesso deve ser exibida, seguida do fluxo normal da aplicação. Quando o sistema mostra sucesso e erro ao mesmo tempo, isso gera confusão para o usuário, que pode entender que o login falhou mesmo tendo sido realizado corretamente. Esse tipo de comportamento também passa a sensação de instabilidade ou falha no sistema.

**Severidade:** Alta  
**Prioridade:** Alta

---

### BUG 12 – Texto de validação de senha exibido incorretamente na tela de login
**Descrição:** Na tela de login, abaixo do campo de senha, é exibida a mensagem "A senha precisa ter no mínimo 8 caracteres e 1 caractere especial.". Esse texto se refere às regras de criação de senha (usadas no cadastro ou redefinição de senha) e não deveria aparecer no fluxo de login.

**Passos para reproduzir:**
1. Acessar a tela de login da aplicação.
2. Observar o texto exibido abaixo do campo Senha.

**Resultado atual:** A tela de login exibe a mensagem "A senha precisa ter no mínimo 8 caracteres e 1 caractere especial.", que corresponde à validação de criação de senha e não ao processo de autenticação.

**Resultado esperado:** A tela de login não deve exibir regras de criação de senha. Em vez disso, deve apresentar a opção "Esqueceu a senha?", para direcionar o usuário ao fluxo de recuperação ou redefinição de senha. A ausência dessa opção dificulta o acesso de usuários que esqueceram suas credenciais.

**Severidade:** Baixa
**Prioridade:** Baixa

---

## Problemas Gerais

### BUG 13 - Problemas de responsividade em viewport mobile
**Descrição:** Alguns elementos da interface ficam desconfigurados quando acessa o sistema em dispositivos móveis.

**Passos para reproduzir:**
1. Abrir o sistema em viewport mobile.
2. Acessar as telas de login e cadastro.
3. Observar a disposição dos elementos na tela.

**Resultado atual:** O layout apresenta quebra visual, excesso de espaço vertical e uma experiência inconsistente em dispositivos móveis.

**Resultado esperado:** Os elementos devem se ajustar corretamente ao tamanho da tela em dispositivos móveis, mantendo alinhamento, proporção adequada e sem rolagem desnecessária. Esse problema de responsividade prejudica a navegação em dispositivos móveis, dificultando a visualização e a interação com os formulários. Como grande parte dos acessos a sistemas web acontece por smartphones, essa falha pode impactar a usabilidade, a percepção de qualidade do produto e até a conversão de usuários.

**Severidade:** Médio  
**Prioridade:** Média

---

### BUG 14 - Ausência de identificadores estáveis nos elementos prejudica automação e manutenção

**Descrição:** Os elementos interativos das telas, como campos de entrada e botões de ação, não possuem identificadores estáveis como `id`, `name` ou `data-testid`. Ao inspecionar os elementos no navegador, observa-se que os campos dependem principalmente de atributos como `class`, `type` e `placeholder`, que não são ideais para automação de testes e rastreabilidade técnica.

**Passos para reproduzir:**
1. Acessar as telas de login e cadastro.
2. Inspecionar os campos e botões no navegador.
3. Verificar os atributos disponíveis nos elementos interativos.

**Resultado atual:** Os elementos não possuem identificadores estáveis que facilitem a criação e manutenção de testes automatizados.

**Resultado atual:** Os elementos não possuem identificadores estáveis que facilitem a criação e manutenção de testes automatizados.

**Resultado esperado:** Os componentes interativos devem possuir identificadores únicos e estáveis, como `data-testid` ou, alternativamente, `id` ou `name`, para facilitar a automação e a manutenção dos testes. Sem esses identificadores, os testes acabam dependendo de seletores frágeis, como `:nth-child()`, classes visuais ou a própria hierarquia do DOM. Com isso, qualquer alteração no layout pode quebrar os testes, mesmo sem mudança funcional na aplicação.

**Severidade:** Baixo  
**Prioridade:** Média

---

## Quais 2 bugs eu corrigiria primeiro e por quê?
Conforme solicitado na tarefa, segue a priorização dos dois bugs mais críticos para correção imediata.

### 1) BUG 01 - Sistema permite cadastrar usuário com todos os campos vazios
Eu corrigiria este bug primeiro porque ele compromete a integridade do dado na origem. 
Quando o sistema aceita registros totalmente vazios, toda a cadeia seguinte fica contaminada: autenticação, consistência da base, experiência do usuário e confiabilidade do produto.

### 2) BUG 09 - Sistema permite login com e-mail e senha vazios após cadastro inconsistente
Este seria o segundo bug a ser corrigido porque representa a consequência mais grave do problema anterior: falha de autenticação com impacto direto em segurança e regra de negócio. 
Permitir login com credenciais vazias é uma quebra crítica do fluxo principal do sistema.

**Justificativa geral da ordem:**
Esses dois bugs afetam o núcleo do produto: cadastro e autenticação. Além do alto impacto funcional, geram risco de segurança, comprometem a credibilidade da aplicação e inviabilizam qualquer confiança mínima no fluxo principal do usuário.

---

## Sugestões de melhoria

### Melhorias funcionais
- Implementar validação obrigatória campo a campo antes do envio.
- Identificar visualmente os campos obrigatórios utilizando o símbolo (*) ao lado do rótulo do campo.
- Exibir legenda informando que (*) indica campo obrigatório.
- Validar formato de e-mail e telefone no front-end e no back-end.
- Validar regras de senha com mensagens objetivas.
- Garantir comparação entre senha e confirmação de senha.
- Bloquear submissão quando houver inconsistências.

### Melhorias de experiência do usuário
- Exibir mensagens mais claras e contextualizadas por campo.
- Destacar visualmente os campos inválidos.
- Evitar alertas contraditórios no mesmo fluxo.
- Ajustar layout mobile para eliminar quebras visuais e rolagem desnecessária.

### Melhorias técnicas
- Criar identificadores estáveis nos elementos, preferencialmente com `data-testid`.
- Padronizar tratamento de erros entre front-end e back-end.
- Adicionar testes automatizados para cenários positivos, negativos e de borda.
- Criar validações server-side para impedir bypass de regras de negócio.

---

## Resumo executivo
O sistema apresenta falhas relevantes em três frentes principais:
1. **Validação de dados:** cadastro e login aceitam entradas inválidas ou vazias.
2. **Confiabilidade do fluxo:** há comportamento contraditório no login com sucesso e erro simultâneos.
3. **Experiência e qualidade técnica:** problemas de responsividade, mensagens pouco úteis e baixa testabilidade dos elementos.

O cenário indica necessidade de reforço imediato nas validações de entrada, nas regras de autenticação e na padronização da experiência do usuário.

