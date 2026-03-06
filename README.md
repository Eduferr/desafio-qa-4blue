# Teste Técnico - QA Tester - 4blue

## Contexto
Este documento foi elaborado com base na tarefa descrita no PDF do teste técnico da 4blue, que solicita a exploração livre do microssistema, identificação de bugs, classificação por severidade e prioridade, além da indicação dos dois bugs que deveriam ser corrigidos primeiro e sugestões de melhoria.

**Sistema avaliado:** `https://qa-play-sim.lovable.app/`  
**Escopo informado no teste:** Tela de Login, Tela de Criação de Conta e Tela simples de Sucesso.

---

## Estratégia de análise
A análise considerou:
- comportamento funcional das telas de login e cadastro;
- validações de campos obrigatórios e formato;
- mensagens de erro e sucesso;
- consistência visual em viewport mobile;
- riscos básicos de segurança;
- observações de testabilidade para futura automação.

---

## Bugs encontrados

### BUG 01 - Sistema permite cadastrar usuário com todos os campos vazios
**Descrição:** Na tela de cadastro, é possível submeter o formulário sem preencher nome, telefone, e-mail, senha e confirmação de senha.

**Passos para reproduzir:**
1. Acessar a tela de cadastro (Criar conta).
2. Deixar todos os campos em branco.
3. Clicar no botão de cadastro.

**Resultado atual:** O sistema aceita o cadastro mesmo com todos os campos vazios.

**Resultado esperado:** O sistema deve impedir o cadastro e exibir validações por campo, informando que os campos obrigatórios não foram preenchidos.

**Severidade:** Crítico  
**Prioridade:** Alta

---

### BUG 02 - Sistema permite cadastro com preenchimento parcial
**Descrição:** O formulário de cadastro aceita submissão mesmo quando apenas um dos campos é informado.

**Passos para reproduzir:**
1. Acessar a tela de cadastro (Criar conta).
2. Preencher apenas um dos campos, como nome ou e-mail.
3. Clicar em cadastrar.

**Resultado atual:** O sistema permite concluir o cadastro com dados incompletos.

**Resultado esperado:** O sistema deve exigir o preenchimento completo de todos os campos obrigatórios antes de permitir o cadastro.

**Severidade:** Crítico  
**Prioridade:** Alta

---

### BUG 03 - Campo de e-mail não valida formato na tela de cadastro
**Descrição:** O campo de e-mail apresenta máscara ou expectativa visual de estrutura, porém não valida formatos inválidos.

**Passos para reproduzir:**
1. Acessar a tela de cadastro (Criar conta).
2. Informar um e-mail inválido, como `teste`, `teste@` ou `teste.com`.
3. Preencher os demais campos conforme necessário.
4. Enviar o formulário.

**Resultado atual:** O sistema aceita o cadastro com e-mail em formato inválido.

**Resultado esperado:** O sistema deve validar o padrão do e-mail e impedir o cadastro enquanto o valor estiver fora do formato esperado.

**Severidade:** Alto  
**Prioridade:** Alta

---

### BUG 04 - Campo de telefone não valida formato na tela de cadastro
**Descrição:** Embora exista máscara visual para telefone, não há validação efetiva do conteúdo informado.

**Passos para reproduzir:**
1. Acessar a tela de cadastro (Criar conta).
2. Informar telefone incompleto ou inválido.
3. Enviar o formulário.

**Resultado atual:** O sistema aceita números fora do formato esperado.

**Resultado esperado:** O sistema deve validar quantidade de dígitos e estrutura do telefone antes de concluir o cadastro.

**Severidade:** Médio  
**Prioridade:** Média

---

### BUG 05 - Campos senha e confirmar senha não validam igualdade
**Descrição:** O sistema não garante que os campos de senha e confirmação possuam exatamente o mesmo valor.

**Passos para reproduzir:**
1. Acessar a tela de cadastro (Criar conta).
2. Preencher senha com um valor.
3. Preencher confirmação com valor diferente.
4. Enviar o formulário.

**Resultado atual:** O sistema permite prosseguir mesmo com divergência entre senha e confirmação.

**Resultado esperado:** O sistema deve bloquear o cadastro e informar que os campos precisam ser idênticos.

**Severidade:** Alto  
**Prioridade:** Alta

---

### BUG 06 - Campos de senha não validam critérios mínimos
**Descrição:** Os campos de senha não validam as regras apresentadas ou esperadas, como mínimo de 8 caracteres e pelo menos 1 caractere especial.

**Passos para reproduzir:**
1. Acessar a tela de cadastro (Criar conta).
2. Informar senha curta ou sem caractere especial.
3. Confirmar a senha.
4. Enviar o formulário.

**Resultado atual:** O sistema aceita senhas fora do critério mínimo.

**Resultado esperado:** O sistema deve rejeitar senhas que não atendam aos critérios definidos e exibir mensagem clara ao usuário.

**Severidade:** Alto  
**Prioridade:** Alta

---

### BUG 07 - Sistema permite login com e-mail e senha vazios após cadastro inconsistente
**Descrição:** Após a criação de usuário inválido com campos vazios, o sistema passa a permitir autenticação com e-mail e senha em branco.

**Passos para reproduzir:**
1. Realizar cadastro com campos vazios.
2. Acessar a tela de login.
3. Deixar e-mail e senha em branco.
4. Clicar em entrar.

