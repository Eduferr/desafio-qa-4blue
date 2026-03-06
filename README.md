# Teste Técnico - QA Tester - 4blue

## Contexto
Este documento foi elaborado com base na tarefa descrita no teste técnico da 4blue, que consiste na exploração livre de um microssistema composto pelas seguintes telas: login, criação de conta e tela de sucesso.

A partir dessa exploração, foram identificados bugs, inconsistências de interface e oportunidades de melhoria, que foram registrados e classificados conforme severidade e prioridade.

Além disso, o documento também apresenta a análise dos dois bugs considerados mais críticos para correção imediata, acompanhada de justificativas técnicas, bem como sugestões de melhoria relacionadas à usabilidade, validação de dados e qualidade geral da aplicação.

**Sistema avaliado:** `https://qa-play-sim.lovable.app/`  

---

## Estratégia de análise
A análise considerou:
- Comportamento funcional das telas de login e cadastro;
- Validações de campos obrigatórios e formato;
- Mensagens de erro e sucesso;
- Consistência visual em viewport mobile;
- Riscos básicos de segurança;
- Observações de testabilidade para futura automação.

---

# Bugs encontrados

## Tela de cadastro

### BUG 01 - Sistema permite cadastrar usuário com todos os campos vazios
**Descrição:** Na tela de cadastro, é possível submeter o formulário sem preencher nome, telefone, e-mail, senha e confirmação de senha.

**Passos para reproduzir:**
1. Acessar a tela de cadastro (Criar conta).
2. Deixar todos os campos em branco.
3. Clicar no botão de cadastro.

**Resultado atual:** O sistema aceita o cadastro mesmo com todos os campos vazios.

**Resultado esperado:** O sistema deve impedir o cadastro e exibir validações por campo, informando que os campos obrigatórios não foram preenchidos.

**Impacto:** A possibilidade de realizar um cadastro com todos os campos vazios compromete gravemente a integridade da base de dados e o funcionamento do sistema de autenticação. Esse comportamento permite a criação de registros inválidos, podendo gerar inconsistências em diversos fluxos da aplicação, como login, recuperação de conta e identificação de usuários, além de indicar ausência de validações básicas no processo de cadastro.

