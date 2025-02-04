# Modelagem de dados  no Monitoramento de Ônibus

No terceiro módulo da capacitação em Desenvolvimento Full Stack do 
Programadores do Amanhã, fui desafiado a modelar um banco de dados 
para solucionar um problema real. Escolhi desenvolver um diário de 
viagens voltado ao sistema de transporte público de São Paulo, com o
objetivo de aprimorar o monitoramento das operações.

A motivação para essa solução surgiu a partir de problemas recorrentes 
enfrentados pela população: atrasos significativos nos itinerários dos ônibus, 
especialmente em paradas intermediárias. Em muitos casos, os usuários precisam 
esperar entre 40 minutos a 1 hora por um ônibus.

Diante desse cenário, desenvolvi um modelo de banco de dados capaz de armazenar 
informações sobre rotas, paradas, motoristas e veículos, além de registrar um 
histórico detalhado das viagens. Essa estrutura permite um controle mais preciso 
do transporte público, tornando possível a avaliação da eficiência operacional e 
a identificação de melhorias para o serviço.

## 🚏 Lógica de Negócio

No sistema de transporte público, a gestão eficiente das viagens depende do relacionamento 
estruturado entre **Rotas, Paradas, Motoristas e Veículos**. Para isso, as entidades são 
organizadas conforme suas regras de negócio e conexões lógicas.  

<br>

🔹 Entidades Principais: 

✔️ Motoristas 

✔️ Veículos 

✔️ Paradas 

✔️ Rotas 

<br>

🔹 Relacionamentos Estruturados:

✔️ Parada_Rota (tabela intermediária que define a sequência das paradas em cada rota) 

✔️ Diário de Viagem (registro detalhado das viagens realizadas) 

---

### 📍 Relação entre Rota e Parada  

As rotas de ônibus são compostas por múltiplas paradas ao longo do trajeto. Da mesma forma, 
uma mesma parada pode ser utilizada por diferentes rotas. Dessa forma, existe uma relação 
**muitos-para-muitos (N:M)** entre as entidades **Rota** e **Parada**.  

Para estruturar essa relação, é criada a entidade associativa **Rota_Parada**, que define 
quais paradas pertencem a cada rota e estabelece a **ordem** de passagem dos ônibus por cada ponto.  

#### 📌 Estrutura da Relação  

1. **Entidades Principais**  
   - **Rota** (`id_rota`, `nome`): Representa um trajeto específico de um ônibus.  
   - **Parada** (`id_parada`, `nome`): Representa um ponto onde os passageiros podem embarcar ou desembarcar.  

2. **Entidade Associativa – Rota_Parada**  
   - `id_rota` (Chave estrangeira de `Rota`)  
   - `id_parada` (Chave estrangeira de `Parada`)  
   - `ordem` (Define a posição da parada dentro da rota)  

Essa estrutura permite definir a sequência exata em que um ônibus percorre sua rota, garantindo 
uma organização eficiente das viagens.  

---

### 🚌 Relação entre Motorista e Veículo  

A operação do sistema de transporte também depende da correta associação entre **Motoristas e Veículos**. 
A regra de negócio determina que **os motoristas são registrados antes dos veículos**, e ao registrar um 
veículo, é obrigatório informar o motorista responsável.  

Essa relação segue um modelo **1:N (um para muitos)**, onde:  

- **Um motorista pode estar associado a múltiplos veículos ao longo do tempo.**  
- **Um veículo só pode ser registrado se houver um motorista atribuído.**  

#### 📌 Estrutura da Relação  

1. **Entidades Principais**  
   - **Motorista** (`id_motorista`, `nome`): Representa um condutor cadastrado no sistema.  
   - **Veículo** (`id_veiculo`, `placa`, `modelo`, `id_motorista`): Representa um veículo em operação, obrigatoriamente vinculado a um motorista.  

Isso garante que todos os veículos cadastrados tenham um responsável designado, enquanto os motoristas 
podem ser registrados previamente e alocados conforme a necessidade.  

---

### 📜 Histórico de Viagens  

Para monitorar e registrar as operações realizadas, o sistema utiliza a entidade **Historico_viagens**. 
Essa entidade associa os dados das rotas, paradas, veículos e horários, permitindo o acompanhamento 
detalhado das viagens realizadas.  

#### 📌 Estrutura da Relação  

1. **Entidades Associadas**  
   - **Historico_viagens**:  
     - Atributos: id, fk_Rota_Parada (Chave estrangeira de **Rota_Parada**), fk_Veiculo (Chave estrangeira 
      de **Veículo**), saida_partida, chegada_destino, criado_em.  

Essa estrutura permite registrar as viagens, com dados de horários e veículos, garantindo um 
controle eficiente do transporte público.  

### 🚀 Impacto  

Esperasse do modelo apresentado uma gestão eficiente do transporte público, organizando as rotas e 
paradas dos ônibus, além de garantir o correto registro e alocação de motoristas e veículos. 
Com esta modelagem, o sistema pode operar de forma estruturada, oferecendo um monitoramento 
preciso das viagens e garantindo a segurança e confiabilidade do serviço.