```csharp
using System.Text.Json.Serialization;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.

builder.Services.Configure<Microsoft.AspNetCore.Http.Json.JsonOptions>(options =>
{
    options.SerializerOptions.AddContext<MyJsonDtoContext>();
});

//builder.Services.Configure<Microsoft.AspNetCore.Mvc.JsonOptions>(options =>
//{
//    options.JsonSerializerOptions.AddContext<MyJsonDtoContext>();
//});


var app = builder.Build();

app.MapPost("/test", (MyJsonDto dto) =>
{
    return dto;
});

app.Run();



public class MyJsonDto
{
    public int Id { get; set; }

    public string Name { get; set; }
}

[JsonSerializable(typeof(MyJsonDto))]
public partial class MyJsonDtoContext : JsonSerializerContext { }
```
