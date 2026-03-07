# Teste Técnico - QA Tester - 4blue

## Contexto

Este documento apresenta os resultados dos testes exploratórios realizados em um microssistema composto pelas telas de Login, Cadastro e Sucesso, com o objetivo de identificar falhas funcionais, inconsistências de interface e oportunidades de melhoria na aplicação.

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

### BUG 03 - Ausência de validação do formato de e-mail no cadastro
**Descrição:** Foram realizados os testes de cadastro utilizando valores inválidos no campo de e-mail, com o objetivo de verificar se o sistema valida corretamente o formato do endereço informado.

**Passos para reproduzir:**
1. Acessar a tela de cadastro.
2. Informar um e-mail inválido, como `teste`, `teste@` ou `teste.com`.
3. Preencher os demais campos com dados válidos.
4. Clicar no botão "Criar Conta".

**Resultado atual:** Nos cenários testados, o sistema permitiu concluir o cadastro mesmo quando o e-mail informado apresentava formato inválido.

**Resultado esperado:** O sistema deve validar o formato do e-mail conforme o padrão indicado pelo campo (ex.: `usuario@dominio.com`) antes de permitir a submissão do formulário, exibindo uma mensagem de erro quando o valor informado não estiver de acordo com o formato esperado. Essa validação deve garantir que o endereço contenha os elementos mínimos de um e-mail válido, como identificador do usuário, símbolo @ e domínio. Além disso, é essencial para garantir a integridade das informações cadastradas e o funcionamento adequado de funcionalidades que dependem desse dado, como autenticação, recuperação de senha e comunicação com o usuário.

**Severidade:** Alta  
**Prioridade:** Alta

---

### BUG 04 - Ausência de validação de e-mail já cadastrado
**Descrição:** Foram realizados testes de cadastro utilizando um endereço de e-mail previamente registrado no sistema, com o objetivo de verificar se a aplicação valida a unicidade desse identificador no momento da criação de novas contas.

**Passos para reproduzir:** 
1. Acessar a tela de cadastro.
2. Realizar um cadastro com um e-mail válido (exemplo: `teste@email.com`).
3. Após a conclusão do cadastro, acessar novamente a tela de criação de conta.
4. Preencher os campos com novos dados, informando novamente o mesmo e-mail (`teste@email.com`).
5. Clicar no botão "Criar Conta".

**Resultado atual:** Nos cenários testados, o sistema permitiu concluir o cadastro mesmo quando o e-mail informado já estava previamente registrado na base de usuários.

**Resultado esperado:** O sistema deve validar se o e-mail informado já está cadastrado antes de permitir a submissão do formulário, impedir a criação de contas duplicadas e exibir uma mensagem informativa ao usuário, como "Este e-mail já está cadastrado". Essa validação é essencial para garantir a unicidade do identificador de conta, preservar a integridade da base de dados e evitar inconsistências em funcionalidades como autenticação, recuperação de senha e comunicação com o usuário. O sistema também pode orientar o usuário a realizar login ou utilizar a funcionalidade de recuperação de senha caso já possua uma conta cadastrada. 

**Severidade:** Alta
**Prioridade:** Alta

---

### BUG 05 - Ausência de validação do formato e conteúdo do campo telefone
**Descrição:** Foram realizados os testes de cadastro informando valores inválidos no campo de telefone, com o objetivo de verificar se o sistema valida corretamente o formato e o conteúdo numérico esperado para esse campo.

**Passos para reproduzir:**
1. Acessar a tela de cadastro.
2. Informar um telefone incompleto ou inválido no campo correspondente.
3. Preencher os demais campos com dados válidos.
4. Clicar no botão "Criar Conta".

**Resultado atual:** Nos cenários testados, o sistema permitiu concluir o cadastro mesmo quando o telefone informado apresentava formato inválido ou continha caracteres não numéricos.

**Resultado esperado:** O sistema deve validar o formato e a quantidade de dígitos do telefone, conforme indicado pela máscara do campo `(00) 00000-0000`, além de restringir a entrada apenas a caracteres numéricos, antes de permitir a submissão do formulário. Essa validação deve garantir que o campo aceite somente números e que o telefone esteja completo de acordo com o padrão esperado. Sem essas validações, o sistema pode registrar dados incorretos ou inconsistentes, comprometendo processos como comunicação com o usuário, autenticação adicional e recuperação de conta.

