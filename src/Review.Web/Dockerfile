FROM mcr.microsoft.com/dotnet/sdk:5.0.103-alpine3.12 AS buid
WORKDIR /app
RUN dotnet --version

# Copiar csproj e restaurar dependecias
COPY *.csproj ./
COPY . .
EXPOSE 8282
RUN dotnet restore
COPY . ./
RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/aspnet:5.0-alpine3.12
WORKDIR /app
COPY --from=buid /app/out .
ENTRYPOINT ["dotnet", "Review.Web.dll"]