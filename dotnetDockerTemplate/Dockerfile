FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app

#EXPOSE 80
EXPOSE 5000
ENV ASPNETCORE_URLS http://+:5000

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["dotnetDockerTemplate/dotnetDockerTemplate.csproj", "dotnetDockerTemplate/"]
RUN dotnet restore "dotnetDockerTemplate/dotnetDockerTemplate.csproj"
COPY . .
WORKDIR "/src/dotnetDockerTemplate"
RUN dotnet build "dotnetDockerTemplate.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dotnetDockerTemplate.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dotnetDockerTemplate.dll"]