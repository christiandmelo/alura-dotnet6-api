# Etapa 1: Construir a aplicação
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app

# Copiar os arquivos de projeto e restaurar as dependências
COPY ./*.csproj ./
RUN dotnet restore

# Copiar o código-fonte e compilar a aplicação
COPY . ./
RUN dotnet publish -c Release -o out

# Etapa 2: Executar a aplicação
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build /app/out .

# Definir variáveis de ambiente para o usuário, senha e endereço do banco de dados
ENV DB_USER=seu_usuario
ENV DB_PASSWORD=sua_senha
ENV DB_HOST=endereco_do_banco_de_dados

# Expor a porta da aplicação
EXPOSE 80

# Iniciar a aplicação quando o contêiner for iniciado
ENTRYPOINT ["dotnet", "FilmesApi.dll"]
