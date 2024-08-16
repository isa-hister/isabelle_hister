# isabelle_hister
Aula de engenharia de software

---
# 1. Descrição do sistema

Sistema para clínica veterinária.

Autora: Isabelle Hister dos Santos.

Nome da clínica veterinária: MiAu.

![https://github.com/isa-hister/isabelle_hister/blob/main/Shares%20are.png](https://github.com/isa-hister/isabelle_hister/blob/main/Shares%20are.png)

1. Uma clínica veterinária atende apenas os animais: gatos e cachorros. 
2. Os clientes devem fazer um cadastro de si e dos animais. 
3. Os clientes devem informar as condições nas quais os animais chegam. 
4. Os clientes devem informar o tipo de ração que o animal come. 
5. O cliente deve informar hábitos do animal. 
6. Para cada animal é possível que mais de um veterinário o atenda. 
7. Os animais podem chegar e serem atendidos de acordo com uma agenda do dia. 
8. Cada animal atendido receberá uma ficha e um prontuário. 
9. Outros dono podem querer marcar horários de atendimento futuro. 
10. O atendimento gera uma receita para o animal. 
11. Quando um cliente chega na clínica veterinária ele é atendido por um atendente. 
12. O atendente deve verificar se existe agenda disponível com um veterinário. 
13. O atendente deve colocar o cliente e seu animal na fila de espera, se for o caso. 
14. O atendente deve levar o cliente e o animal até o veterinário. 
15. O veterinário deve realizar uma entrevista com o dono do animal. 
16. O resultado da entrevista deve ir para um formulário. 
17. O veterinário deverá examinar o animal e anotar em prontuário(ficha) suas observações. 
18. Dependendo da situação do animal este receberá uma receita.
19. A clínica possui horário de funcionamento definido entre as 08h as 18h.
20. Após as 18h, é cobrado serviço de plantão.
21. A clínica possui veterinários especialistas em oftalmologia, cardiologia e obstetrícia.
22. A clínica possui petshop com serviço de banho e tosa.
23. A clínica aceitas as seguintes formas de pagamento: pix, cartão de débito e dinheiro.
24. O petshop vende ração.
25. O petshop vende roupas, camas e brinquedos.
26. A clínica atende planos de saúde pet.
27. A clínica vende vacinas e realiza as vacinações.

---
# 2. Diagrama do banco de dados

```mermaid
erDiagram
    CLIENTE {
        int id
        string nome
        string telefone
        string endereco
    }

    ANIMAL {
        int id
        string nome
        string especie
        string raca
        string idade
        string condicao
        string tipo_racao
        string habitos
    }

    VETERINARIO {
        int id
        string nome
        string especialidade
    }

    ATENDENTE {
        int id
        string nome
    }

    AGENDA {
        int id
        datetime data_hora
        int cliente_id
        int animal_id
        int veterinario_id
        string status
    }

    FICHA {
        int id
        int animal_id
        string observacoes
    }

    RECEITA {
        int id
        int ficha_id
        string descricao
    }

    CLIENTE ||--o{ ANIMAL : possui
    ANIMAL ||--o{ FICHA : possui
    FICHA ||--o{ RECEITA : gera
    ANIMAL ||--o{ AGENDA : tem
    CLIENTE ||--o{ AGENDA : agenda
    VETERINARIO ||--o{ AGENDA : atende
    ATENDENTE ||--o{ AGENDA : organiza
```

---
# 3. Diagrama de casos de uso

![https://github.com/isa-hister/isabelle_hister/blob/main/Diagrama%20sem%20nome.drawio.png](https://github.com/isa-hister/isabelle_hister/blob/main/Diagrama%20sem%20nome.drawio.png)

---
# 4. Principais telas do sistema

![https://github.com/isa-hister/isabelle_hister/blob/main/Imagem_banco.png](https://github.com/isa-hister/isabelle_hister/blob/main/Imagem_banco.png) ![https://github.com/isa-hister/isabelle_hister/blob/main/Imagem_script.png](https://github.com/isa-hister/isabelle_hister/blob/main/Imagem_script.png)
![https://github.com/isa-hister/isabelle_hister/blob/main/imagem_inicio.png](https://github.com/isa-hister/isabelle_hister/blob/main/imagem_inicio.png) ![https://github.com/isa-hister/isabelle_hister/blob/main/imagem_login.png](https://github.com/isa-hister/isabelle_hister/blob/main/imagem_login.png)
![https://github.com/isa-hister/isabelle_hister/blob/main/imagem_zip.png](https://github.com/isa-hister/isabelle_hister/blob/main/imagem_zip.png) ![https://github.com/isa-hister/isabelle_hister/blob/main/imagem_grafico.png](https://github.com/isa-hister/isabelle_hister/blob/main/imagem_grafico.png)
![https://github.com/isa-hister/isabelle_hister/blob/main/imagem_ficha.png](https://github.com/isa-hister/isabelle_hister/blob/main/imagem_ficha.png) ![https://github.com/isa-hister/isabelle_hister/blob/main/imagem_atendentes.png](https://github.com/isa-hister/isabelle_hister/blob/main/imagem_atendentes.png)

---
# 5. Arquitetura do sistema


```mermaid
graph TD;
    subgraph Clínica Veterinária
        direction TB

        Cliente -->|Cadastra-se| SistemaDeCadastro
        Cliente -->|Marca consulta| SistemaDeAgenda
        Cliente -->|Realiza pagamento| SistemaDePagamento

        Atendente -->|Verifica agenda| SistemaDeAgenda
        Atendente -->|Registra chegada| SistemaDeFilaDeEspera
        Atendente -->|Leva cliente e animal ao veterinário| SalaDeConsulta

        Veterinario -->|Realiza entrevista| SalaDeConsulta
        Veterinario -->|Examinar animal| SalaDeExame
        Veterinario -->|Preenche prontuário| SistemaDeProntuario
        Veterinario -->|Gera receita| SistemaDeReceita

        Petshop -->|Venda de produtos| SistemaDeVenda
        Petshop -->|Venda de vacinas| SistemaDeVacinas
        Petshop -->|Realiza vacinação| SalaDeVacina

        SistemaDeCadastro
        SistemaDeAgenda
        SistemaDePagamento
        SistemaDeFilaDeEspera
        SalaDeConsulta
        SalaDeExame
        SistemaDeProntuario
        SistemaDeReceita
        SistemaDeVenda
        SistemaDeVacinas
        SalaDeVacina

    end

    subgraph Sistemas Externos
        direction TB
        SistemaBancario
        PlanoDeSaudePet
    end

    SistemaDePagamento -->|Pix, Cartão de Débito, Dinheiro| SistemaBancario
    SistemaDeVenda -->|Ração, Roupas, Camas, Brinquedos| Cliente
    SistemaDeVacinas -->|Venda e vacinação| Cliente
    SistemaDePagamento -->|Planos de Saúde| PlanoDeSaudePet

    style SistemaBancario fill:#f9f,stroke:#333,stroke-width:2px;
    style PlanoDeSaudePet fill:#f9f,stroke:#333,stroke-width:2px;

    subgraph Infraestrutura da Clínica
        ServidorCadastro[(Servidor Cadastro)]
        ServidorAgenda[(Servidor Agenda)]
        ServidorPagamento[(Servidor Pagamento)]
        ServidorFilaDeEspera[(Servidor Fila de Espera)]
        ServidorProntuario[(Servidor Prontuário)]
        ServidorReceita[(Servidor Receita)]
        ServidorVenda[(Servidor Venda)]
        ServidorVacinas[(Servidor Vacinas)]

        SistemaDeCadastro --> ServidorCadastro
        SistemaDeAgenda --> ServidorAgenda
        SistemaDePagamento --> ServidorPagamento
        SistemaDeFilaDeEspera --> ServidorFilaDeEspera
        SistemaDeProntuario --> ServidorProntuario
        SistemaDeReceita --> ServidorReceita
        SistemaDeVenda --> ServidorVenda
        SistemaDeVacinas --> ServidorVacinas

    end

```

```mermaid
graph TD;
    ClientWeb -->|HTTP Request| ServidorWeb
    ServidorWeb -->|Executa| AplicacaoPHP
    AplicacaoPHP -->|Consulta/Atualiza| ServidorBD
    ServidorBD -->|Resposta de Dados| AplicacaoPHP
    AplicacaoPHP -->|HTTP Response| ServidorWeb
    ServidorWeb -->|HTTP Response| ClientWeb

    ClientWeb(Client Web)
    ServidorWeb[Servidor Web]
    AplicacaoPHP[Aplicação PHP]
    ServidorBD[(Servidor de Banco de Dados)]
    
    style ServidorWeb fill:#f9f,stroke:#333,stroke-width:2px;
    style AplicacaoPHP fill:#bbf,stroke:#333,stroke-width:2px;
    style ServidorBD fill:#bff,stroke:#333,stroke-width:2px;

```
___