# C# Database/WinUi3 Cheat sheet 

Hier vind je een overzicht van de packages die je nodig hebt om te werken met een database in C# en WinUi3, zodat je geen 50 bladzijden moet lezen in Itslearning om te weten wat `Update-Database` is.


# Table of Contents <!-- omit in toc -->
- [Packages voor WinUi3](#packages-voor-winui3)
- [Project Setup](#project-setup)
- [Database Migraten](#database-migraten)

<br>
<br>

# Packages voor WinUi3
dit zijn alle packages die je nodig hebt om te werken met een database in C# en WinUi3.

> ### `Microsoft.EntityFrameworkCore.Tools`
> dit is om een nieuwe database te maken via de `Package Manager Console`

> ### `Pomelo.EntityFrameworkCore.MySql`
> dit is de `EntityFramework`. hiermee kan je calls naar je database maken om bijvoorbeeld data op te halen.

> ### `System.Text.Json`
> dit is om [`runtime-errors`](https://www.geeksforgeeks.org/dsa/runtime-errors/) te zien.


<br>
<br>


# Project Setup

>[!IMPORTANT] 
> Als je met WinUI3 werkt, moet je dit aan de bovenkant van je `<projectname>.csproj` plaatsen:
>```xml
><WindowsAppSdkDeploymentManagerInitialize>false</WindowsAppSdkDeploymentManagerInitialize>
>``` 

<br>

1. maak een mapje genaamt `Data`. Hier komt alles wat met de database te maken heeft.

2. Maak daarin een `AppDbContext.cs` aan met de volgende inhoud:

    ```csharp
    using Microsoft.EntityFrameworkCore;
    using System;

    namespace <projectname>.Data
    {
        public class AppDbContext : DbContext
        {
            protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
            {
                optionsBuilder.UseMySql(
                    @"server=localhost;port = 3306;
                      user = root;
                      password =;
                      database = databasename",
                    ServerVersion.Parse("10.4.17-mariadb")
                );
            }
        }
    }
    ```

3. Maak nu een model aan die je in je database wilt hebben. als vooorbeeld maken we `Car.cs` aan met de volgende inhoud:
    ```csharp
    using System;  

    namespace <projectname>.Data
    {
        internal class Car
        {
            public int Id { get; set; }
            public string Brand { get; set; }
            public string Model { get; set; }
            public DateTime Year { get; set; }
        }
    }
    ```

4. In `AppDbContext.cs` voeg je de nieuwe model toe. EfCore maak dit automatisch in een tabel.

    ```csharp
    public DbSet<Car> Cars { get; set; }
    ```

<br>

Dat was het. Nu kan je verder met het `Migraten` van je database.

<br>
<br>
<br>


# Database Migraten


### 1. Nieuwe Migration
Als je het voor het eerst aanmaakt, type je in de `Package Manager Console`:
```powershell
PM> Add-Migration Initial
```
anders type je een passend naam in.
```powershell
PM> Add-Migration "Add_Cars"
```
dit maakt een nieuwe mapje genaamt `Migrations` met een `202501010000_Initial.cs` bestand ( _of iets dat er op lijkt._)

<br>

### 2. Migration toevoegen

In de `Package Manager Console` type:
```powershell
PM> Update-Database
```
dit voegt de meest recente migration toe aan de database.

Als alles goed ging, staat er nu een nieuwe tabel in je database genaamd `Cars`.

<br>
