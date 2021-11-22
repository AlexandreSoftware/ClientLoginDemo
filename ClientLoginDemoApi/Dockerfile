FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["ClientLoginDemo/ClientLoginDemo.csproj", "ClientLoginDemo/"]
RUN dotnet restore "ClientLoginDemo/ClientLoginDemo.csproj"
COPY . .
WORKDIR "/src/ClientLoginDemo"
RUN dotnet build "ClientLoginDemo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ClientLoginDemo.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ClientLoginDemo.dll"]