**Severidade:** Crítico  
**Prioridade:** Alta\
**Link_Reprodução:** [Bug01 - Vídeo](https://drive.google.com/file/d/1VjPqs_c17_RciTYtFVtGL7Nci5xVIeGz/view?usp=drive_link)

---

### BUG 02 - Sistema permite cadastro com preenchimento parcial
**Descrição:** O formulário de cadastro aceita submissão mesmo quando apenas um dos campos é informado.

**Passos para reproduzir:**
1. Acessar a tela de cadastro (Criar conta).
2. Preencher apenas um ou alguns dos campos do formulário (por exemplo: apenas nome ou apenas e-mail).
3. Deixar os demais campos obrigatórios em branco
4. Clicar em cadastrar.

**Resultado atual:** O sistema permite concluir o cadastro com dados incompletos.

**Resultado esperado:** O sistema deve exigir o preenchimento completo de todos os campos obrigatórios antes de permitir o cadastro.

**Impacto:** A possibilidade de concluir o cadastro com preenchimento parcial compromete a integridade e a consistência dos dados armazenados no sistema, permitindo a criação de contas incompletas ou inválidas. Esse comportamento pode afetar fluxos posteriores da aplicação, como autenticação, recuperação de senha, comunicação com o usuário e rastreabilidade de informações, além de indicar ausência de validação adequada dos campos obrigatórios no processo de cadastro.

**Severidade:** Crítico  
**Prioridade:** Alta\
**Link_Reprodução:** [Bug02 - Vídeo](https://drive.google.com/file/d/1ilkN8u6F06TOo5RpckThC35lClqwa3N1/view?usp=drive_link)

---

### BUG 03 - Campo de e-mail não valida formato
**Descrição:** O campo de e-mail apresenta máscara ou expectativa visual de estrutura, porém não valida formatos inválidos.

**Passos para reproduzir:**
1. Acessar a tela de cadastro (Criar conta).
2. Informar um e-mail inválido, como `teste`, `teste@` ou `teste.com`.
3. Preencher os demais campos conforme necessário, com dados válidos.
4. Enviar o formulário.

**Resultado atual:** O sistema aceita o cadastro com e-mail em formato inválido.

**Resultado esperado:** O sistema deve validar o padrão do e-mail e impedir o cadastro enquanto o valor estiver fora do formato esperado.

**Impacto:** A ausência de validação adequada do formato de e-mail permite o cadastro de usuários com endereços inválidos, comprometendo a integridade da base de dados e dificultando processos que dependem desse contato, como recuperação de senha, envio de notificações e comunicação com o usuário.

**Severidade:** Alto  
**Prioridade:** Alta\
**Link_Reprodução:** [Bug03 - Vídeo](https://drive.google.com/file/d/1il4u2jHXvLrALipwEjMPZhMjxHtdnsqU/view?usp=drive_link)

---

### BUG 04 - Campo de telefone não valida formato e caractere númerico
**Descrição:** Embora exista máscara visual para telefone, não há validação efetiva do conteúdo informado.

**Passos para reproduzir:**
1. Acessar a tela de cadastro (Criar conta).
2. Informar telefone incompleto ou inválido.
3. Preencher os demais campos conforme necessário, com dados válidos.
4. Enviar o formulário.

**Resultado atual:** O sistema aceita números fora do formato esperado.

**Resultado esperado:** O sistema deve validar quantidade de dígitos e estrutura do telefone antes de concluir o cadastro.

**Impacto:** A ausência de validação efetiva do campo de telefone permite o cadastro de dados inválidos ou incompletos, comprometendo a qualidade e a confiabilidade das informações armazenadas no sistema. Isso pode dificultar processos de contato, recuperação de conta, autenticação adicional e comunicação com o usuário, além de gerar inconsistências na base de dados.

**Severidade:** Médio  
**Prioridade:** Média\
**Link_Reprodução:** [Bug04 - Vídeo](https://drive.google.com/file/d/1tFQdsI3oBZ7L0NPSmTqHixFnO-CkiECl/view?usp=drive_link)

---

### BUG 05 - Campos senha e confirmar senha não validam igualdade
**Descrição:** O sistema não garante que os campos de senha e confirmação possuam exatamente o mesmo valor.

**Passos para reproduzir:**
1. Acessar a tela de cadastro (Criar conta).
2. Preencher senha com um valor.
3. Preencher confirmação com valor diferente.
4. Preencher os demais campos conforme necessário, com dados válidos.
5. Enviar o formulário.

**Resultado atual:** O sistema permite prosseguir mesmo com divergência entre senha e confirmação.

**Resultado esperado:** O sistema deve bloquear o cadastro e informar que os campos precisam ser idênticos.

**Impacto:** A ausência de validação entre os campos de senha e confirmação pode resultar na criação de contas com credenciais diferentes das pretendidas pelo usuário. Esse comportamento pode impedir futuros acessos à conta, gerar frustração durante o login e aumentar a demanda por suporte para recuperação de senha.

**Severidade:** Alto  
**Prioridade:** Alta\
**Link_Reprodução:** [Bug05 - Vídeo](https://drive.google.com/file/d/1Ce7h2TiAXbD37hwHHUmYd4AmX9tf6z45/view?usp=drive_link)

---

### BUG 06 - Campos de senha não validam critérios mínimos
**Descrição:** Os campos de senha não validam as regras apresentadas ou esperadas, como mínimo de 8 caracteres e pelo menos 1 caractere especial.

**Passos para reproduzir:**
1. Acessar a tela de cadastro (Criar conta).
2. Informar senha curta ou sem caractere especial.
3. Confirmar a senha.
4. Preencher os demais campos conforme necessário, com dados válidos.
5. Enviar o formulário.

**Resultado atual:** O sistema aceita senhas fora do critério mínimo.

**Resultado esperado:** O sistema deve rejeitar senhas que não atendam aos critérios definidos e exibir mensagem clara ao usuário.

**Impacto:** A falta de validação das regras de complexidade de senha viola boas práticas de segurança e pode resultar na criação de credenciais vulneráveis. Isso aumenta o risco de acessos indevidos, ataques de força bruta e comprometimento de contas de usuários, além de indicar falhas nas políticas de segurança da aplicação.

**Severidade:** Alto  
**Prioridade:** Alta

---

### BUG 07 - Campos do formulário ultrapassam o container 
**Descrição:** Na tela de cadastro, alguns campos do formulário, como **Telefone** e **Confirmar senha**, excedem os limites visuais do card principal, causando quebra de layout e desalinhamento entre os elementos da interface.

**Passos para reproduzir:**
1. Acessar a tela de cadastro.
2. Observar o posicionamento dos campos no formulário.
3. Verificar o alinhamento visual dos inputs em relação ao container principal.

**Resultado atual:** Alguns campos ultrapassam a área do card, ficando visualmente desalinhados e comprometendo a organização da interface.

**Resultado esperado:** Todos os campos devem permanecer contidos dentro do card, com largura, espaçamento e alinhamento consistentes, preservando a harmonia visual da tela.

**Impacto:** O problema compromete a consistência visual da interface e transmite sensação de baixa qualidade do produto. Além de prejudicar a experiência do usuário, pode dificultar a leitura, o preenchimento dos campos e a percepção de confiabilidade da aplicação, especialmente em fluxos sensíveis como cadastro.

**Severidade:** Médio  
**Prioridade:** Média\
**Link_Reprodução:** [Bug07 - Vídeo](https://drive.google.com/file/d/1sQRty8JUj0ZrA95FPyEnSjOfObIiX9A4/view?usp=drive_link)

---

### BUG 08 - Sistema permite cadastro com e-mail já existente

**Descrição:** O sistema não valida se o e-mail informado já está cadastrado na base de usuários, permitindo a criação de múltiplas contas com o mesmo endereço de e-mail.

**Passos para reproduzir:** 
1. Acessar a tela de cadastro (Criar conta).
2. Realizar um cadastro com um e-mail válido (exemplo: teste@email.com).
3. Após concluir o cadastro, acessar novamente a tela de criação de conta.
4. Tentar cadastrar um novo usuário utilizando o mesmo e-mail.

**Resultado atual:** O sistema permite concluir o cadastro utilizando um e-mail que já existe na base de usuários.

**Resultado esperado:** O sistema deve impedir o cadastro e exibir mensagem informando que o e-mail já está cadastrado, orientando o usuário a realizar login ou recuperar a senha.

**Impacto:** A ausência de validação de unicidade do e-mail pode gerar múltiplas contas associadas ao mesmo endereço, comprometendo a integridade da base de dados e causando inconsistências em fluxos como autenticação, recuperação de senha, comunicação com o usuário e controle de identidade. Além disso, pode gerar conflitos na gestão de contas e dificultar o suporte ao usuário.

**Severidade:** Alto
**Prioridade:** Alta\
**Link_Reprodução:** [Bug08 - Vídeo](https://drive.google.com/file/d/1kizlnLkKQBdAP0RiNhoP_MtjqDIyfgJo/view?usp=drive_link)

---

## Tela de Login

### BUG 09 - Sistema permite login com e-mail e senha vazios após cadastro inconsistente
**Descrição:** Após a criação de usuário inválido com e-mail e senha vazios, o sistema passa a permitir autenticação com e-mail e senha em branco.

**Passos para reproduzir:**
1. Realizar cadastro com campos vazios.
2. Acessar a tela de login.
3. Deixar e-mail e senha em branco.
4. Clicar em entrar.

**Resultado atual:** O sistema autentica o usuário com credenciais vazias.

**Resultado esperado:** O sistema deve bloquear a autenticação sem credenciais válidas e impedir que registros inválidos sejam utilizados para login.

**Impacto:** Trata-se de uma falha crítica de segurança, pois permite o bypass do mecanismo de autenticação, possibilitando acesso ao sistema sem credenciais válidas. Esse comportamento compromete diretamente a integridade do controle de acesso da aplicação, podendo permitir acessos não autorizados a funcionalidades e dados do sistema. Além disso, evidencia ausência de validações adequadas no lado do servidor (server-side), aumentando o risco de inconsistências na base de dados e uso indevido da plataforma.

**Severidade:** Crítico  
**Prioridade:** Alta\
**Link_Reprodução:** [Bug09 - Vídeo]()

---

### BUG 10 - Mensagem de erro de login é genérica
**Descrição:** Ao tentar autenticar, a mensagem exibida é genérica: "Conta não encontrada. Crie uma conta primeiro." Isso dificulta entender se o problema está no e-mail inexistente, na senha incorreta ou em outro cenário.

**Passos para reproduzir:**
1. Acessar a tela de login.
2. Informar credenciais inválidas ou parcialmente incorretas.
3. Clicar em entrar.

**Resultado atual:** O sistema exibe mensagem genérica, sem boa orientação do problema.

**Resultado esperado:** O sistema deve exibir retorno consistente e útil, sem ambiguidade excessiva, mantendo equilíbrio entre usabilidade e segurança.

**Impacto:** A mensagem de erro genérica reduz a clareza do feedback fornecido ao usuário durante o processo de autenticação, dificultando a identificação do real motivo da falha no login. Isso pode gerar frustração, tentativas repetidas de acesso, aumento na demanda por suporte técnico e menor eficiência no processo de correção ou recuperação de credenciais pelo usuário.

**Severidade:** Médio  
**Prioridade:** Média\
**Link_Reprodução:** [Bug10 - Vídeo](https://drive.google.com/file/d/1AKVxkl10M2X586W5C5xzce6ndV76s6mx/view?usp=drive_link)

---

### BUG 11 - Login válido exibe simultaneamente mensagem de sucesso e alerta de erro inesperado
**Descrição:** Ao realizar login com credenciais válidas, o sistema apresenta mensagem de sucesso, porém também exibe um alerta de "Erro inesperado".

**Passos para reproduzir:**
1. Cadastrar um usuário válido.
2. Acessar a tela de login.
3. Informar e-mail e senha válidos.
4. Clicar em entrar.

**Resultado atual:** O sistema sinaliza sucesso e erro ao mesmo tempo.

**Resultado esperado:** Em caso de autenticação bem-sucedida, apenas a mensagem de sucesso deve ser exibida, seguida do fluxo esperado de navegação.

**Impacto:** A exibição simultânea de mensagens de sucesso e erro gera inconsistência no feedback do sistema, comprometendo a confiabilidade da aplicação e causando confusão para o usuário. Esse comportamento pode levar o usuário a interpretar que o login falhou, mesmo quando a autenticação foi bem-sucedida, impactando negativamente a experiência de uso e a percepção de estabilidade do sistema.

**Severidade:** Alto  
**Prioridade:** Alta\
**Link_Reprodução:** [Bug11 - Vídeo](https://drive.google.com/file/d/17IUxBwP_WTXdp9U5SoVUDSB6sOHKHnXj/view?usp=drive_link)

---

### BUG 12 – Texto de validação de senha exibido incorretamente na tela de login

**Descrição:** Na tela de login, abaixo do campo de senha, é exibida a mensagem "A senha precisa ter no mínimo 8 caracteres e 1 caractere especial.". Esse texto refere-se às regras de criação de senha (fluxo de cadastro ou redefinição de senha) e não é aplicável ao processo de autenticação. Além disso, a tela de login não apresenta a opção "Esqueceu a senha?", que é uma funcionalidade comum para recuperação de acesso.

**Passos para reproduzir:**
1. Acessar a tela de login da aplicação.
2. Observar o texto exibido abaixo do campo Senha.

**Resultado atual:** A tela de login apresenta a mensagem: "A senha precisa ter no mínimo 8 caracteres e 1 caractere especial.". Esse texto corresponde à validação de criação de senha e não ao fluxo de login.

**Resultado esperado:** A tela de login deve apresentar a opção: "Esqueceu a senha?". Essa opção deve direcionar o usuário para o fluxo de recuperação ou redefinição de senha.

**Impacto:** Pode gerar confusão ao usuário, pois a mensagem exibida sugere uma validação de formato de senha que não se aplica ao processo de autenticação.

**Severidade:** Baixa
**Prioridade:** Baixa\
**Link_Reprodução:** [Bug12 - Imagem](https://drive.google.com/file/d/1k4655IMAEC4P1uelZYUs01Vui0K5S2o5/view?usp=drive_link)

---

## Problemas Gerais

### BUG 13 - Problemas de responsividade em viewport mobile
**Descrição:** Há erro de responsividade recorrente nas telas mobile, com formulários excessivamente estendidos na vertical, elementos desconfigurados e barra de rolagem vertical desnecessária.

**Passos para reproduzir:**
1. Abrir o sistema em viewport mobile.
2. Acessar as telas de login e cadastro.
3. Observar a disposição visual dos componentes.

**Resultado atual:** O layout apresenta quebra visual, excesso de espaço vertical e experiência inconsistente em dispositivos móveis.

**Resultado esperado:** Os elementos devem se adaptar corretamente ao viewport mobile, sem deformações, sem desalinhamentos e sem rolagem desnecessária.

**Impacto:** A falha de responsividade compromete a experiência de navegação em dispositivos móveis, dificultando a visualização e interação com os formulários. Considerando que grande parte dos acessos a sistemas web ocorre por smartphones, o problema pode impactar negativamente a usabilidade, a percepção de qualidade do produto e as taxas de conversão de usuários.

**Severidade:** Médio  
**Prioridade:** Média\
**Link_Reprodução:** [Bug13 - Vídeo](https://drive.google.com/file/d/1arJvGQaK4BwVtF__uSWPIFItW7r2OV3A/view?usp=drive_link)

---

### BUG 14 - Ausência de identificadores estáveis nos elementos prejudica a automação e manutenção
**Descrição:** Os elementos interativos das telas, especialmente os campos de entrada de dados do usuário e botões de ação, não possuem identificadores estáveis e específicos, como `id`, `name` ou `data-testid`. Na inspeção, observa-se que os campos dependem principalmente de atributos como `class`, `type` e `placeholder`, que não são ideais para automação confiável e rastreabilidade técnica.

**Passos para reproduzir:**
1. Acessar as telas de login e cadastro.
2. Inspecionar os campos e botões no navegador.
3. Verificar os atributos disponíveis nos elementos interativos.

**Resultado atual:** Os elementos não possuem identificadores estáveis suficientes para facilitar automação confiável.

**Resultado esperado:** Os componentes interativos devem possuir identificadores únicos, consistentes e estáveis, preferencialmente `data-testid`, ou alternativamente `id/name`, para permitir automação confiável, manutenção simplificada e melhor rastreabilidade técnica.

**Impacto:** Sem identificadores estáveis (id, name, data-testid), os testes acabam usando seletores frágeis como: :nth-child(), classes visuais e hierarquia do DOM. Qualquer alteração de layout pode quebrar os testes mesmo sem mudança funcional.

**Severidade:** Baixo  
**Prioridade:** Média\
**Link_Reprodução:** [Bug14 - Imagem](https://drive.google.com/open?id=1u2untEkZj5Pgw5KFOrOuHKI2kkk8ws4b&usp=drive_copy)

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

