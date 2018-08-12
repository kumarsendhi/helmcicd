FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app

FROM microsoft/aspnetcore-build:2.0 AS build
COPY *.csproj ./
RUN dotnet restore

COPY . ./

RUN dotnet publish  -c Release -o out

FROM base AS final
WORKDIR /app
COPY  --from=build-env /app/out .
ENTRYPOINT ["dotnet", "Kubernetes1.dll"]