---
ms.openlocfilehash: 819118115ac34a40bf6c37b618fff91c89d5232f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
When the retailer's storefront UI is built, it should display all products in inventory. To fulfill such a requirement, an action responding to an HTTP GET action verb is needed.

The following table depicts the relationship between HTTP action verbs, CRUD operations, and ASP.NET Core attributes. For example, an HTTP PUT action verb is most often used to support an update operation. Such an action is annotated with the `[HttpPut]` attribute.

|HTTP action verb|CRUD operation|ASP.NET Core attribute|
|----------------|--------------|----------------------|
|POST            |Create        |`[HttpPost]`          |
|GET             |Read          |`[HttpGet]`           |
|PUT             |Update        |`[HttpPut]`           |
|DELETE          |Delete        |`[HttpDelete]`        |

In addition to the action verbs in the preceding table, a web API in ASP.NET Core supports HEAD, OPTIONS, and PATCH.

The following sections demonstrate how to support each of these four actions in the web API.

## <a name="retrieve-a-product"></a>Retrieve a product

Replace the `// GET by ID action` comment in *Controllers/ProductsController.cs* with the following:

```csharp
[HttpGet("{id}")]
public async Task<ActionResult<Product>> GetById(long id)
{
    var product = await _context.Products.FindAsync(id);

    if (product == null)
    {
        return NotFound();
    }

    return product;
}
```

The preceding action:

* Responds only to the HTTP GET verb, as denoted by the `[HttpGet]` attribute.
* Requires that the `id` value is included in the URL segment after `api/products/`. Remember, the `/api/products` pattern was defined by the controller-level `[Route]` attribute.
* Queries the database for a product matching the provided `id` parameter.

Each `ActionResult` used in the preceding action is mapped to the corresponding HTTP status code in the following table.

|ASP.NET Core<br>action result|HTTP status code|Description|
|-----------------------------|----------------|-----------|
|`Ok` is implied              |200             |A product matching the provided `id` parameter exists in the database.<br>The product is included in the response body in the media type as defined in the `Accept` HTTP request header (JSON by default).|
|`NotFound`                   |404             |A product matching the provided `id` parameter doesn't exist in the database.|

## <a name="add-a-product"></a>Add a product

Replace the `// POST action` comment in *Controllers/ProductsController.cs* with the following:

```csharp
[HttpPost]
public async Task<ActionResult<Product>> Create(Product product)
{
    _context.Products.Add(product);
    await _context.SaveChangesAsync();

    return CreatedAtAction(nameof(GetById), new { id = product.Id }, product);
}
```

The preceding action:

* Responds only to the HTTP POST verb, as denoted by the `[HttpPost]` attribute.
* Inserts the request body's `Product` object into the database.

> [!NOTE]
> Because the controller is annotated with the `[ApiController]` attribute, it's implied that the `product` parameter will be found in the request body.

The first parameter in the `CreatedAtAction` method call represents an action name. The `nameof` keyword is used to avoid hard-coding the action name. `CreatedAtAction` uses the action name to generate a `Location` HTTP response header with a URL to the newly created product.

Each `ActionResult` used in the preceding action is mapped to the corresponding HTTP status code in the following table.

|ASP.NET Core<br>action result|HTTP status code|Description|
|-----------------------------|----------------|-----------|
|`CreatedAtAction`            |201             |The product was added to the database.<br>The product is included in the response body in the media type as defined in the `Accept` HTTP request header (JSON by default).|
|`BadRequest` is implied      |400             |The request body's `Product` object is invalid.|

## <a name="modify-a-product"></a>Modify a product

Replace the `// PUT action` comment in *Controllers/ProductsController.cs* with the following:

```csharp
[HttpPut("{id}")]
public async Task<IActionResult> Update(long id, Product product)
{
    if (id != product.Id)
    {
        return BadRequest();
    }

    _context.Entry(product).State = EntityState.Modified;
    await _context.SaveChangesAsync();

    return NoContent();
}
```

The preceding action:

* Responds only to the HTTP PUT verb, as denoted by the `[HttpPut]` attribute.
* Requires that the `id` value is included in the URL segment after `api/products/`.
* Updates the `Name` and `Price` properties of the product.

> [!NOTE]
> Because the controller is annotated with the `[ApiController]` attribute, it's implied that the `product` parameter will be found in the request body.

Each `ActionResult` used in the preceding action is mapped to the corresponding HTTP status code in the following table.

|ASP.NET Core<br>action result|HTTP status code|Description|
|-----------------------------|----------------|-----------|
|`NoContent`                  |204             |The product was updated in the database.|
|`BadRequest`                 |400             |The request body's `Id` value doesn't match the route's `id` value.|
|`BadRequest` is implied      |400             |The request body's `Product` object is invalid.|

## <a name="remove-a-product"></a>Remove a product

Replace the `// DELETE action` comment in *Controllers/ProductsController.cs* with the following:

```csharp
[HttpDelete("{id}")]
public async Task<IActionResult> Delete(long id)
{
    var product = await _context.Products.FindAsync(id);

    if (product == null)
    {
        return NotFound();
    }

    _context.Products.Remove(product);
    await _context.SaveChangesAsync();

    return NoContent();
}
```

The preceding action:

* Responds only to the HTTP DELETE verb, as denoted by the `[HttpDelete]` attribute.
* Requires that `id` is included in the URL path.
* Queries the database for a product matching the provided `id` parameter.

Each `ActionResult` used in the preceding action is mapped to the corresponding HTTP status code in the following table.

|ASP.NET Core<br>action result|HTTP status code|Description|
|-----------------------------|----------------|-----------|
|`NoContent`                  |204             |The product was deleted from the database.|
|`NotFound`                   |404             |A product matching the provided `id` parameter doesn't exist in the database.|

## <a name="build-and-run"></a>Build and run

Run the following command:

```bash
dotnet run > ContosoPets.Api.log &
```

The web API is running and is ready for testing via curl.

> [!IMPORTANT]
> Don't forget to check *ContosoPets.Api.log* for troubleshooting information, if required.
