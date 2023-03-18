#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["BeautyShop/BeautyShop.csproj", "BeautyShop/"]
RUN dotnet restore "BeautyShop/BeautyShop.csproj"
COPY . .
WORKDIR "/src/BeautyShop"
RUN dotnet build "BeautyShop.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BeautyShop.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BeautyShop.dll"]