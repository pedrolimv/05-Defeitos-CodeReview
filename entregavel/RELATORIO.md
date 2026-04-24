# 📦 Relatório Final

> **Atividade:** Bug Report Profissional + Code Review Guiado
> **Curso:** Qualidade de Software
> **Professor:** Prof. Claudio Nunes

---

## 👥 Identificação da dupla

| Nome completo | RA | GitHub |
|---|---|---|
| Raoní Gullo Pereira Matheus | 230300 |
| Pedro Henrique de Lima Silva | 228022 | pedrolimv |
| Leonardo Polvineli Barga | 226225 | 

**Ambiente de testes:** 
Navegador: Chrome Versão 140.0.7339.186
Sistema Operacional: Windows 10
Versão da aplicação e testes parte A : TarefaQS v1.0.0


---

## 📋 Sumário

- [Parte A — Bug Reports](#parte-a--bug-reports)
- [Parte B — Code Review](#parte-b--code-review)
- [Reflexão final](#-reflexão-final)
- [Declarações](#-declarações)

---

## Parte A — Bug Reports

Trio : Raoní Matheus 230300 + Leonardo Povineli 226225 + Pedro Henrique Lima 228022 
Data da exploração: 23/04/2026  
Navegador usado: Google Chrome Versão 140.0.7339.186
Sistema operacional: Windows 10

BUG-001
Título: Sistema permite salvar tarefa vazia (sem título)

Severidade: Média

Justificativa da severidade: Permite entrada de dados inválidos, comprometendo a integridade das informações 

Prioridade: P2

Justificativa da prioridade: Afeta diretamente a qualidade dos dados, mas não impede o uso do sistema.

Ambiente:
Navegador: Chrome Versão 140.0.7339.186
Sistema Operacional: Windows 10
Versão da aplicação: TarefaQS v1.0.0

Passos para reprodução:
1.	Acesse a aplicação de testes 
2.	Clique no campo de adicionar tarefa 
3.	Deixe o campo vazio 
4.	Clique no botão de adicionar/salvar tarefa
   
Resultado esperado:
O sistema deve impedir a criação da tarefa e exibir uma mensagem de validação (ex: "Título é obrigatório").

Resultado obtido:
A tarefa é criada mesmo sem título.

Evidência:
<img width="886" height="223" alt="image" src="https://github.com/user-attachments/assets/cddb3e78-b343-439f-b4e8-d76010172cae" />

Sugestão de causa raiz (opcional):
Falta de validação de entrada antes de inserir a tarefa na lista.




BUG-002
Título: Lista de tarefas é perdida ao atualizar a página

Severidade: Alta

Justificativa da severidade: Perda de dados do usuário afeta diretamente a confiabilidade do sistema.

Prioridade: P1

Justificativa da prioridade: Impacta na usabilidade diária e mantenimento da ferramenta por parte do usuário.

Ambiente:
Navegador: Chrome Versão 140.0.7339.186
Sistema Operacional: Windows 10
Versão da aplicação: TarefaQS v1.0.0

Passos para reprodução:
1.	Adicionar uma ou mais tarefas 
2.	Confirmar que elas aparecem na lista 
3.	Atualizar a página (F5)
   
Resultado esperado:
As tarefas devem permanecer salvas após recarregar a página.

Resultado obtido:
Todas as tarefas desaparecem após o refresh.

Evidência:
antes: <img width="947" height="992" alt="image" src="https://github.com/user-attachments/assets/6dd850fa-607d-4b22-b6fa-535de22d1350" />

depois: <img width="949" height="1036" alt="image" src="https://github.com/user-attachments/assets/66d100c2-a8b3-4592-85cd-ef72f432ce0a" />





BUG-003
Título: Tarefa continua visível após ser marcada como concluída

Severidade: Média

Justificativa da severidade: A funcionalidade de conclusão não cumpre completamente seu propósito, causando inconsistência na gestão das tarefas.

Prioridade: P2

Justificativa da prioridade: Impacta uma funcionalidade central do sistema (controle de status das tarefas).

Ambiente:
Navegador: Chrome Versão 140.0.7339.186
Sistema Operacional: Windows 10
Versão da aplicação: TarefaQS v1.0.0

Passos para reprodução:
1.	Acesse a aplicação 
2.	Adicione uma nova tarefa 
3.	Marque a tarefa como concluída (checkbox ou botão equivalente) 
4.	Observe o comportamento da tarefa na lista
   
Resultado esperado:
Ao marcar como concluída, o sistema deveria:
•	Remover a tarefa da lista ativa OU 
•	Aplicar diferenciação clara (ex: riscado, mudança de cor, seção separada) 

Resultado obtido:
A tarefa permanece visualmente igual às demais, sem indicação clara de que foi concluída.

Evidência:
<img width="955" height="963" alt="image" src="https://github.com/user-attachments/assets/63fa5e36-4b9e-4aa2-8fa6-63c005fafed6" />



## Parte B — Code Review

Trio : Raoní Matheus 230300 + Leonardo Povineli 226225 + Pedro Henrique Lima 228022 
Data de revisão: 23/04/2026  

Finding #1

📍 Linha(s): ~14–16
🏷 Rótulo: blocker
📂 Dimensão: Segurança
⚠️ Severidade: Crítica

🐛 Problema:
A query SQL é construída por concatenação de string com entrada do usuário, permitindo SQL Injection.

💡 Sugestão de correção:

// ajuste sugerido
db.executarQuery(
  'SELECT * FROM usuarios WHERE nome = ?',
  [nome]
);




Finding #2

📍 Linha(s): ~3
🏷 Rótulo: nit
📂 Dimensão: Padrões
⚠️ Severidade: Baixa

🐛 Problema:
A constante TIPOS_VALIDOS é declarada, mas não é utilizada para validação em nenhum ponto do código.

💡 Sugestão de correção:

// ajuste sugerido
if (!TIPOS_VALIDOS.includes(dados.tipo)) {
  throw new Error('Tipo de usuário inválido');
}

📚 Referência (opcional): boas práticas de validação de entrada





Finding #3

📍 Linha(s): ~10–12, 27–38
🏷 Rótulo: major
📂 Dimensão: Erros
⚠️ Severidade: Média

🐛 Problema:
Funções async não possuem tratamento de erro (try/catch), o que pode resultar em falhas não tratadas.

💡 Sugestão de correção:

// ajuste sugerido
try {
  return await db.executarQuery('SELECT * FROM usuarios WHERE ativo = 1');
} catch (err) {
  logger.error(err);
  throw err;
}






Finding #4

📍 Linha(s): ~27–30
🏷 Rótulo: major
📂 Dimensão: Erros
⚠️ Severidade: Média

🐛 Problema:
O código assume que o usuário sempre existe após buscarPorId. Se retornar null, haverá erro ao acessar propriedades.

💡 Sugestão de correção:

// ajuste sugerido
if (!u) {
  throw new Error('Usuário não encontrado');
}





Finding #5

📍 Linha(s): ~14–16
🏷 Rótulo: major
📂 Dimensão: Segurança
⚠️ Severidade: Média

🐛 Problema:
A busca por usuário usa concatenação de string, enquanto outras queries usam abstração do banco, criando inconsistência e risco de segurança.

💡 Sugestão de correção:

// ajuste sugerido
db.executarQuery(
  'SELECT * FROM usuarios WHERE nome = ?',
  [nome]
);







Finding #6

📍 Linha(s): ~27–30
🏷 Rótulo: nit
📂 Dimensão: Legibilidade
⚠️ Severidade: Baixa

🐛 Problema:
Uso de variável pouco descritiva (u), dificultando leitura e manutenção.

💡 Sugestão de correção:

// ajuste sugerido
const usuario = await db.buscarPorId('usuarios', id);

### Resumo

| # | Linha         | Dimensão     | Rótulo  | Severidade |
| - | ------------- | ------------ | ------- | ---------- |
| 1 | ~14–16        | Segurança    | blocker | Crítica    |
| 2 | ~3            | Padrões      | nit     | Baixa      |
| 3 | ~10–12, 27–38 | Erros        | major   | Média      |
| 4 | ~27–30        | Erros        | major   | Média      |
| 5 | ~14–16        | Segurança    | major   | Média      |
| 6 | ~27–30        | Legibilidade | nit     | Baixa      |


## 💭 Reflexão final

> Responda em 1-2 parágrafos. Esta reflexão **é obrigatória**.

**Qual dimensão do checklist foi mais difícil aplicar? Por quê?**
 
A dimensão mais difícil de aplicar foi Segurança, principalmente ao identificar problemas que não geram erro imediato no funcionamento do código, como SQL Injection ou inconsistências no uso de queries parametrizadas. Esses problemas exigem uma análise mais profunda dos dados.


**O que vocês fariam diferente se revisassem o código novamente?**

Se fôssemos revisar o código novamente, provavelmente faríamos uma leitura mais estruturada desde o início, separando mentalmente cada dimensão do checklist (segurança, erros, padrões e legibilidade) antes de apontar os problemas. Também seria útil testar mentalmente cenários de uso e falha.

## 📣 Declarações

### Uso de IA como parceiro de trabalho

- [ ] Não usamos IA nesta atividade.
- [X] Usamos IA para esclarecer conceitos teóricos.
- [X] Usamos IA para revisar a redação dos bug reports.
- [ ] Usamos IA para discutir se um achado era ou não um defeito.
- [X] Uso específico: Utilizamos a IA em algumas sugestões de correções das findings detalhadas na parte B

### Declaração de autoria

Declaramos que este relatório é de autoria do trio, que exploramos
pessoalmente a aplicação da Parte A e lemos o código da Parte B. As
findings aqui registradas representam nosso próprio julgamento
técnico.
