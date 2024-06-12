
## Autores

- [@danielPedroo](https://www.github.com/danielpedroo)

## Contribuindo

Olá pessoal, bem-vindos ao meu GitHub! É um prazer ter você aqui. Faça um fork, adapte o projeto ou estude e aprenda mais e mais :D <3

## Projeto/Finalidades

Este projeto é baseado na seção de desafios da [DIO](https://www.dio.me/) (Digital Innovation One). O projeto trilha-net-api-desafio-main está no repositório da [DIO - Trilha_API](https://github.com/digitalinnovationone/trilha-net-api-desafio) e possui todos os dados e soluções.

Este projeto demonstra meus conhecimentos em C# API - AVANADE, abordando as soluções requisitadas.

## Dicas

Este projeto foi refatorado no [Visual Studio Community 2022](https://visualstudio.microsoft.com/pt-br/downloads/). Alguns arquivos podem estar ausentes, mas isso não atrapalha a compilação e execução do projeto.

- **IDE**: Visual Studio Community 2022
- **Banco de dados**: SQL Server

**Observação**: Desligue/Suspenda seu antivírus durante o desenvolvimento do projeto. O projeto conta com um executável (.exe), no meu caso `TaskWeb.exe`, para compilar e iniciar o Swagger. Se optar por deixar o antivírus ligado, ele pode capturar o arquivo, resultando em erro de execução. Fique atento(a)!

## Observações

Aqui estão alguns tópicos sobre o desenvolvimento do projeto e seus entrelaços.

![Http EndPoint](https://miro.medium.com/v2/resize:fit:884/1*_aaLph_L70t0BozQpIon-A.png)

Esta é uma tabela de exemplos, baseada em um CRUD de usuários.

### Extensões do Entity Framework

Instale as extensões do Entity Framework via gerenciador de tarefas [Nuget](https://www.nuget.org/) via **terminal do desenvolvedor** da sua IDE com os comandos:

- `dotnet add package Microsoft.EntityFrameworkCore.Design`
- `dotnet add package Microsoft.EntityFrameworkCore.SqlServer`

Esses comandos trazem métodos para conectar ao banco de dados e gerar a tabela de migração. Se usar um banco diferente do SQL Server, ajuste o package, por exemplo:

- `dotnet add package Microsoft.EntityFrameworkCore.MySQL`

### Criando Conexão com o Banco de Dados

Utilizar o JSON:

- **appsettings.Development.json**: Utilizado para Testes/Desenvolvimento.
- **appsettings.json**: Utilizado para produção e/ou implantação no mundo real.

Exemplo de configuração de conexão no JSON:

```Json
"ConnectionStrings": {
  "ConnectionOffice": "Server=localhost\\sqlexpress;Initial Catalog=Agenda;Integrated Security=True;TrustServerCertificate=True;"
}
```
  
## Adicionar o serviço/conexão do banco de dados
  
   Este codigo e colocado na **Program** de seu projeto e abaixo deste comentario // Add services to the container. Este fara a sua conexão como banco de dados.

```Json
   builder.Services.AddDbContext<AgendaContextEF>(options =>
   options.UseSqlServer(builder.Configuration.GetConnectionString("ConnectionOffice")));
   
   builder.Services.AddDbContext<Banco de dados que sera adicionado>(options =>
   options.UseSqlServer(builder.Configuration.GetConnectionString(Nome da conexao do banco em formato de string no JSON)));
```

## Migration
	
- Mapeamento das classes para a tranformação de tabelas

  Todas as clases que estiver com o tipo **DbSet<Nome da classe>** nome do atributo {get; set;}. Se tornaram tabelas dentro do banco de dados.
	
  - `Ex: DbSet<Tasks> TaskHub {get; set;}`

	Comando para a criação da tabela: **dotnet-ef migrations add CreateTableContato**

- Obs: O ultimo dado **CreateTableContato** pode ser trocado pelo nome de sua preferência pois ele serve apenas como histotico de migração,
	
	Para setar o banco na sua aplicação utilize o comando: 
	 **dotnet ef database update**
	
	**Obs de erro**: Possivelmente e provavel que você tenha problema com 
	invariantCulture mediante a alguns parametros
	
	- 1° - Desabilite na sua solução se exister a função invariantCulture que esta em true, coleque em **false**
	
	- 2° - Verifique o Json appsettings, caso estiver algo como "CultureInfo": "pt-BR" <-- **Exclua**
	
	- 3° - Verifique o a string connection do json.Development, atualize desta forma: 
	
```Json
"ConnectionStrings": {
  "ConnectionOffice": "Server=localhost\\sqlexpress;Initial Catalog=Agenda;Integrated Security=True;TrustServerCertificate=True;"
}
```
