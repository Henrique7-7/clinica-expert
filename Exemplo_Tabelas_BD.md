Algumas das tabelas que devem rodar no nosso projeto :

Tabbela Pacientes :
Responsável por centralizar o cadastro. É aqui que entram os cuidados práticos com a privacidade e a LGPD.

id_paciente (Primary Key): Identificador único de cada pessoa.

nome_completo: Nome do paciente.

cpf (Unique): Documento único (a regra unique impede que a mesma pessoa seja cadastrada duas vezes).

telefone: Dado essencial para que o sistema consiga enviar os lembretes de consulta.

data_nascimento: Para calcular a idade do paciente no momento do atendimento.


-------------------------------------------------------------------------------------------------------------------------------------------------------------------------


Tabela profissionais :

Organiza a equipe médica e os funcionários da clínica.

id_profissional (Primary Key): Identificador único.

nome_completo: Nome do médico.

especialidade: Área de atuação (ex: Cardiologia, Clínico Geral).

crm (Unique): Registro do conselho médico, garantindo que os dados do profissional sejam autênticos e não se repitam.


-------------------------------------------------------------------------------------------------------------------------------------------------------------------------


Tabela agendamentos :

Esta é a tabela crucial para o seu papel, pois é ela que elimina os conflitos de horários mencionados na sua postagem.

id_agendamento (Primary Key): Código da reserva.

id_paciente (Foreign Key): Referência ao paciente que vai ser atendido.

id_profissional (Foreign Key): Referência ao médico que fará o atendimento.

data_hora_consulta: O dia e o horário exato (ex: 2026-09-20 14:30:00).

status: Define o estado atual (ex: "Agendado", "Cancelado", "Concluído").


-------------------------------------------------------------------------------------------------------------------------------------------------------------------------


Tabela historico_atendimentos :

Resolve o problema da "perda de informações", criando um prontuário digital seguro.

id_atendimento (Primary Key): Código do registro médico.

id_agendamento (Foreign Key): Conecta o que foi conversado na sala à consulta que estava na agenda.

anotacoes_medicas: Onde o médico digita os sintomas, diagnósticos e prescrições.

data_registro: Carimbo de data e hora em que a ficha foi salva, para fins de auditoria.



