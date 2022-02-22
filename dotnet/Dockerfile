#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.
#docker build -t dotnet-webapi -f Dockerfile .
#docker run -d -p 8080:80 --name dotnet-webapi-container dotnet-webapi

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["dotnet-webapi-test.csproj", "."]
RUN dotnet restore "./dotnet-webapi-test.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "dotnet-webapi-test.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dotnet-webapi-test.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dotnet-webapi-test.dll"]