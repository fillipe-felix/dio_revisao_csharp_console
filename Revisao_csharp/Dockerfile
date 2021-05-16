FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Revisao_csharp/Revisao_csharp.csproj", "Revisao_csharp/"]
RUN dotnet restore "Revisao_csharp/Revisao_csharp.csproj"
COPY . .
WORKDIR "/src/Revisao_csharp"
RUN dotnet build "Revisao_csharp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Revisao_csharp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Revisao_csharp.dll"]
