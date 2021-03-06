# Creating an Application Service
* [Unit of Work](#unit-of-work)
* [Hide from Controller](#hide-from-controller)

## Unit of Work
By default functions in an application service are transactional, meaning if there's an exception in the function then all repository functions are rolled back. It can be turned off by adding the ```UnitOfWork``` attribute to your function and setting ```IsDisabled``` to ```true```.
```csharp
[UnitOfWork(IsDisabled: true)]
```

You can also use Unit of Work to impersonate another tenant

```csharp
using (_unitOfWorkManager.Current.SetTenantId(input.TentantId))
{
} 
```

## Hide from Controller
The __.Web.Core__ module is configured to generate WebAPI controllers for any application services found in __.Application__. To prevent a specific application service or function in a service from being generated, add the ```RemoteService``` attibute and set ```isEnabled``` to ```false```.
```csharp
[RemoteService(isEnabled: false)]
```

## Function Names
HTTP verbs are determined by method name prefixes, otherwise __Post__ is used as default HTTP verb. You can also override or specify a preferred method using the the HTTP-verb attributes found in Microsoft.AspNet.WebApi.Core.

* __Get:__ Used if method name starts with 'Get'.
* __Put:__ Used if method name starts with 'Put' or 'Update'.
* __Delete:__ Used if method name starts with 'Delete' or 'Remove'.
* __Post:__ Used if method name starts with 'Post', 'Create' or 'Insert'.
* __Patch:__ Used if method name starts with 'Patch'.

## See Also
* [ASP\.NET Boilerplate Tutorials](README.md)
* [Project Architecture](projectarchitecture.md)
* [Frontend Built-in Functions](angularbuiltin.md)
