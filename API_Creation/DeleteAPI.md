# API Integration -- Delete

### First Create Blank API Project

### Remove `WeatherForcastController.cs` and `WeatherForcast.cs` file

### Step-1 : First Add Below `Package` from the `NuGet Package Manager`

```
- System.Data.SqlClient
- EnterpriseLibrary.Data
```

### Step-2 : Add `ConnectionString` to the `appsettings.json` file

```
"ConnectionStrings": {
    "ConnectionString": "Data Source=ConnectionString;Initial Catalog=DatabaseName;Integrated Security=True"
}
```

### Step-3 : Create `Model Folder` and Create `PersonModel` and Add Below Code

```
namespace WebApi_Demo.Models
using System.ComponentModel.DataAnnotations;

namespace WebApi_Demo.Models
{
    public class PersonModel
    {
        public int? PersonID { get; set; }

        [Required]
        public string Name { get; set; }

        [Required]
        public string Contact { get; set; }

        [Required]
        public string Email { get; set; }
    }
}
```

### Step-4 : Create PersonController

`How to Create PersonController`
`Right click on Controller Add -> Controller -> MVC Controller - Empty -> API Controller - Empty`

### Add Below Code to the `PersonController`

```
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using WebApi_Demo.BAL;

namespace WebApi_Demo.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class PersonController : ControllerBase
    {
        #region API_PersonDelete
        [HttpDelete]
        public IActionResult DeletePerson(int PersonID)
        {
            Person_BALBase balPerson = new Person_BALBase();
            bool IsSuccess = balPerson.API_Person_Delete(PersonID);

            Dictionary<string,dynamic> response = new Dictionary<string, dynamic>();
            if (IsSuccess)
            {
                response.Add("status", true);
                response.Add("message", "Data Deleted Successfully!");
                return Ok(response);
            }
            else
            {
                response.Add("status", false);
                response.Add("message", "Data Cannot Deleted Successfully!");
                return Ok(response);
            }
        }
        #endregion API_PersonDelete
    }
}
```

### Step-5 : Create `DAL Folder` into the Project

### Add `DAL_Helper.cs` file into DAL Folder and Add Below Code

```
namespace WebApi_Demo.DAL
{
    public class DAL_Helper
    {
        public static string ConnString = new ConfigurationBuilder().AddJsonFile("appsettings.json").Build().GetConnectionString("ConnectionString");
    }
}
```

### Step-6 : Create `Person_DALBase.cs` into DAL Folder and Add Below Code

```
using Microsoft.Practices.EnterpriseLibrary.Data.Sql;
using System.Data;
using System.Data.Common;

namespace WebApi_Demo.DAL
{
    public class Person_DALBase : DAL_Helper
    {
        #region API_PersonDelete
        public bool API_Person_Delete(int PersonID)
        {
            try
            {
                SqlDatabase sqlDB = new SqlDatabase(ConnString);
                DbCommand cmd = sqlDB.GetStoredProcCommand("API_Person_Delete");
                sqlDB.AddInParameter(cmd, "@PersonID", SqlDbType.Int, PersonID);
                if (Convert.ToBoolean(sqlDB.ExecuteNonQuery(cmd)))
                {
                    return true;
                }
                else
                {
                    return false;
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.ToString());
                return false;
            }
        }
        #endregion API_PersonDelete
    }
}
```

### Step-7 : Create `BAL` Folder into the Project

### Create `Person_BALBase.cs` file into the `BAL Folder` and Add Below Code

```
using WebApi_Demo.DAL;

namespace WebApi_Demo.BAL
{
    public class Person_BALBase
    {
        #region API_PersonDelete
        public bool API_Person_Delete(int PersonID)
        {
            try
            {
                Person_DALBase dalPerson = new Person_DALBase();
                if (dalPerson.API_Person_Delete(PersonID))
                {
                    return true;
                }
                else
                {
                    return false;
                }
            }
            catch (Exception ex)
            {
                return false;
            }
        }
        #endregion API_PersonDelete
    }
}
```
