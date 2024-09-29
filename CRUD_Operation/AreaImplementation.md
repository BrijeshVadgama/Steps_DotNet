# Implementation of Area in MVC

### Create Area Folder

```
Right Click On Project -> Add -> New Scaffolded Items -> MVC Area -> Add -> Give Area Name -> Add
```

### In Program.cs

After Create `Area` Folder Add Below Code in `Program.cs` File

```
app.MapControllerRoute(
    name: "areas",
    pattern: "{area:exists}/{controller=Home}/{action=Index}/{id?}"
);
```

### Add 2 Files

Add Below 2 Files into `Area` Folder From `Views` Folder

```
_ViewImports.cshtml
_ViewStart.cshtml
```

### Import Model

Write Below Line into `_ViewImports.cshtml`

```
@using YourProjectName.Areas.AreaName.Models
```

### Area and Route in Controller

Add Below 2 lines into `Controller` Where would you use `Area`

```
[Area("AreaName")]
[Route("AreaName/{controller}/{action}")]
```
