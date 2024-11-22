---
tags:
  - dotnet
  - swagger
---
If you want to add JWT authentication to your swagger, you can use two following extension methods to `IServiceColletion` and `WebAppliction` and use them in your `Program.cs` file.

```CSharp
public static IServiceCollection AddApiDocumentation(this IServiceCollection services)  
{  
    // Learn more about configuring Swagger/OpenAPI at https://aka.ms/aspnetcore/swashbuckle
    // ApiExplorer using <see cref="Endpoint.Metadata"/>. 
    services.AddEndpointsApiExplorer();
    
    services.AddSwaggerGen(options =>  
    {  
        options.SwaggerDoc("v1", new OpenApiInfo  
        {  
            Version = "v1",  
            Title = "Identix Microservice",  
            Description = "Manage authentication and authorization for Habitasion microservices.",  
            TermsOfService = new Uri("https://habitasion.io/terms"),  
            Contact = new OpenApiContact  
            {  
                Name = "Contact us",  
                Url = new Uri("https://habitasion.io/contact")  
            },            License = new OpenApiLicense  
            {  
                Name = "MTI License",  
                Url = new Uri("https://habitasion.io/license")  
            }
		});

		options.AddSecurityDefinition("Bearer", new OpenApiSecurityScheme  
        {  
            In = ParameterLocation.Header,  
            Description = "Please enter token like: {token}",  
            Name = "Authorization",  
            Type = SecuritySchemeType.Http,  
            BearerFormat = "JWT",  
            Scheme = "bearer"  
        });

        options.AddSecurityRequirement(new OpenApiSecurityRequirement  
        {  
            {
				new OpenApiSecurityScheme  
                {  
                    Reference = new OpenApiReference  
                    {  
                        Type = ReferenceType.SecurityScheme,  
                        Id = "Bearer"  
                    }  
                },
				Array.Empty<string>()  
            }
		});    
	});

	return services;  
}
```