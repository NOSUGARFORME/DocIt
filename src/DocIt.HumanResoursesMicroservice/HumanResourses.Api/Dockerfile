FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["src/DocIt.HumanResoursesMicroservice/DocIt.HumanResourses.Api/DocIt.HumanResourses.Api.csproj", "src/DocIt.HumanResoursesMicroservice/DocIt.HumanResourses.Api/"]
RUN dotnet restore "src/DocIt.HumanResoursesMicroservice/DocIt.HumanResourses.Api/DocIt.HumanResourses.Api.csproj"
COPY . .
WORKDIR "/src/src/DocIt.HumanResoursesMicroservice/DocIt.HumanResourses.Api"
RUN dotnet build "DocIt.HumanResourses.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DocIt.HumanResourses.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DocIt.HumanResourses.Api.dll"]
