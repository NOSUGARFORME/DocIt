FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["src/DocIt.TaskMicroservice/Task.Api/Task.Api.csproj", "src/DocIt.TaskMicroservice/Task.Api/"]
RUN dotnet restore "src/DocIt.TaskMicroservice/Task.Api/Task.Api.csproj"
COPY . .
WORKDIR "/src/src/DocIt.TaskMicroservice/Task.Api"
RUN dotnet build "Task.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Task.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Task.Api.dll"]
