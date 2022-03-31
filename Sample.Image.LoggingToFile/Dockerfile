#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY Sample.Image.LoggingToFile/Sample.Image.LoggingToFile.csproj Sample.Image.LoggingToFile/
RUN dotnet restore "Sample.Image.LoggingToFile/Sample.Image.LoggingToFile.csproj"
COPY . .
WORKDIR "/src/Sample.Image.LoggingToFile"
RUN dotnet build "Sample.Image.LoggingToFile.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Sample.Image.LoggingToFile.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Sample.Image.LoggingToFile.dll"]
