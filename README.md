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
  * To be more secured, add user secrets by right clicking on your project and `add user secrets`. You can add your connection string in the newly populated file, and delete the appsettings.json.
```
"ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\MSSQLLocalDB;Database=DBNAMEHERE;Trusted_Connection=True;MultipleActiveResultSets=true"
  }
```
* Create a new class in the `Data` folder for your DbContext (i.e. <EnterDBNameHere>DbContext)
* Derive your new DbContext class from DbContext (i.e. <EnterDBNameHere>DbContext : DbContext) a. Make sure you bring in the namespace `Microsoft.EntityFrameworkCore`
* Create a new Constructor for your DbContext class, and require the DbContextOptions parameter and have that constructor derive from the base a. Example Constructor looks like this:
 ```
 public DemoClass13DbContext(DbContextOptions<DemoClass13DbContext> options) : base(options)
    {
	 
	}
 ```

