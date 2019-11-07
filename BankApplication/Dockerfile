FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["BankApplication/BankApplication.csproj", "BankApplication/"]
RUN dotnet restore "BankApplication/BankApplication.csproj"
COPY . .
WORKDIR "/src/BankApplication"
RUN dotnet build "BankApplication.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "BankApplication.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "BankApplication.dll"]