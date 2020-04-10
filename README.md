# Starting from scratch
  * Create a new project and select `ASP.NET Core Web Application`
  * Choose empty
  * In `Startup.cs` in `ConfigureServices` method, add `services.AddMvc()` in code block.
  * In `Configure` method
  *replace*
  ```
  endpoints.MapGet("/", async context =>
{
    await context.Response.WriteAsync("Hello World!");
});
   ```
   with
   
   ```
   app.UseEndpoints(endpoints =>
{
    endpoints.MapControllerRoute("default", "{controllers=Home}/{action=Index}/{id?}");
});
```
* Create `Controllers`, `Data`, & `Models` folders in root of project
* Create your models in `Models` folder
* In `appsettings.json` add connection string. Don't forget to change database name.
  * To be more secured, add user secrets by right clicking on your project and `add user secrets`. You can add your connection string in the newly populated file, and delete the appsettings.json.
```
"ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\MSSQLLocalDB;Database=DBNAMEHERE;Trusted_Connection=True;MultipleActiveResultSets=true"
  }
```


