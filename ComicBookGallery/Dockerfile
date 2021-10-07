#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.
# syntax=docker/dockerfile:1
FROM amazonlinux:2 AS base

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["ComicBookGallery/ComicBookGallery.csproj", "ComicBookGallery/"]
RUN dotnet restore "ComicBookGallery/ComicBookGallery.csproj"
COPY . .
WORKDIR "/src/ComicBookGallery"
RUN dotnet build "ComicBookGallery.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ComicBookGallery.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ComicBookGallery.dll"]
