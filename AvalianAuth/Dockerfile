#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-nanoserver-1809 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-nanoserver-1809  AS build
WORKDIR /src
COPY ["AvalianAuth/AvalianAuth.csproj", "AvalianAuth/"]
RUN dotnet restore "AvalianAuth/AvalianAuth.csproj"
COPY . .
WORKDIR "/src/AvalianAuth"
RUN dotnet build "AvalianAuth.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AvalianAuth.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AvalianAuth.dll"]