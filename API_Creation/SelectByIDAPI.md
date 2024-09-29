# API Integration -- SelectByID

### Step-1 : Add Below Code to the `PersonController`

```
#region API_PersonSelectByID
[HttpGet("{PersonID}")]
public IActionResult GetPersonByID(int PersonID)
{
    Person_BALBase balPerson = new Person_BALBase();
    PersonModel personModel = balPerson.API_Person_SelectByID(PersonID);

    Dictionary<string, dynamic> response = new Dictionary<string, dynamic>();
    if (personModel != null)
    {
        response.Add("status", true);
        response.Add("message", "Data Found!");
        response.Add("data", personModel);
        return Ok(response);
    }
    else
    {
        response.Add("status", false);
        response.Add("data", null);
        return Ok(response);
    }

}
#endregion API_PersonSelectByID
```

### Step-2 : Add Below Code to the `Person_DALBase.cs`

```
#region API_Person_SelectByID
public PersonModel API_Person_SelectByID(int PersonID)
{
    try
    {
        SqlDatabase sqlDB = new SqlDatabase(ConnString);
        DbCommand cmd = sqlDB.GetStoredProcCommand("API_Person_SelectByID");
        PersonModel personModel = new PersonModel();
        sqlDB.AddInParameter(cmd, "@PersonID", SqlDbType.Int, PersonID);

        using (IDataReader dr = sqlDB.ExecuteReader(cmd))
        {
            while (dr.Read())
            {
                personModel.PersonID = Convert.ToInt32(dr["PersonID"].ToString());
                personModel.Name = dr["Name"].ToString();
                personModel.Contact = dr["Contact"].ToString();
                personModel.Email = dr["Email"].ToString();

            }
        }
        return personModel;
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.ToString());
        return null;
    }
}
#endregion API_Person_SelectByID
```

### Step-3 : Add Below Code to the `Person_BALBase.cs`

```
#region API_SelectPersonByID
public PersonModel API_Person_SelectByID(int PersonID)
{
    try
    {
        Person_DALBase dalPerson = new Person_DALBase();
        PersonModel personModels = dalPerson.API_Person_SelectByID(PersonID);
        return personModels;
    }
    catch
    {
        return null;
    }
}
#endregion API_SelectPersonByID
```
