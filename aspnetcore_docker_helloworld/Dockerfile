FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["aspnetcore_docker_helloworld.csproj", "./"]
RUN dotnet restore "aspnetcore_docker_helloworld.csproj"
COPY . .
RUN dotnet build "aspnetcore_docker_helloworld.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "aspnetcore_docker_helloworld.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "aspnetcore_docker_helloworld.dll"]