**Severidade:** Média  
**Prioridade:** Média

---

### BUG 06 - Ausência de validação de igualdade entre os campos senha e confirmar senha
**Descrição:** Foram realizados os testes de cadastro informando valores diferentes nos campos de senha e confirmação de senha, com o objetivo de verificar se o sistema valida corretamente a correspondência entre esses dois campos.

**Passos para reproduzir:**
1. Acessar a tela de cadastro.
2. Preencher o campo senha com um valor.
3. Preencher o campo confirmar senha com um valor diferente.
4. Preencher os demais campos com dados válidos.
5. Clicar no botão "Criar Conta".

**Resultado atual:** Nos cenários testados, o sistema permitiu concluir o cadastro mesmo quando os valores informados nos campos de senha e confirmação eram diferentes.

**Resultado esperado:** O sistema deve validar se os valores informados nos campos senha e confirmar senha são idênticos antes de permitir a submissão do formulário, exibindo uma mensagem de erro quando houver divergência entre os campos. Essa validação é necessária para garantir que o usuário cadastre corretamente suas credenciais e evitar situações em que a conta seja criada com uma senha diferente da pretendida, o que pode impedir futuros acessos e gerar demandas adicionais de recuperação de senha.

**Severidade:** Alta  
**Prioridade:** Alta

---

### BUG 07 - Ausência de validação de critérios mínimos de segurança para senha
**Descrição:** Foram realizados os testes de cadastro informando senhas que não atendem aos critérios mínimos de segurança esperados, com o objetivo de verificar se o sistema valida corretamente os requisitos definidos para criação de senha.

**Passos para reproduzir:**
1. Acessar a tela de cadastro.
2. Informar uma senha que não atenda aos critérios mínimos definidos (por exemplo, com menos de 8 caracteres ou sem caractere especial).
3. Preencher o campo confirmar senha com o mesmo valor.
4. Preencher os demais campos com dados válidos.
5. Clicar no botão "Criar Conta".

**Resultado atual:** Nos cenários testados, o sistema permitiu concluir o cadastro mesmo quando a senha informada não atendia aos critérios mínimos de segurança.

**Resultado esperado:** O sistema deve validar os critérios mínimos de segurança da senha antes de permitir a submissão do formulário, como quantidade mínima de caracteres e presença de caracteres especiais, exibindo mensagens claras quando os requisitos não forem atendidos. A ausência dessa validação pode permitir a criação de senhas fracas, aumentando o risco de acessos indevidos, ataques de força bruta e comprometimento de contas de usuários, além de indicar falhas nas práticas básicas de segurança da aplicação.

**Severidade:** Alta  
**Prioridade:** Alta

---

### BUG 08 - Sobreposição e quebra de layout entre campos do formulário na tela de cadastro
**Descrição:** Foi realizada a análise da interface da tela de cadastro com o objetivo de verificar a consistência visual e o alinhamento dos elementos do formulário em relação ao container principal.

**Passos para reproduzir:**
1. Acessar a tela de cadastro.
2. Observar o posicionamento e o alinhamento dos campos do formulário.
3. Verificar a relação visual entre os inputs e os limites do card principal.

**Resultado atual:** No cenário observado, os campos posicionados na coluna direita do formulário, como **Telefone** e **Confirmar senha**, ultrapassam os limites esperados de layout e ficam parcialmente sobrepostos aos campos da coluna esquerda (**Nome completo** e **Senha**). Além disso, esses campos também excedem os limites visuais do card principal, causando quebra de layout e desalinhamento na interface.

**Resultado esperado:** Os campos do formulário devem manter alinhamento consistente em suas respectivas colunas, sem sobreposição entre elementos e respeitando os limites do container principal. Essa organização é essencial para preservar a clareza visual da interface e garantir uma experiência adequada ao usuário durante o preenchimento do cadastro.

**Severidade:** Média  
**Prioridade:** Média

---



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

