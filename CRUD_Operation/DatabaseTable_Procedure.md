# Create Database

```
CREATE DATABASE IF NOT EXISTS CoffeeShopManagementSystem
```

# Create Table

```
CREATE TABLE [Product]
(
	 [ProductID] INT PRIMARY KEY IDENTITY(1,1) NOT NULL
	,[ProductName] VARCHAR(100) NOT NULL
	,[ProductPrice] DECIMAL(10,2) NOT NULL
	,[ProductCode] VARCHAR(100) NOT NULL
	,[Description] VARCHAR(100) NOT NULL
	,[UserID] INT FOREIGN KEY REFERENCES [USER](UserId) NOT NULL
);
```

# Procedures

### Select All

```
CREATE OR ALTER PROCEDURE [dbo].[SP_Select_All_Products]
AS
BEGIN
	SELECT
		 [dbo].[Product].[ProductID]
		,[dbo].[Product].[ProductName]
		,[dbo].[Product].[ProductPrice]
		,[dbo].[Product].[ProductCode]
		,[dbo].[Product].[Description]
		,[dbo].[Product].[UserID]
		,[dbo].[User].[UserName]
	FROM
		[dbo].[Product]
			INNER JOIN
		[dbo].[User] ON [dbo].[User].[UserID] = [dbo].[Product].[UserID]
	ORDER BY
		 [dbo].[Product].[ProductID]
		,[dbo].[Product].[ProductName]
END
```

### Select ByID

```
CREATE OR ALTER PROCEDURE [dbo].[SP_Select_Product_ByID]
@ProductID			INT
AS
BEGIN
	SELECT
		 [dbo].[Product].[ProductID]
		,[dbo].[Product].[ProductName]
		,[dbo].[Product].[ProductPrice]
		,[dbo].[Product].[ProductCode]
		,[dbo].[Product].[Description]
		,[dbo].[Product].[UserID]
		,[dbo].[User].[UserName]
	FROM
		[dbo].[Product]
			INNER JOIN [dbo].[User] ON [dbo].[User].[UserID] = [dbo].[Product].[UserID]
	WHERE
		[dbo].[Product].[ProductID] = @ProductID
END
```

### Insert

```
CREATE OR ALTER PROCEDURE [dbo].[SP_Insert_Product]
@ProductName		VARCHAR(100),
@ProductPrice		DECIMAL(10,2),
@ProductCode		VARCHAR(100),
@Desciption			VARCHAR(100),
@UserID				INT
AS
BEGIN
	INSERT INTO [dbo].[Product]
	(
		 [ProductName]
		,[ProductPrice]
		,[ProductCode]
		,[Description]
		,[UserID]
	)
	VALUES
	(
		 @ProductName
		,@ProductPrice
		,@ProductCode
		,@Desciption
		,@UserID
	)
END
```

### Update

```
CREATE OR ALTER PROCEDURE [dbo].[SP_Update_Product_ByID]
 @ProductID			INT
,@ProductName		VARCHAR(100)
,@ProductPrice		DECIMAL(10,2)
,@ProductCode		VARCHAR(100)
,@Description		VARCHAR(100)
,@UserID			INT
AS
BEGIN
	UPDATE [dbo].[Product]
		SET  [ProductName] = @ProductName
			,[ProductPrice] = @ProductPrice
			,[ProductCode] = @ProductCode
			,[Description] = @Description
			,[UserID] = @UserID
	WHERE
		[dbo].[Product].[ProductID] = @ProductID
END
```

### Delete

```
CREATE OR ALTER PROCEDURE [dbo].[SP_Delete_Product_ByID]
@ProductID			INT
AS
BEGIN
	DELETE
	FROM [dbo].[Product]
	WHERE [dbo].[Product].[ProductID] = @ProductID
END
```
