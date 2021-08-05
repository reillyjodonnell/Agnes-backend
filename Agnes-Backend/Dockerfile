#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["Agnes-Backend/Agnes-Backend.csproj", "Agnes-Backend/"]
RUN dotnet restore "Agnes-Backend/Agnes-Backend.csproj"
COPY . .
WORKDIR "/src/Agnes-Backend"
RUN dotnet build "Agnes-Backend.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Agnes-Backend.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Agnes-Backend.dll"]