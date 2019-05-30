FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["ApiPucCoins/ApiPucCoins.csproj", "ApiPucCoins/"]
RUN dotnet restore "ApiPucCoins/ApiPucCoins.csproj"
COPY . .
WORKDIR "/src/ApiPucCoins"
RUN dotnet build "ApiPucCoins.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ApiPucCoins.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ApiPucCoins.dll"]