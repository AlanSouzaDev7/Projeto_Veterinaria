# 🐾 Guia de Commits — Projeto Veterinária

> Como registrar cada mudança no sistema da clínica de forma clara, padronizada e fácil de acompanhar.

Este projeto adota o padrão **[Clean Commit](https://github.com/wgtechlabs/clean-commit)**: um jeito simples de escrever mensagens de commit usando **um emoji + um tipo + uma descrição curta**.

Assim como um prontuário bem preenchido conta a história de cada paciente, um histórico de commits bem escrito conta a história de cada parte do sistema. Qualquer pessoa da equipe deve conseguir abrir o histórico e entender **o que mudou, onde e por quê**, sem precisar abrir o código.

---

## 📑 Sumário

1. [Formato da mensagem](#-1-formato-da-mensagem)
2. [Os 9 tipos](#-2-os-9-tipos)
3. [Escopos do projeto](#-3-escopos-do-projeto)
4. [Regras de escrita](#-4-regras-de-escrita)
5. [Exemplos por módulo](#-5-exemplos-por-módulo)
6. [Certo x errado](#-6-certo-x-errado)
7. [Mudanças que quebram compatibilidade](#-7-mudanças-que-quebram-compatibilidade)
8. [Corpo e rodapé do commit](#-8-corpo-e-rodapé-do-commit)
9. [Fluxo de trabalho no projeto](#-9-fluxo-de-trabalho-no-projeto)
10. [Cola rápida](#-10-cola-rápida)

---

## 🩺 1. Formato da mensagem

```
<emoji> <tipo>: <descrição>
<emoji> <tipo> (<escopo>): <descrição>
```

| Parte | O que é | Exemplo |
|---|---|---|
| **emoji** | Identifica o tipo de relance | `📦` |
| **tipo** | A natureza da mudança | `new` |
| **escopo** | O módulo do sistema afetado (opcional, mas recomendado) | `(agenda)` |
| **descrição** | O que foi feito, em poucas palavras | `cadastro de consultas pela recepção` |

**Resultado:**

```
📦 new (agenda): cadastro de consultas pela recepção
```

---

## 💊 2. Os 9 tipos

| Emoji | Tipo | Quando usar | Na veterinária, por exemplo… |
|:---:|---|---|---|
| 📦 | `new` | Funcionalidade, arquivo ou recurso novo | Criar a tela de cadastro de pets |
| 🔧 | `update` | Mudança em algo que já existe: melhoria, refatoração ou correção de bug | Corrigir o cálculo da idade do animal |
| 🗑️ | `remove` | Remoção de código, arquivos, funções ou dependências | Tirar um campo que a clínica não usa mais |
| 🔒 | `security` | Correção de segurança ou vulnerabilidade | Impedir que a recepção veja dados financeiros |
| ⚙️ | `setup` | Configuração do projeto, CI/CD, ferramentas, build | Configurar a conexão com o banco de dados |
| ☕ | `chore` | Manutenção e arrumação, sem mudar comportamento | Atualizar versões de bibliotecas |
| 🧪 | `test` | Criar, alterar ou corrigir testes | Testar conflito de horário entre consultas |
| 📖 | `docs` | Documentação | Atualizar este guia ou o README |
| 🚀 | `release` | Lançamento de uma nova versão do sistema | Publicar a versão 1.0.0 |

> 💡 **Correção de bug:** o Clean Commit não tem um tipo `fix`. Bugs comuns entram como `🔧 update`. Se o bug for uma falha de segurança, use `🔒 security`.

---

## 🏥 3. Escopos do projeto

O escopo indica **em qual "setor da clínica"** a mudança aconteceu. Use sempre um destes nomes, em minúsculas e sem acento:

| Escopo | Módulo do sistema |
|---|---|
| `usuarios` | 👤 Cadastro de usuários e login |
| `permissoes` | 🔐 Perfis de acesso (administrador, veterinário, recepção) |
| `agenda` | 📅 Agendamentos de consultas e procedimentos |
| `horarios` | 🕒 Horários de funcionamento e escalas da equipe |
| `clientes` | 🧑 Tutores (donos dos animais) |
| `pacientes` | 🐶 Animais atendidos |
| `estoque` | 📦 Controle de materiais e medicamentos |
| `financeiro` | 💰 Pagamentos, cobranças e caixa |
| `relatorios` | 📊 Relatórios administrativos |
| `banco` | 🗄️ Tabelas, migrations e seeds |
| `interface` | 🎨 Layout, estilos e componentes visuais |
| `ci` | ⚙️ Automação de testes e deploy |

Se a mudança envolve vários módulos ao mesmo tempo, **omita o escopo**. Se aparecer um módulo novo, adicione-o a esta tabela no mesmo Pull Request.

---

## 📋 4. Regras de escrita

1. **Tipo sempre em minúsculas:** `new`, nunca `New` ou `NEW`.
2. **Verbo no presente ou descrição direta:** "adiciona alerta", "alerta de estoque baixo". Nunca "adicionei" ou "adicionado".
3. **Sem ponto final.**
4. **Máximo de 72 caracteres** na linha inteira, contando emoji, tipo e escopo.
5. **Descrição em português**, começando com letra minúscula. Os tipos continuam em inglês, como no padrão.
6. **Um commit, um assunto.** Se precisou usar "e" para descrever duas coisas diferentes, provavelmente são dois commits.
7. **Nada de mensagens vazias**, como "ajustes", "teste", "arrumando" ou "commit final".

---

## 🐕 5. Exemplos por módulo

**👤 Usuários e 🔐 permissões**
```
📦 new (usuarios): cadastro de funcionários pelo administrador
🔧 update (usuarios): exige senha com no mínimo 8 caracteres
🔒 security (permissoes): bloqueia acesso da recepção ao financeiro
```

**📅 Agenda e 🕒 horários**
```
📦 new (agenda): agendamento de consultas pela recepção
🔧 update (agenda): impede duas consultas no mesmo horário
📦 new (horarios): escala semanal dos veterinários
🔧 update (horarios): considera feriados no horário de funcionamento
```

**🧑 Clientes e 🐶 pacientes**
```
📦 new (clientes): cadastro de tutores com CPF e telefone
📦 new (pacientes): vínculo de vários animais ao mesmo tutor
🔧 update (pacientes): corrige cálculo da idade do animal
🗑️ remove (clientes): campo de fax do cadastro
```

**📦 Estoque**
```
📦 new (estoque): alerta de material com estoque baixo
🔧 update (estoque): busca de materiais por nome ou código
🔧 update (estoque): baixa automática de vacina após aplicação
```

**💰 Financeiro e 📊 relatórios**
```
📦 new (financeiro): registro de pagamento por PIX
📦 new (relatorios): relatório mensal de atendimentos
```

**⚙️ Infraestrutura, 🧪 testes e 📖 documentação**
```
⚙️ setup (banco): configura conexão com PostgreSQL
⚙️ setup (ci): roda testes automaticamente nos pull requests
☕ chore: atualiza dependências do projeto
🧪 test (agenda): cobre conflito de horário entre consultas
📖 docs: adiciona guia de commits
🚀 release: versão 1.0.0
```

---

## ⚖️ 6. Certo x errado

| ❌ Evite | ✅ Prefira | Por quê |
|---|---|---|
| `ajustes` | `🔧 update (agenda): corrige horário de término da consulta` | Diz o que mudou e onde |
| `📦 New: Cadastro de pets.` | `📦 new (pacientes): cadastro de pets` | Tipo minúsculo, sem ponto |
| `📦 new: adicionei a tela de estoque` | `📦 new (estoque): tela de controle de materiais` | Sem verbo no passado |
| `🔧 update: estoque, agenda e login` | Três commits separados, um por módulo | Um commit, um assunto |
| `fix: bug do cadastro` | `🔧 update (clientes): aceita CPF com pontuação` | Usa o tipo do padrão e descreve o problema |
| `📦 new (pacientes): cadastro de animais com nome, espécie, raça, idade, peso e foto` | `📦 new (pacientes): cadastro de animais` | Passou de 72 caracteres. Os detalhes vão no corpo |

---

## 🚨 7. Mudanças que quebram compatibilidade

Quando uma mudança obriga outras partes do sistema (ou outras pessoas da equipe) a se adaptarem, coloque um **`!`** colado ao tipo:

```
🔧 update!: separa tutores e pacientes em tabelas diferentes
🔒 security!: exige novo login de todos os usuários
```

O `!` só pode ser usado com `new`, `update`, `remove` e `security`. Sempre explique no corpo do commit o que precisa ser feito para se adaptar.

---

## 📝 8. Corpo e rodapé do commit

Para mudanças simples, a primeira linha basta. Quando houver algo importante a explicar, use o **corpo** (separado por uma linha em branco) e o **rodapé**:

```
🔧 update (agenda): impede duas consultas no mesmo horário

Antes era possível marcar dois animais com o mesmo veterinário
no mesmo horário. Agora o sistema verifica a agenda antes de
salvar e exibe a mensagem "Horário indisponível".

Closes #18
```

- **Corpo:** explica o *porquê* e o contexto, não repete o código.
- **Rodapé:** `Closes #número` fecha a tarefa ligada a este commit quando ele chegar à `main`.

---

## 🔄 9. Fluxo de trabalho no projeto

```
Tarefa (Issue)  →  Branch  →  Commits  →  Pull Request  →  Desenvolvimento → Homologação → main
```

1. **Tarefa:** toda mudança nasce de uma issue criada com o modelo **📌 Tarefa**.
2. **Branch:** criada a partir de `Desenvolvimento`, com o número da tarefa:
   - `feature/12-alerta-estoque-baixo` para coisas novas
   - `fix/15-calculo-idade-animal` para correções
3. **Commits:** seguindo este guia.
4. **Pull Request:** o **título do PR segue o mesmo formato** do Clean Commit, por exemplo `📦 new (estoque): alerta de material com estoque baixo`. A descrição usa o template de PR do projeto.
5. **Promoção:** `Desenvolvimento` → `Homologação` (validação pela clínica) → `main` (produção).

---

## 📌 10. Cola rápida

```
📦 new        coisa nova
🔧 update     mudança, melhoria ou correção
🗑️ remove     remoção
🔒 security   segurança
⚙️ setup      configuração e ferramentas
☕ chore      manutenção
🧪 test       testes
📖 docs       documentação
🚀 release    nova versão

Formato:  <emoji> <tipo> (<escopo>): <descrição>
Limite:   72 caracteres · minúsculas · sem ponto final
```

---

<sub>🐾 Baseado no padrão <a href="https://github.com/wgtechlabs/clean-commit">Clean Commit</a>, de Waren Gonzaga (WG Tech Labs), adaptado para o Projeto Veterinária.</sub>
