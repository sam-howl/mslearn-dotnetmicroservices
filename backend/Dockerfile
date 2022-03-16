# Build Image
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
# Copy the file backend.csproj found locally to the /src directory that was just created
COPY backend.csproj .
RUN dotnet restore
# Copy everything in the local working directory to the image
COPY . .
RUN dotnet publish -c release -o /app
# Publish Image(?)
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
EXPOSE 80
EXPOSE 443
# Copy everything from the /app directory of the build image created above into the app directory of this image
COPY --from=build /app .
# Sets the entrypoint of this image to dotnet and passes backend.dll as an argument
ENTRYPOINT ["dotnet", "backend.dll"]