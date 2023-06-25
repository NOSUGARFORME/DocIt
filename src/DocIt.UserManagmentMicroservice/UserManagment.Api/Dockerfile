FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["src/DocIt.UserManagmentMicroservice/UserManagment.Api/UserManagment.Api.csproj", "src/DocIt.UserManagmentMicroservice/UserManagment.Api/"]
RUN dotnet restore "src/DocIt.UserManagmentMicroservice/UserManagment.Api/UserManagment.Api.csproj"
COPY . .
WORKDIR "/src/src/DocIt.UserManagmentMicroservice/UserManagment.Api"
RUN dotnet build "UserManagment.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "UserManagment.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "UserManagment.Api.dll"]