**Resultado atual:** O sistema autentica o usuário com credenciais vazias.

**Resultado esperado:** O sistema deve bloquear a autenticação sem credenciais válidas e impedir que registros inválidos sejam utilizados para login.

**Severidade:** Crítico  
**Prioridade:** Alta

---

### BUG 08 - Campo de e-mail não valida formato na tela de login
**Descrição:** Na tela de login, o campo de e-mail não impede o envio de valores em formato inválido.

**Passos para reproduzir:**
1. Acessar a tela de login.
2. Informar um e-mail inválido.
3. Informar qualquer senha.
4. Clicar em entrar.

**Resultado atual:** O sistema processa a tentativa sem validação de formato.

**Resultado esperado:** O sistema deve validar o padrão do e-mail antes de enviar a tentativa de autenticação.

**Severidade:** Médio  
**Prioridade:** Média

---

### BUG 09 - Mensagem de erro de login é genérica e não orienta adequadamente o usuário
**Descrição:** Ao tentar autenticar, a mensagem exibida é genérica: "Conta não encontrada. Crie uma conta primeiro." Isso dificulta entender se o problema está no e-mail inexistente, na senha incorreta ou em outro cenário.

**Passos para reproduzir:**
1. Acessar a tela de login.
2. Informar credenciais inválidas ou parcialmente incorretas.
3. Clicar em entrar.

**Resultado atual:** O sistema exibe mensagem genérica, sem boa orientação do problema.

**Resultado esperado:** O sistema deve exibir retorno consistente e útil, sem ambiguidade excessiva, mantendo equilíbrio entre usabilidade e segurança.

**Severidade:** Médio  
**Prioridade:** Média

---

### BUG 10 - Login válido exibe simultaneamente mensagem de sucesso e alerta de erro inesperado
**Descrição:** Ao realizar login com credenciais válidas, o sistema apresenta mensagem de sucesso, porém também exibe um alerta de "Erro inesperado".

**Passos para reproduzir:**
1. Cadastrar um usuário válido.
2. Acessar a tela de login.
3. Informar e-mail e senha válidos.
4. Clicar em entrar.

**Resultado atual:** O sistema sinaliza sucesso e erro ao mesmo tempo.

**Resultado esperado:** Em caso de autenticação bem-sucedida, apenas a mensagem de sucesso deve ser exibida, seguida do fluxo esperado de navegação.

**Severidade:** Alto  
**Prioridade:** Alta

---

### BUG 11 - Problemas de responsividade em viewport mobile
**Descrição:** Há erro de responsividade recorrente nas telas mobile, com formulários excessivamente estendidos na vertical, elementos desconfigurados e barra de rolagem vertical desnecessária.

**Passos para reproduzir:**
1. Abrir o sistema em viewport mobile.
2. Acessar as telas de login e cadastro.
3. Observar a disposição visual dos componentes.

**Resultado atual:** O layout apresenta quebra visual, excesso de espaço vertical e experiência inconsistente em dispositivos móveis.

**Resultado esperado:** Os elementos devem se adaptar corretamente ao viewport mobile, sem deformações, sem desalinhamentos e sem rolagem desnecessária.

**Severidade:** Médio  
**Prioridade:** Média

---

### BUG 12 - Ausência de identificadores estáveis nos elementos prejudica a automação e manutenção
**Descrição:** Os elementos não estão identificados de forma consistente por atributos como `id`, `name` ou preferencialmente `data-testid`, o que dificulta automação, manutenção dos testes e rastreabilidade técnica.

**Passos para reproduzir:**
1. Inspecionar os elementos das telas no navegador.
2. Verificar os atributos disponíveis nos campos e botões.

**Resultado atual:** Os elementos não possuem identificadores estáveis suficientes para facilitar automação confiável.

**Resultado esperado:** Os componentes devem possuir identificadores consistentes e estáveis, preferencialmente específicos para teste.

**Severidade:** Baixo  
**Prioridade:** Média

---

## Quais 2 bugs eu corrigiria primeiro e por quê?
Conforme solicitado na tarefa, segue a priorização dos dois bugs mais críticos para correção imediata.

### 1) BUG 01 - Sistema permite cadastrar usuário com todos os campos vazios
Eu corrigiria este bug primeiro porque ele compromete a integridade do dado na origem. Quando o sistema aceita registros totalmente vazios, toda a cadeia seguinte fica contaminada: autenticação, consistência da base, experiência do usuário e confiabilidade do produto.

### 2) BUG 07 - Sistema permite login com e-mail e senha vazios após cadastro inconsistente
Este seria o segundo bug a ser corrigido porque representa a consequência mais grave do problema anterior: falha de autenticação com impacto direto em segurança e regra de negócio. Permitir login com credenciais vazias é uma quebra crítica do fluxo principal do sistema.

**Justificativa geral da ordem:**
Esses dois bugs afetam o núcleo do produto: cadastro e autenticação. Além do alto impacto funcional, geram risco de segurança, comprometem a credibilidade da aplicação e inviabilizam qualquer confiança mínima no fluxo principal do usuário.

---

## Sugestões de melhoria

### Melhorias funcionais
- Implementar validação obrigatória campo a campo antes do envio.
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

