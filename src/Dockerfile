FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env
WORKDIR /app

RUN apt-get update && \
    apt-get install -y nodejs npm

COPY . ./
RUN dotnet restore

WORKDIR /app/GC.WebReact

RUN npm install

RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build-env /app/GC.WebReact/out .

EXPOSE 80

ENTRYPOINT ["dotnet", "GC.WebReact.dll"]