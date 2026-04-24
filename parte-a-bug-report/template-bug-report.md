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




