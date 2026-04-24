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
