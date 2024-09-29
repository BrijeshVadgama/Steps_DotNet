# API Integration -- Insert

### Step-1 : Add Below Code to the `PersonController`

```
#region API_PersonInsert
[HttpPost]
public IActionResult InsertPerson([FromForm]PersonModel personModel)
{
    Person_BALBase balPerson = new Person_BALBase();
    bool IsSuccess = balPerson.API_Person_Insert(personModel);

    Dictionary<string, dynamic> response = new Dictionary<string, dynamic>();
    if (IsSuccess)
    {
        response.Add("status", true);
        response.Add("message", "Data Inserted Successfully!");
        return Ok(response);
    }
    else
    {
        response.Add("status", false);
        response.Add("message", "Data Cannot Inserted Successfully!");
        return Ok(response);
    }
}
#endregion API_PersonInsert
```

### Step-2 : Add Below Code to the `Person_DALBase.cs`

```
#region API_PersonInsert
public bool API_Person_Insert(PersonModel personModel)
{
    try
    {
        SqlDatabase sqlDB = new SqlDatabase(ConnString);
        DbCommand cmd = sqlDB.GetStoredProcCommand("API_Person_Insert");

        sqlDB.AddInParameter(cmd, "@Name", SqlDbType.VarChar, personModel.Name);
        sqlDB.AddInParameter(cmd, "@Contact", SqlDbType.VarChar, personModel.Contact);
        sqlDB.AddInParameter(cmd, "@Email", SqlDbType.VarChar, personModel.Email);

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
#endregion API_PersonInsert
```

### Step-3 : Add Below Code to the `Person_BALBase.cs`

```
#region API_PersonInsert
public bool API_Person_Insert(PersonModel personModel)
{
    try
    {
        Person_DALBase dalPerson = new Person_DALBase();
        if (dalPerson.API_Person_Insert(personModel))
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
#endregion API_PersonInsert
```
