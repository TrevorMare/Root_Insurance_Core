FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY GoogleDialogFlow.sln ./
COPY GoogleDialogFlow.API/GoogleDialogFlow.API.csproj GoogleDialogFlow.API/
COPY GoogleDialogFlow.API.Data/GoogleDialogFlow.API.Data.csproj GoogleDialogFlow.API.Data/
COPY GoogleDialogFlow.API.Core/GoogleDialogFlow.API.Core.csproj GoogleDialogFlow.API.Core/
RUN dotnet restore -nowarn:msb3202,nu1503
COPY . .
WORKDIR /src/GoogleDialogFlow.API
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "GoogleDialogFlow.API.dll"]
