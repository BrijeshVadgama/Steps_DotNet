# Create Below Procedure for API Integration

### Create Table

```
CREATE TABLE[Person]
(
	 [PersonID] INT PRIMARY KEY IDENTITY(1,1) NOT NULL
	,[Name] VARCHAR(50) NOT NULL
	,[Contact] VARCHAR(50) NOT NULL
	,[Email] VARCHAR(50) NOT NULL
)
```

### Insert Some Records

```
INSERT INTO [dbo].[Person] VALUES ('ABC','968574126','abc@gmail.com')
INSERT INTO [dbo].[Person] VALUES ('DEF','968574126','def@gmail.com')
INSERT INTO [dbo].[Person] VALUES ('GHI','968574126','ghi@gmail.com')
INSERT INTO [dbo].[Person] VALUES ('JKL','968574126','jkl@gmail.com')
INSERT INTO [dbo].[Person] VALUES ('MNO','968574126','mno@gmail.com')
```

`SELECTALL PROCEDURE`

```
CREATE OR ALTER PROCEDURE [dbo].[API_Person_SelectAll]
AS
BEGIN
	SELECT
		 [dbo].[Person].[PersonID]
		,[dbo].[Person].[Name]
		,[dbo].[Person].[Contact]
		,[dbo].[Person].[Email]
	FROM
		[dbo].[Person]
	ORDER BY
		 [dbo].[Person].[Name]
		,[dbo].[Person].[Email]
END
```

`SELECTBYID PROCEDURE`

```
CREATE OR ALTER PROCEDURE [dbo].[API_Person_SelectByID]
@PersonID	INT
AS
BEGIN
	SELECT
		 [Person].[PersonID]
		,[Person].[Name]
		,[Person].[Contact]
		,[Person].[Email]
	FROM
		[dbo].[Person]
	WHERE
		[dbo].[Person].[PersonID] = @PersonID
END
```

`INSERT PROCEDURE`

```
CREATE OR ALTER PROCEDURE [dbo].[API_Person_Insert]
 @Name		VARCHAR(50)
,@Contact	VARCHAR(50)
,@Email		VARCHAR(50)
AS
BEGIN
	INSERT INTO [dbo].[Person]
	(
		 [Name]
		,[Contact]
		,[Email]
	)
	VALUES
	(
		 @Name
		,@Contact
		,@Email
	)
END
```

`UPDATE PROCEDURE`

```
CREATE OR ALTER PROCEDURE [dbo].[API_Person_Update]
 @PersonID	INT
,@Name		VARCHAR(50)
,@Contact	VARCHAR(50)
,@Email		VARCHAR(50)
AS
BEGIN
	UPDATE [dbo].[Person]
	SET
		 [Name] = @Name
		,[Contact] = @Contact
		,[Email] = @Email
	WHERE
		[dbo].[Person].[PersonID] = @PersonID
END
```

`DELETE PROCEDURE`

```
CREATE OR ALTER PROCEDURE [dbo].[API_Person_Delete]
@PersonID	INT
AS
BEGIN
	DELETE
	FROM [dbo].[Person]
	WHERE
		[dbo].[Person].[PersonID] = @PersonID
END
```
