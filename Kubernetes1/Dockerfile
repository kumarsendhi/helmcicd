FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY ["Kubernetes1/Kubernetes1.csproj", "Kubernetes1/"]

RUN dotnet restore "$PROJECT_DIR/Kubernetes1.csproj"
COPY . .
WORKDIR "/src/Kubernetes1"
RUN dotnet build "Kubernetes1.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Kubernetes1.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Kubernetes1.dll"]