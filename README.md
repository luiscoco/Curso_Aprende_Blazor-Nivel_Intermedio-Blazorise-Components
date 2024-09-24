# How to install Blazorise Components in your Blazor Web Application

**Note:** For more information about this sample visit this URL: https://blazorise.com/docs/start

## 1. Load the Nuget packages

![image](https://github.com/user-attachments/assets/86e463d1-df00-4c0b-bec2-8e88948184d8)

## 2. Modify the App.razor component to include the Radzen references

Include these lines in the **App.razor** component:

```
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-rbsA2VBKQhggwzxH7pPCaAqO46MgnOM80zW1RWuH61DGLwZJEdK2Kadq2F9CUG65" crossorigin="anonymous">
<link href="_content/Blazorise.Icons.FontAwesome/v6/css/all.min.css" rel="stylesheet">
<link href="_content/Blazorise/blazorise.css" rel="stylesheet" />
<link href="_content/Blazorise.Bootstrap5/blazorise.bootstrap5.css" rel="stylesheet" />
```

This is the **App.razor** whole code:

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <base href="/" />
    <link rel="stylesheet" href="bootstrap/bootstrap.min.css" />
    <link rel="stylesheet" href="app.css" />
    <link rel="stylesheet" href="blazoriseSample1.styles.css" />
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-rbsA2VBKQhggwzxH7pPCaAqO46MgnOM80zW1RWuH61DGLwZJEdK2Kadq2F9CUG65" crossorigin="anonymous">
    <link href="_content/Blazorise.Icons.FontAwesome/v6/css/all.min.css" rel="stylesheet">
    <link href="_content/Blazorise/blazorise.css" rel="stylesheet" />
    <link href="_content/Blazorise.Bootstrap5/blazorise.bootstrap5.css" rel="stylesheet" />
    <link rel="icon" type="image/png" href="favicon.png" />
    <HeadOutlet @rendermode="InteractiveServer" />
</head>

<body>
    <Routes @rendermode="InteractiveServer" />
    <script src="_framework/blazor.web.js"></script>
</body>

</html>
```

## 3. Include in the _Imports.razor the Radzen.Blazor

```
@using System.Net.Http
@using System.Net.Http.Json
@using Microsoft.AspNetCore.Components.Forms
@using Microsoft.AspNetCore.Components.Routing
@using Microsoft.AspNetCore.Components.Web
@using static Microsoft.AspNetCore.Components.Web.RenderMode
@using Microsoft.AspNetCore.Components.Web.Virtualization
@using Microsoft.JSInterop
@using blazoriseSample1
@using blazoriseSample1.Components
@using Blazorise
```

## 4. Modify the middleware(program.cs)

We have to include this code:

```
builder.Services
    .AddBlazorise(options =>
    {
        options.Immediate = true;
    })
    .AddBootstrap5Providers()
    .AddFontAwesomeIcons();
```

This is the **Program.cs** file

```csharp
using blazoriseSample1.Components;
using Blazorise;
using Blazorise.Bootstrap5;
using Blazorise.Icons.FontAwesome;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddRazorComponents()
    .AddInteractiveServerComponents();

builder.Services
    .AddBlazorise(options =>
    {
        options.Immediate = true;
    })
    .AddBootstrap5Providers()
    .AddFontAwesomeIcons();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/Error", createScopeForErrors: true);
    // The default HSTS value is 30 days. You may want to change this for production scenarios, see https://aka.ms/aspnetcore-hsts.
    app.UseHsts();
}

app.UseHttpsRedirection();

app.UseStaticFiles();
app.UseAntiforgery();

app.MapRazorComponents<App>()
    .AddInteractiveServerRenderMode();

app.Run();

```

## 5. Create a new Razor Component to validate the Radzen installation

We right on the **Pages** folder and we select the menu option **Add->Razor Component**

![image](https://github.com/user-attachments/assets/00275830-0f8d-4d84-98cd-3d04df98217e)

This is the new Razor Component source code:

```razor
@page "/tests/buttons"

@* https://bootstrap5demo.blazorise.com/tests/buttons *@
@* https://github.com/Megabit/Blazorise *@

<Row>
    <Column>
        <Card Margin="Margin.Is4.OnY">
            <CardHeader>
                <CardTitle>Default Buttons</CardTitle>
            </CardHeader>
            <CardBody>
                <CardText>Use the color enums like <code>Color.Primary</code></CardText>
            </CardBody>
            <CardBody>
                <Button Color="Color.Primary" @onclick="OnClickButtonBlazorise">Primary</Button>
                <Button Color="Color.Secondary">Secondary</Button>
                <Button Color="Color.Success">Success</Button>
                <Button>Default</Button>
            </CardBody>
        </Card>
    </Column>
</Row>

<br />

<br />

<p>@message</p>

@code {

    public string message = "";

    public void OnClickButtonBlazorise()
    {
        message = "Hello World!";
    }
}
```

## 6. Modify the NavMenu.razor component and add a new NavLink

```
<div class="nav-item px-3">
     <NavLink class="nav-link" href="tests/buttons">
         <span class="bi bi-list-nested-nav-menu" aria-hidden="true"></span> BlazoriseButtons
     </NavLink>
</div>
```

## 7. Run the application to validate the result

![image](https://github.com/user-attachments/assets/ac943ec9-9b9a-4af9-9054-bbfd5f86ef67)
