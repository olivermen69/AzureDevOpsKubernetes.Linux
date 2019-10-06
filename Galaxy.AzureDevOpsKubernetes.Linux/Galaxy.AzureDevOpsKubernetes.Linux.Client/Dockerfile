FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["Galaxy.AzureDevOpsKubernetes.Linux.Client/Galaxy.AzureDevOpsKubernetes.Linux.Client.csproj", "Galaxy.AzureDevOpsKubernetes.Linux.Client/"]
RUN dotnet restore "Galaxy.AzureDevOpsKubernetes.Linux.Client/Galaxy.AzureDevOpsKubernetes.Linux.Client.csproj"
COPY . .
WORKDIR "/src/Galaxy.AzureDevOpsKubernetes.Linux.Client"
RUN dotnet build "Galaxy.AzureDevOpsKubernetes.Linux.Client.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Galaxy.AzureDevOpsKubernetes.Linux.Client.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Galaxy.AzureDevOpsKubernetes.Linux.Client.dll"]
