# API Integration -- SelectAll

### Step-1 : Add Below Code to the `PersonController`

```
#region API_PersonSelectAll
[HttpGet]
public IActionResult GetAllPerson()
{
    Person_BALBase balPerson = new Person_BALBase();
    List<PersonModel> modelPerson = balPerson.API_Person_SelectAll();

    Dictionary<string, dynamic> response = new Dictionary<string, dynamic>();
    if (modelPerson.Count > 0 && modelPerson != null)
    {
        response.Add("status", true);
        response.Add("message", "Data Found!");
        response.Add("data", modelPerson);
        return Ok(response);
    }
    else
    {
        response.Add("status", false);
        response.Add("data", null);
        return Ok(response);
    }

}
#endregion API_PersonSelectAll
```

### Step-2 : Add Below Code to the `Person_DALBase.cs`

```
#region API_Person_SelectAll
public List<PersonModel> API_Person_SelectAll()
{
    try
    {
        SqlDatabase sqlDB = new SqlDatabase(ConnString);
        DbCommand cmd = sqlDB.GetStoredProcCommand("API_Person_SelectAll");
        List<PersonModel> personModels = new List<PersonModel>();
        using (IDataReader dr = sqlDB.ExecuteReader(cmd))
        {
            while (dr.Read())
            {
                PersonModel personModel = new PersonModel();
                personModel.PersonID = Convert.ToInt32(dr["PersonID"].ToString());
                personModel.Name = dr["Name"].ToString();
                personModel.Contact = dr["Contact"].ToString();
                personModel.Email = dr["Email"].ToString();
                personModels.Add(personModel);
            }
        }
        return personModels;
    }
    catch (Exception ex) 
    {
        Console.WriteLine(ex.ToString());
        return null;
    }
}
#endregion API_Person_SelectAll
```

### Step-3 : Add Below Code to the `Person_BALBase.cs`

```
#region API_SelectAllPerson
public List<PersonModel> API_Person_SelectAll()
{
    try
    {
        Person_DALBase dalPerson = new Person_DALBase();
        List<PersonModel> personModels = dalPerson.API_Person_SelectAll();
        return personModels;
    }
    catch
    {
        return null;
    }
}
#endregion API_SelectAllPerson
```
