# Implementation of our Custom Error Page

### Program.cs

Add Below Code in program.cs file

```
if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/Home/Error");
}
else
{
    app.UseStatusCodePagesWithReExecute("/ErrorPage/{0}");
}
```

### Create ErrorPageController

Add Below Code in ErrorPageController.cs file

```
[Route("ErrorPage/{statuscode}")]
public IActionResult Error404Page(int statuscode)
{
    if (statuscode == 404)
    {
        return View();
    }
    return View();
}
```

### Crete Error404Page.cshtml

Add Below Code in Error404Page.cs file

```
@{
    Layout = null;
}

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>404 - Page Not Found</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body, html {
            height: 100%;
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: #f5f5f5;
        }

        .container {
            text-align: center;
            background-color: white;
            padding: 40px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            border-radius: 10px;
        }

        .container h1 {
            font-size: 100px;
            color: #333;
            margin-bottom: 10px;
        }

        .container h2 {
            font-size: 24px;
            color: #555;
            margin-bottom: 20px;
        }

        .container p {
            font-size: 16px;
            color: #777;
            margin-bottom: 30px;
        }

        .container a {
            padding: 10px 20px;
            text-decoration: none;
            background-color: #3498db;
            color: white;
            border-radius: 5px;
            transition: background-color 0.3s;
        }

        .container a:hover {
            background-color: #2980b9;
        }

        /* Add responsive design for smaller screens */
        @@media (max-width: 600px) {
            .container {
                padding: 20px;
            }

            .container h1 {
                font-size: 70px;
            }

            .container h2 {
                font-size: 20px;
            }

            .container p {
                font-size: 14px;
            }
        }
    </style>
</head>
<body>

<div class="container">
    <h1>404</h1>
    <h2>Oops! Page not found</h2>
    <p>Sorry, but the page you're looking for doesn't exist.</p>
    <a href="/">Go Back Home</a>
</div>

</body>
</html>
```
