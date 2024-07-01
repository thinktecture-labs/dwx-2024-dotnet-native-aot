# Native AOT with ASP.NET Core

This repo contains the slides and example code for Kenny Pflug's talk on Native AOT with ASP.NET Core. The talk was held at the DWX 2024 in Nuremburg, Germany.

## Prerequisites

You require the [.NET 8 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/8.0) for the code example. The code can run on multiple platforms and has been tested on Windows and Ubuntu. If you experience problems, please [create an issue](https://github.com/thinktecture-labs/dwx-2024-dotnet-native-aot/issues/new) in this repo.

## How to run the example code

### Example 1 - Memory, App Size, Startup Time

In the subfolder `MemoryAppSizeStartupTime`, you can find a minimal ASP.NET Core app which prints the startup time and memory footprint to the console. To run it, use the following commands:

```bash
# Make sure you are in the root folder of the repo
cd MemoryAppSizeStartupTime
dotnet publish -o bin/native-aot
cd bin/native-aot
./WebApp # append .exe on Windows
```

Alternatively, you can run the app in regular CLR mode:

```bash
# Make sure you are in the root folder of the repo
cd MemoryAppSizeStartupTime
dotnet run -c Release
```

For the different dockerfile, you can use `docker build -t <image-name> -f <target-file> .` to build the image and then compare their sizes.

### Example 2 - ASP.NET Core Web API with Native AOT

This web app represents a full example with ADO.NET data access, mediator pattern, Object-To-Object mapping.

To set up the database, run the following command:

```bash
# Make sure you are in the root folder of the repo
docker compose -f docker-compose.postgres-dev.yml up -d
```

Then, you can run the app:

```bash
# Make sure you are in the root folder of the repo
cd WebApp
dotnet publish -o bin/native-aot
cd bin/native-aot
./WebApp # append .exe on Windows
```

You can then use the `requests.http` file to call different Minimal API endpoints. .http files are supported out-of-the-box by Visual Studio, Visual Studio Code, and JetBrains Rider, amongst others.