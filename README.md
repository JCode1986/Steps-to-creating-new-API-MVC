# Starting from scratch
  * Create a new project and select `ASP.NET Core Web Application`
  * Choose empty
  * In `Startup.cs` in `ConfigureServices` method, add `services.AddMvc()` in code block.
  * In `Configure` method
  
  <strong>replace</strong>
  ```
  endpoints.MapGet("/", async context =>
{
    await context.Response.WriteAsync("Hello World!");
});
   ```
  <strong>with</strong>
   
   ```
   app.UseEndpoints(endpoints =>
{
    endpoints.MapControllerRoute("default", "{controllers=Home}/{action=Index}/{id?}");
});
```
* Create `Controllers`, `Data`, & `Models` folders in root of project
* Create your [models](https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/adding-model?view=aspnetcore-3.1&tabs=visual-studio) in `Models` folder
* In `appsettings.json` add connection string. Don't forget to change database name.
  * To be more secured, add user secrets by right clicking on your project and [Manager User Secrets](https://codefellows.github.io/code-401-dotnet-guide/Resources/UserSecrets.html). You can add your connection string in the newly populated file, and delete the appsettings.json.
```
"ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\MSSQLLocalDB;Database=DBNAMEHERE;Trusted_Connection=True;MultipleActiveResultSets=true"
  }
```
* Create a new class in the `Data` folder for your DbContext (i.e. EnterDBNameHereDbContext)
* Derive your new DbContext class from DbContext (i.e. EnterDBNameHereDbContext : DbContext) a. Make sure you bring in the namespace `Microsoft.EntityFrameworkCore`
* Create a new Constructor for your DbContext class, and require the DbContextOptions parameter and have that constructor derive from the base a. Example Constructor looks like this:
 ```
 public EnterDBNameHereDbContext(DbContextOptions<EnterDBNameHereDbContext> options) : base(options)
    {
	 
	}
 ```
* Go to `Startup.cs`
* Register DbContext in services. by add the following code inside configureServices() add the following code:(Change out the name of the Context for your DbContext, as well as the “DefaultConnection” with your DefualtConnection name found in your appsettings.json file.
```
services.AddDbContext<DemoClass13DbContext>(options =>
      options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));
```
* Setup our app to support dependency injection. We do this by adding a constructor to our startup class that requires IConfiguration. This is the code for that:
```
 public Startup(IConfiguration configuration)
  {
	    
  }
```
* Make sure to add `using Microsoft.Extensions.Configuration` and `using Microsoft.Extensions.DependencyInjection` libraries
* Open `Packager Manager Console` in the `tools` bar under `NuGet Package Manager` or on the bottom left tab.
* Add initial migration by typing `add-migration` with a message with no spaces (i.e. initial)
* Update database by typing `update-database`
* Now you can start adding tables in the `Data` folder under your `DbContext` file
	* `public DbSet<MODELNAME> TABLENAME {get; set;}`
* Always `add-migration` and `update-database` after a major change.
