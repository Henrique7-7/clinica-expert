[backendfim.md](https://github.com/user-attachments/files/32340796/backendfim.md)

# Back-End — Clínica Expert

**Integrante:** Luis Henrique

**Papel escolhido:** Desenvolvimento Back-End

---

## Por que escolhi essa área

Escolhi back-end porque é a área que resolve o principal problema do projeto. O front-end monta as telas, mas quem decide se um agendamento pode ou não acontecer é o servidor. Achei interessante justamente por ser a parte que o usuário não vê, mas sem a qual nada funciona.

## O que faz esse profissional

O back-end cuida da parte "de trás" do sistema: a lógica que processa as informações, as regras que o sistema precisa seguir e o banco de dados onde tudo fica guardado.

Quando a recepção clica em "salvar agendamento", é o back-end que verifica se o horário está livre, se o médico atende aquela especialidade e se a clínica está aberta naquele dia. Só depois disso a informação é gravada.

Resumindo: o front-end mostra, o back-end decide.

## Principais responsabilidades

- Criar as regras do sistema (o que pode e o que não pode)
- Trabalhar junto com o banco de dados para gravar e buscar as informações
- Fazer a comunicação entre o banco e as telas do front-end
- Validar as informações antes de salvar
- Controlar quem pode fazer o quê no sistema
- Programar o envio automático dos lembretes
- Cuidar da segurança dos dados dos pacientes

## Conhecimentos importantes

- Uma linguagem de programação de servidor (Java, Python, Node.js, entre outras)
- Banco de dados e SQL
- Noções de API, que é o que liga o back-end ao front-end
- Noções de segurança e LGPD, já que o sistema lida com dados de saúde
- Git, para versionar o código com a equipe
- Atenção a detalhes e pensamento lógico, porque uma regra mal feita gera consulta duplicada

## O que eu entregaria no projeto

- A definição dos dados que o sistema precisa guardar, em conjunto com a área de banco de dados
- As regras de agendamento implementadas
- A API que conecta o sistema às telas
- O controle de acesso por tipo de usuário
- A rotina automática de lembretes
- Uma base com dados de teste para o João validar o sistema

## Como isso ajuda a resolver o problema da clínica

**Conflito de horário.** É a dor mais ligada ao back-end. No fluxo que apresentamos tem uma etapa chamada "sistema verifica disponibilidade" — essa etapa é o back-end. Antes de gravar, o sistema confere se o médico está livre naquele horário.

**Perda de informação.** Hoje os dados estão espalhados em telefone, mensagens e planilhas. O back-end junta tudo em um banco de dados único, com um código próprio para cada paciente, evitando cadastro duplicado.

**Paciente sem lembrete.** O lembrete não depende de ninguém clicar. É uma rotina que roda sozinha todo dia, procura as consultas do dia seguinte e dispara os avisos.

**Acompanhar os atendimentos.** Cada agendamento passa por etapas que o sistema controla, então a clínica consegue saber o que foi concluído, cancelado ou quem faltou.

## Regras que definimos para o sistema

1. Um médico não pode ter duas consultas no mesmo horário.
2. Um paciente não pode ter duas consultas no mesmo horário, mesmo em unidades diferentes.
3. A consulta só pode ser marcada se a especialidade do médico for a correta.
4. Só é possível agendar dentro do horário de funcionamento da clínica.
5. Só a recepção e a administração podem criar ou alterar agendamentos. O paciente apenas consulta, confirma e cancela o dele.
6. O lembrete é enviado 24h antes, uma única vez.
7. Ao cancelar, o horário fica livre de novo e fica registrado quem cancelou.
8. O atendimento precisa seguir as etapas na ordem, sem pular nenhuma.

## Etapas do agendamento

```
AGENDADO → CONFIRMADO → EM ATENDIMENTO → CONCLUÍDO
```

Podendo virar CANCELADO ou FALTA no meio do caminho.

O sistema não deixa pular etapa. Não dá para ir de "agendado" direto para "concluído". E cancelamento não volta atrás — se o paciente mudar de ideia, faz um agendamento novo.

## Decisões que tomamos

**A vaga continua reservada mesmo sem o paciente confirmar.** O lembrete serve para diminuir a falta, não para tirar a vaga de quem simplesmente não viu a mensagem.

**Não há prazo mínimo para cancelar.** O público da clínica popular lida com imprevisto de transporte e trabalho. Colocar regra rígida atrapalharia mais do que ajudaria.

**A falta é marcada pela recepção.** O sistema não tem como saber se o paciente apareceu ou não.

## Com quem eu preciso trabalhar

**Matheus (Requisitos)** — é dele que vêm as regras que eu implemento. Se o requisito estiver confuso, a regra sai errada.

**Victor (Front-end)** — a gente precisa combinar quais informações cada tela envia e recebe. Se a tela espera um dado que a API não manda, não funciona.

**Vinicius (Banco de Dados)** — é a área com quem eu trabalho mais de perto. Ele monta a estrutura das tabelas e eu escrevo o código que grava e busca essas informações. Se a estrutura do banco não previr, por exemplo, o horário de funcionamento da unidade, eu não consigo implementar a regra que impede agendamento fora do expediente.

**João (Testes)** — eu preparo os dados de teste e ele verifica se as regras estão funcionando, tipo "tentar agendar em horário ocupado tem que dar erro".

## O que aconteceria sem esse papel

O sistema teria telas bonitas e nada funcionando por trás. Na prática:

- Não existiria verificação de horário, e os conflitos continuariam como estão hoje
- Os dados não ficariam salvos de forma organizada
- Os lembretes teriam que ser enviados na mão
- As regras ficariam só no front-end, o que é inseguro
- Os dados dos pacientes ficariam desprotegidos

Sem back-end, a proposta vira só um desenho de telas.

## O que seria desenvolvido primeiro

Pensando na ordem do back-end:

1. **Cadastro de pacientes e profissionais** — sem isso não dá para agendar nada, então é a base de tudo.
2. **Agendamento com verificação de conflito** — é a dor principal da clínica, o que mais atrapalha hoje.
3. **Registro do atendimento** — para a clínica conseguir acompanhar o que foi feito.
4. **Lembretes automáticos** — importante, mas o sistema já funciona sem eles.
5. **Painel de acompanhamento** — os relatórios para a gestão vêm por último, porque dependem de já existir dado no sistema.

A lógica é começar pelo que sustenta o resto, depois resolver o problema maior, e deixar por último o que agrega valor mas não impede o sistema de funcionar.

## Limitações e cuidados

**Segurança acumulada no back-end.** Nossa equipe tem cinco pessoas e não tem ninguém dedicado à segurança da informação. Essa parte ficou comigo. Dá para fazer nesse trabalho, mas num projeto real seria um risco, porque exige conhecimento específico de LGPD e proteção de dados de saúde.

**Dependência entre back-end e banco de dados.** Como as duas áreas são muito próximas, qualquer mudança na estrutura das tabelas afeta meu código. Isso exige combinar bem as decisões com o Vinicius antes de implementar, senão um refaz o trabalho do outro.

**Dados de saúde.** O sistema lida com informação sensível, então precisa de acesso restrito por tipo de usuário e senha protegida. Só quem realmente precisa da informação deve conseguir acessar.

