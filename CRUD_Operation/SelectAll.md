# Select All Product

### Add ConnectionString to appsettings.json

```
{
  "ConnectionStrings": {
    "ConnectionString": "Data Source=Your_Database_Connection_String;Initial Catalog=Your_Database_Name;Integrated Security=true;"
  }
}
```

### Add Product Routing in \_Layout.cshtml

```
 <li class="nav-item">
     <a class="nav-link text-dark" asp-controller="Product" asp-action="ProductList">Product</a>
 </li>
```

# Create ProductController

### Configuration

```
#region Configuration
private IConfiguration configuration;

public ProductController(IConfiguration _configuration)
{
    configuration = _configuration;
}
#endregion Configuration
```

### Method

In ProductController Add this method to display all products

```
#region ProductList
public IActionResult ProductList()
{
    string connectionString = this.configuration.GetConnectionString("ConnectionString");
    SqlConnection conn = new SqlConnection(connectionString);
    conn.Open();
    SqlCommand cmd = conn.CreateCommand();
    cmd.CommandType = CommandType.StoredProcedure;
    cmd.CommandText = "SP_Select_All_Products";
    SqlDataReader reader = cmd.ExecuteReader();
    DataTable dt = new DataTable();
    dt.Load(reader);
    return View(dt);
}
#endregion ProductList
```

### Create ProductList View

```
@using System.Data;

@{
    ViewData["Title"] = "Product List";
}

<h1 class="mt-3 mb-3">Product List</h1>

<table class="table table-bordered table-hover table-striped">
    <thead>
        <tr>
            <th>ProductName</th>
            <th>ProductPrice</th>
            <th>ProductCode</th>
            <th>Description</th>
            <th>Username</th>
            <th>Action</th>
        </tr>
    </thead>
    <tbody>
        @{
            foreach(DataRow product in Model.Rows)
            {
                <tr>
                    <td>@product["ProductName"]</td>
                    <td>@product["ProductPrice"]</td>
                    <td>@product["ProductCode"]</td>
                    <td>@product["Description"]</td>
                    <td>@product["Username"]</td>
                    <td>
                        <button class="btn btn-sm btn-success">Edit</button>
                        <button class="btn btn-sm btn-danger">Delete</button>
                    </td>
                </tr>
            }
        }
    </tbody>
</table>
```
