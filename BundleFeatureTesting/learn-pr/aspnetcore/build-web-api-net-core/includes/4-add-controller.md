---
ms.openlocfilehash: e5d8a8fa162ed36d71586ad442438e65904c8cbd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
A *Controller* is a public class with one or more public methods known as *actions*. By convention, a Controller class is placed in the project root's *Controllers* directory. The actions are exposed as callable HTTP endpoints inside the web API controller.

1. Run the following command:

    ```bash
    touch ./Controllers/ProductsController.cs
    ```

    An empty class file named *ProductsController.cs* is created in the *Controllers* directory. The directory name *Controllers* is a convention. The directory name comes from the Model-View-**Controller** architecture used by the web API.

    > [!NOTE]
    > By convention, controller class names are suffixed with *Controller*.
1. Refresh file explorer, and add the following code to *Controllers/ProductsController.cs*. Save your changes.

    ```csharp
    using System.Collections.Generic;
    using System.Linq;
    using System.Threading.Tasks;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.EntityFrameworkCore;
    using ContosoPets.Api.Data;
    using ContosoPets.Api.Models;

    namespace ContosoPets.Api.Controllers
    {
        [Route("api/[controller]")]
        [ApiController]
        public class ProductsController : ControllerBase
        {
            private readonly ContosoPetsContext _context;

            public ProductsController(ContosoPetsContext context)
            {
                _context = context;
            }

            [HttpGet]
            public ActionResult<List<Product>> GetAll() =>
                _context.Products.ToList();

            // GET by ID action

            // POST action

            // PUT action

            // DELETE action
        }
    }
    ```

    This class derives from `ControllerBase`, the base class for an MVC controller without web UI support. The following attributes define its behavior:

    * `[Route]` defines the routing pattern `api/[controller]`. The `[controller]` token is replaced by the controller's name (case-insensitive, without the *Controller* suffix), so requests to `https://localhost:5001/api/products` are handled by this controller.
    * `[ApiController]` adds behaviors that make it easier to build web APIs. Some behaviors include [parameter source inference](https://docs.microsoft.com/aspnet/core/web-api/#binding-source-parameter-inference), [attribute routing as a requirement](https://docs.microsoft.com/aspnet/core/web-api/#attribute-routing-requirement), and [model validation error handling enhancements](https://docs.microsoft.com/aspnet/core/web-api/#automatic-http-400-responses).

    Within the class definition:

    * [Constructor injection](https://docs.microsoft.com/aspnet/core/mvc/controllers/dependency-injection#constructor-injection) provides an instance of `ContosoPetsContext` to the controller.
    * An HTTP GET action named `GetAll` is created for retrieving all products.
1. Start the web API by running the following command:

    ```bash
    dotnet run > ContosoPets.Api.log &
    ```
1. Run the following command:

    ```bash
    curl -k -s https://localhost:5001/api/products | jq
    ```

    > [!TIP]
    > Select the **Reconnect** button if the Cloud Shell session times out.

    The following JSON is returned:

    ```json
    [
      {
        "id": 1,
        "name": "Squeaky Bone",
        "price": 20.99
      },
      {
        "id": 2,
        "name": "Knotted Rope",
        "price": 12.99
      }
    ]
    ```

1. [!INCLUDE[kill command](../../includes/kill-dotnet-processes.md)]

Actions to support CRUD operations on products data will be added to `ProductsController` in the next unit.
