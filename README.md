# Teste Técnico - QA Tester - 4blue

## Contexto

Este documento apresenta os resultados dos testes exploratórios realizados em um microssistema composto pelas telas de Login, Cadastro e Sucesso, com o objetivo de identificar falhas funcionais, inconsistências de interface e oportunidades de melhoria da aplicação.

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

## 📝 Tela de cadastro

### BUG 01 - Ausência total de dados na submissão do cadastro  

**Descrição:** Foi realizado o teste de cadastro com todos os campos obrigatórios (nome, telefone, e-mail, senha e confirmação de senha) deixados em branco.

**Passos para reproduzir:**
1. Acessar a tela de cadastro.
2. Deixar todos os campos do formulário em branco.
3. Clicar no botão "Criar Conta".

**Resultado atual:** No cenário testado, o sistema permitiu concluir o cadastro sem nenhum dado preenchido.

**Resultado esperado:** O sistema deve impedir a submissão do formulário quando nenhum dado for preenchido e exibir mensagens de validação para cada campo obrigatório, informando que o preenchimento é necessário. Essa validação é essencial para preservar a integridade dos dados e o funcionamento do sistema de autenticação da aplicação.

**Severidade:** Crítica  
**Prioridade:** Alta\
**Evidência:** [Ausência total de dados na submissão](https://drive.google.com/file/d/1VjPqs_c17_RciTYtFVtGL7Nci5xVIeGz/view?usp=drive_link) 

---

### BUG 02 - Ausência parcial de dados na submissão do cadastro  

**Descrição:** Foram realizados testes de cadastro com preenchimento parcial dos campos obrigatórios. Em cada execução, um dos campos (nome, telefone, e-mail, senha ou confirmação de senha) foi deixado em branco para verificar a validação individual dos campos obrigatórios.

**Passos para reproduzir:**
1. Acessar a tela de cadastro.
2. Preencher apenas um ou alguns campos do formulário (por exemplo: apenas nome ou apenas e-mail).
3. Deixar os demais campos obrigatórios em branco.
4. Clicar no botão "Criar Conta".

**Resultado atual:** Em todos os cenários testados, o sistema permitiu a conclusão do cadastro mesmo com um dos campos obrigatórios deixado em branco.

**Resultado esperado:** O sistema deve impedir a submissão do formulário quando qualquer campo obrigatório não estiver preenchido, exibindo mensagens de validação específicas para o campo correspondente. Essa validação é necessária para garantir a integridade dos dados e evitar a criação de registros incompletos que possam comprometer funcionalidades como autenticação, recuperação de conta e comunicação com o usuário.

**Severidade:** Crítica  
**Prioridade:** Alta\
**Evidência:** [Ausência parcial de dados na submissão](https://drive.google.com/file/d/1gXr5REtdUjw7I2QDg2BfqPt2ubDh4W70/view?usp=drive_link) 

---

### BUG 03 - Ausência de validação do formato de e-mail no cadastro  

**Descrição:** Foram realizados os testes de cadastro utilizando valores inválidos no campo de e-mail, com o objetivo de verificar se o sistema valida corretamente o formato do endereço informado.

**Passos para reproduzir:**
1. Acessar a tela de cadastro.
2. Informar um e-mail inválido, como `teste`, `teste@` ou `teste.com`.
3. Preencher os demais campos com dados válidos.
4. Clicar no botão "Criar Conta".

**Resultado atual:** Nos cenários testados, o sistema permitiu concluir o cadastro mesmo quando o e-mail informado apresentava formato inválido.

**Resultado esperado:** O sistema deve validar o formato do e-mail conforme o padrão esperado (ex.: `usuario@dominio.com`) antes de permitir a submissão do formulário, exibindo mensagem de erro quando o valor informado não estiver em conformidade. Essa validação é necessária para garantir a integridade dos dados e o correto funcionamento de funcionalidades como autenticação, recuperação de senha e comunicação com o usuário.

**Severidade:** Alta  
**Prioridade:** Alta\
**Evidência:** [validação do formato de e-mail](https://drive.google.com/file/d/1POF5ETKGYBHgDxH0BqhEYabLwUPe4zZ4/view?usp=drive_link) 

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

**Resultado esperado:** O sistema deve validar se o e-mail informado já está cadastrado antes de permitir a submissão do formulário, impedindo a criação de contas duplicadas e exibindo uma mensagem informativa ao usuário, como `Este e-mail já está cadastrado`. Essa validação garante a unicidade das contas, preserva a integridade da base de dados e evita inconsistências em funcionalidades como autenticação, recuperação de senha e comunicação com o usuário, podendo também orientar o usuário a realizar login ou recuperar a senha.

**Severidade:** Alta  
**Prioridade:** Alta\
**Evidência:** [validação de e-mail já cadastrado](https://drive.google.com/file/d/1b_35704nvcjxXP7X4x3mGOlSNfr-bFSO/view?usp=drive_link) 

---

### BUG 05 - Ausência de validação do formato e conteúdo do campo telefone  

**Descrição:** Foram realizados os testes de cadastro informando valores inválidos no campo de telefone, com o objetivo de verificar se o sistema valida corretamente o formato e o conteúdo numérico esperado para esse campo.

**Passos para reproduzir:**
1. Acessar a tela de cadastro.
2. Informar um telefone incompleto ou inválido no campo correspondente.
3. Preencher os demais campos com dados válidos.
4. Clicar no botão "Criar Conta".

**Resultado atual:** Nos cenários testados, o sistema permitiu concluir o cadastro mesmo quando o telefone informado apresentava formato inválido ou continha caracteres não numéricos.

**Resultado esperado:** O sistema deve validar o formato e a quantidade de dígitos do telefone conforme a máscara do campo `(00) 00000-0000`, permitindo apenas caracteres numéricos antes da submissão do formulário. Essa validação garante que o número esteja completo e no padrão esperado, evitando o registro de dados incorretos que possam comprometer funcionalidades como comunicação com o usuário, autenticação adicional e recuperação de conta.

**Severidade:** Média  
**Prioridade:** Média\
**Evidência:** [validação do formato e conteúdo do campo telefone](https://drive.google.com/file/d/1Fer5PPAqHN43calWp0_6yxeyqtgtKRTy/view?usp=drive_link) 

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

**Resultado esperado:** O sistema deve validar se os valores informados nos campos senha e confirmar senha são idênticos antes de permitir a submissão do formulário, exibindo mensagem de erro quando houver divergência. Essa validação garante que o usuário cadastre corretamente suas credenciais e evita problemas de acesso ou solicitações desnecessárias de recuperação de senha.

**Severidade:** Alta  
**Prioridade:** Alta\
**Evidência:** [validação de igualdade senha e confirmar senha](https://drive.google.com/file/d/1D0Z8lwYK1j18bdeh5q-r0IuSIQTEclKI/view?usp=drive_link) 

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

**Resultado esperado:** O sistema deve validar critérios mínimos de segurança da senha antes da submissão do formulário, como quantidade mínima de caracteres e presença de caracteres especiais, exibindo mensagens claras quando os requisitos não forem atendidos. Essa validação é necessária para evitar senhas fracas e reduzir riscos de acessos indevidos e comprometimento de contas de usuários.

**Severidade:** Alta  
**Prioridade:** Alta\
**Evidência:** [Ausência de identificadores](https://drive.google.com/file/d/1gTDXfxvFjHeFXNUmEbDloBAXUx-3NY--/view?usp=drive_link) 

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
**Prioridade:** Média\
**Evidência:** [Ausência de identificadores](https://drive.google.com/file/d/1U7YhxAzlC1-DW_3oSLXIjbJ1L2o32g7B/view?usp=drive_link) 

---

## 🔐 Tela de Login

### BUG 09 - Permissão de login com e-mail e senha vazios após cadastro inconsistente  

**Descrição:** Foi realizado o teste de autenticação após criar um cadastro inconsistente, com o objetivo de verificar se o sistema valida corretamente a presença das credenciais obrigatórias (e-mail e senha) no processo de login.

**Passos para reproduzir:**
1. Tentar acessar o sistema com os campos E-mail e Senha em branco.
2. Realizar um cadastro deixando os campos E-mail e Senha vazios.
3. Após a conclusão do cadastro, acessar novamente a tela de login.
4. Realizar novo acesso deixando os campos E-mail e Senha em branco.
5. Clicar no botão "Entrar".

**Resultado atual:** No cenário testado, o sistema permitiu a autenticação do usuário mesmo quando os campos de e-mail e senha estavam vazios.

**Resultado esperado:** O sistema deve impedir o processo de autenticação quando os campos de e-mail e senha não estiverem preenchidos, exibindo uma mensagem de erro apropriada e bloqueando o acesso. Além disso, registros inconsistentes criados durante o processo de cadastro não devem ser aceitos como credenciais válidas para login. A ausência dessa validação compromete o controle de acesso da aplicação e pode representar risco à segurança do sistema.

**Severidade:** Crítica  
**Prioridade:** Alta\
**Evidência:** [Login com e-mail e senha vazios](https://drive.google.com/file/d/1sgXKDgbuuBMXRN7ftJsUzcHcZvQwVzuc/view?usp=drive_link) 

---

### BUG 10 - Permissão de login apenas com e-mail após cadastro inconsistente  

**Descrição:** Foi realizado o teste de autenticação após criar um cadastro inconsistente, com o objetivo de verificar se o sistema valida corretamente a presença das credenciais obrigatórias (senha) no processo de login.

**Passos para reproduzir:**
1. Realizar um cadastro deixando o campo de senha em branco.
2. Após a conclusão do cadastro, acessar a tela de login.
3. Informar o e-mail cadastrado.
4. Deixar o campo de senha em branco.
5. Clicar no botão "Entrar".

**Resultado atual:** No cenário testado, o sistema permitiu a autenticação do usuário informando apenas o e-mail cadastrado, mesmo sem o preenchimento da senha.

**Resultado esperado:** O sistema deve impedir o processo de autenticação quando o campo de senha não estiver preenchido, exibindo uma mensagem de erro apropriada e bloqueando o acesso. Além disso, registros inconsistentes criados durante o processo de cadastro não devem ser aceitos como credenciais válidas para login. A ausência dessa validação compromete o controle de acesso da aplicação e pode representar um risco à segurança do sistema.

**Severidade:** Crítica  
**Prioridade:** Alta\
**Evidência:** [login apenas com e-mail](https://drive.google.com/file/d/1QfKMCU0lvDmFCmC9rj09YjCxi5i6t-kC/view?usp=drive_link) 

---

### BUG 11 - Mensagem de erro genérica no processo de login

**Descrição:** Foram realizados os testes de autenticação com credenciais inválidas, com o objetivo de verificar se o sistema apresenta mensagens de erro claras e informativas quando ocorre falha no processo de login.

**Passos para reproduzir:**
1. Acessar a tela de login.
2. Informar um e-mail já cadastrado no sistema.
3. Informar a senha inexistente ou deixar o campo senha em branco.
4. Clicar no botão "Entrar".

**Resultado atual:** Nos cenários testados, o sistema exibe apenas a mensagem genérica **"Conta não encontrada. Crie uma conta primeiro."**, sem indicar claramente o motivo da falha no login.

**Resultado esperado:** O sistema deve exibir mensagens claras e apropriadas ao contexto da falha de autenticação. Em casos de credenciais incorretas, pode ser exibida uma mensagem neutra como `E-mail ou senha inválidos`. Quando o e-mail não estiver cadastrado, o sistema pode orientar o usuário com a mensagem `Conta não encontrada. Crie uma conta primeiro`. Mensagens claras ajudam a evitar tentativas repetidas de acesso, frustração do usuário e aumento na demanda por suporte.

**Severidade:** Média  
**Prioridade:** Média\
**Evidência:** [Mensagem de erro genérica](https://drive.google.com/file/d/19emn0ffEoaSyeYbDUywUZAqlSd_ncNRr/view?usp=drive_link) 

---

### BUG 12 - Exibição simultânea de mensagem de sucesso e erro inesperado após login válido   

**Descrição:** Foram realizados os testes de autenticação com credenciais válidas, com o objetivo de verificar o comportamento do sistema após a realização de um login bem-sucedido.

**Passos para reproduzir:**
1. Acessar a tela de login.
2. Informar um e-mail já cadastrado no sistema.
3. Informar a senha correspondente.
4. Clicar no botão "Entrar".

**Resultado atual:** Nos cenários testados, o sistema exibiu simultaneamente uma mensagem de sucesso no login e um alerta informando `Erro inesperado`.

**Resultado esperado:** Quando o login for realizado com sucesso, o sistema deve exibir apenas a confirmação de autenticação bem-sucedida e seguir o fluxo normal da aplicação, redirecionando o usuário para a próxima tela. A exibição simultânea de mensagens de sucesso e erro gera ambiguidade na comunicação com o usuário, podendo causar confusão sobre o estado real da autenticação e transmitir a percepção de instabilidade ou falha no sistema.

**Severidade:** Alta  
**Prioridade:** Alta\
**Evidência:** [Exibição simultânea de mensagem](https://drive.google.com/file/d/17IUxBwP_WTXdp9U5SoVUDSB6sOHKHnXj/view?usp=drive_link) 

---

### BUG 13 – Exibição incorreta de regra de criação de senha na tela de login  

**Descrição:** Foi realizada a análise da interface da tela de login com o objetivo de verificar a consistência das mensagens e orientações apresentadas ao usuário durante o processo de autenticação.

**Passos para reproduzir:**
1. Acessar a tela de login da aplicação.
2. Observar o texto exibido abaixo do campo Senha.

**Resultado atual:** No cenário observado, a tela de login exibe a mensagem `A senha precisa ter no mínimo 8 caracteres e 1 caractere especial.`, que corresponde a regras de criação de senha utilizadas em fluxos de cadastro ou redefinição de senha.

**Resultado esperado:** A tela de login não deve exibir regras relacionadas à criação de senha. Em vez disso, a interface deve apresentar orientações adequadas ao processo de autenticação, como a opção `Esqueceu a senha?`, permitindo ao usuário acessar o fluxo de recuperação ou redefinição de senha. A presença de mensagens inadequadas pode gerar confusão na interface e prejudicar a experiência do usuário durante o acesso ao sistema.

**Severidade:** Baixa  
**Prioridade:** Baixa\
**Evidência:** [Exibição incorreta de regra de criação](https://drive.google.com/file/d/1k4655IMAEC4P1uelZYUs01Vui0K5S2o5/view?usp=sharing) 

---

## 🛠️ Problemas Gerais

### BUG 14 - Problemas de responsividade em viewport mobile na aplicação  

**Descrição:** Foi realizada a análise da interface da aplicação em viewport mobile, com o objetivo de verificar o comportamento responsivo das telas em dispositivos móveis.

**Passos para reproduzir:**
1. Abrir o sistema em viewport mobile (simulando um dispositivo móvel no navegador).
2. Navegar pelas telas da aplicação (login, cadastro e sucesso).
3. Observar a disposição e o comportamento dos elementos da interface.

**Resultado atual:** Nos cenários observados, o layout apresenta inconsistências no posicionamento e dimensionamento de alguns elementos da interface, provocando overflow horizontal (parte do conteúdo sai da tela).

**Resultado esperado:** Os elementos da interface devem se ajustar corretamente ao tamanho da tela em dispositivos móveis, mantendo alinhamento, proporção adequada e organização visual consistente. Problemas de responsividade podem prejudicar a navegação e dificultar a interação com os elementos da interface, impactando negativamente a experiência do usuário.

**Severidade:** Média  
**Prioridade:** Média\
**Evidência:** [Responsividade em viewport mobile](https://drive.google.com/file/d/1arJvGQaK4BwVtF__uSWPIFItW7r2OV3A/view?usp=sharing) 

---

## 🎯 Quais 2 bugs eu corrigiria primeiro e por quê?  

Considerando o impacto funcional, os riscos de segurança e a integridade dos dados da aplicação, os dois bugs priorizados para correção imediata são aqueles que afetam diretamente os fluxos críticos do sistema: cadastro de usuários e autenticação.

### 1) BUG 01 — Ausência total de dados na submissão do cadastro

Este bug deve ser corrigido primeiro porque compromete a integridade dos dados logo na origem. 
Ao permitir o cadastro de usuários sem nenhum dado preenchido, o sistema passa a aceitar registros inválidos na base de dados, o que pode impactar funcionalidades essenciais como autenticação, recuperação de senha e comunicação com o usuário.

### 2) BUG 09 - Permissão de login com e-mail e senha vazios após cadastro inconsistente 

Este bug deve ser priorizado em seguida porque compromete diretamente o controle de acesso da aplicação. 
Permitir login sem credenciais válidas representa uma falha crítica no mecanismo de autenticação e um risco de segurança significativo, pois possibilita acesso indevido ao sistema. Esse comportamento quebra uma regra fundamental de autenticação da aplicação.

---

## 💡 Sugestões de melhorias para as telas

### Tela de cadastro

**Melhorias funcionais**
- Garantir a validação obrigatória dos campos antes do envio do formulário.
- Validar o formato de e-mail e telefone tanto no front-end quanto no back-end.
- Validar os critérios mínimos de segurança para senha, com mensagens claras sobre os requisitos.
- Garantir a verificação de igualdade entre os campos senha e confirmação de senha.
- Impedir o envio do formulário quando houver campos obrigatórios não preenchidos ou dados inconsistentes.

**Melhorias de experiência do usuário**
- Indicar visualmente os campos obrigatórios utilizando o símbolo (*) ao lado do rótulo do campo.
- Exibir uma legenda indicando que (*) representa campo obrigatório.
- Destacar visualmente os campos inválidos durante o preenchimento.
- Exibir mensagens de erro claras e contextualizadas para cada campo.

---

### Tela de login

**Melhorias funcionais**
- Disponibilizar uma funcionalidade de recuperação de senha na própria tela de login, permitindo que o usuário redefina sua senha de forma segura caso a esqueça.
- Garantir validações no servidor para impedir autenticação com credenciais vazias ou inválidas.

**Melhorias de experiência do usuário**
- Exibir mensagens de erro mais claras e contextualizadas durante o processo de autenticação.
- Destacar visualmente os campos inválidos quando houver erro no preenchimento.
- Evitar a exibição de alertas contraditórios no mesmo fluxo de interação.

---

### Problemas gerais da aplicação

**Melhorias de experiência do usuário**
- Ajustar o layout em dispositivos móveis para evitar quebras visuais e rolagem desnecessária.
- Melhorar o aproveitamento do espaço vertical nas telas de login e cadastro em desktop, reduzindo espaçamentos excessivos quando o conteúdo puder ser exibido na área visível da página.

---

### Melhorias técnicas
- Criar identificadores estáveis nos elementos da interface, preferencialmente utilizando `data-testid`, ou alternativamente `id` ou `name`, para facilitar a automação de testes e a manutenção dos seletores. A ausência desses identificadores obriga o uso de seletores frágeis baseados em classes ou na estrutura do DOM, o que pode causar falhas quando ocorrem alterações no HTML ou no layout, além de dificultar integrações e a manutenção do sistema.
- Padronizar o tratamento de erros entre front-end e back-end.
- Adicionar testes automatizados para cenários positivos, negativos e casos de borda.

---

## Resumo Geral
O sistema apresenta falhas relevantes em três frentes principais:
1. **Validação de dados:** cadastro e login aceitam entradas inválidas ou vazias.
2. **Confiabilidade do fluxo:** há comportamento contraditório no login com sucesso e erro simultâneos.
3. **Experiência e qualidade técnica:** problemas de responsividade, mensagens pouco úteis e dificuldade de automação devido à ausência de identificadores estáveis nos elementos da interface.
