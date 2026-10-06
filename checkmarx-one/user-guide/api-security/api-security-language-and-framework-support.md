# API Security Language and Framework Support

This section provides relevant information about the current support for API security queries in Java.

| **Language** | **Framework** | **Framework Support Details** | **Details Needed** |
|---|---|---|---|
| Java | Spring and all Spring-related frameworks | • RequestMapping annotation<br>• Get/Post/Put/Delete/PatchMapping annotations. | • Each method with this annotation, including the method info, method annotations, and annotations parameter values<br>• If the class of the method has this annotation, we need its parameter value, too, as it's the prefix |

There are nine queries for Java support in SAST. The table below shows the framework with the query, query name, brief description, category in SAST, and the JSON result generated.

| **Framework** | **Query Name** | **Description** | **Category** |
|---|---|---|---|
| Spring and all Spring-related frameworks | Java_WebApi_GetApiList | This is the main query and returns the list of endpoint information. | Executable |
| Spring and all Spring-related frameworks | Java_WebApi_MethodsWithAnnotation | Retrieves all the endpoints with API annotations. | General |
| Spring and all Spring-related frameworks | Java_WebApi_MethodsNoAnnotation | Retrieves all the endpoints without API annotations but with a defined route template. | General |
| Spring and all Spring-related frameworks | Java_WebApi_Create_Comment | Collects details for every endpoint and provides this information, including the URL, HTTP method, method name, method line, method row, response type, and request type. | General |
| Spring and all Spring-related frameworks | Java_WebApi_RetrieveURLAndMethodInfo | Retrieves the method's route path, name, location, and request type (GET, POST, PUT or DELETE). | General |
| Spring and all Spring-related frameworks | Java_WebApi_RetrieveResponseType | Retrieves method details related to response type, structure, and HTTP status code. | General |
| Spring and all Spring-related frameworks | Java_WebApi_RetrieveRequestInfo | Retrieves method parameters, their name, data type, data structure, and source code location (line and file name), and determines if they serve as framework arguments. | General |
| Spring and all Spring-related frameworks | Java_WebApi_GetType | Retrieves parameter type and its type structure, particularly when dealing with custom classes. | General |
| Spring and all Spring-related frameworks | Java_WebApi_ExtractProperties | Retrieves the fields of an unknown class. | General |

<details>

<summary>Limitations</summary>

This section aims to detail the limitations of the supported frameworks.

**Spring**

- We only include the path parameter in the `RequestMappingInfo` object if it is a string literal. In situations where where it is an array initializer or a binary expression, it returns an empty string. When searching the method, we only rely on the method name since there is no available information about the controller, only the handler. This approach may lead to incorrect results if two methods have identical names. See example:

```
RequestMappingInfo info = RequestMappingInfo
                .paths("/user/{id}").methods(RequestMethod.GET).build();
Method method = UserHandler.class.getMethod("getUser", Long.class);
mapping.registerMapping(info, handler, method);
```

</details>

<details>

<summary>Notes</summary>

In the Spring frameworks, for methods without annotations, filter them out based on the following criteria:

- Annotations like @PostConstruct, @ExceptionHandler, @Bean, @Scheduled, @InitBinder and @ModelAttribute.
- *Static* methods and classes.
- *Private* classes.
- Methods with the @Override annotation.
- Methods with the @Value annotation.
- Methods with the @Test annotation.
- Method Invokes

</details>

This section provides relevant information about the current support for API security queries in the C# language.

| **Language** | **Framework** | **Framework Support Details** | **Details Needed** |
|---|---|---|---|
| CSharp | Web API / MVC | • RequestMapping annotation<br>• HttpGet/HttpPost/HttpPut/HttpDelete/RoutePrefix/Route annotations<br>• Convention-based Routing (e.g., `Routes.MapHttpRoute`)<br>• `NonAction` attribute<br>• Attribute Routing (optional parameters and route prefix) | • Each method with this annotation, including the method info, method annotations, and annotations parameter values<br>• If the class of the method has this annotation, we need its parameter value, too, as it's the prefix |

There are ten queries for *C#* support in SAST. The table below provides a brief overview of them.

| **Framework** | **Query Name** | **Description** | **Category** |
|---|---|---|---|
| Web API / MVC | CSharp_WebApi_GetApiList | This is the main query and returns the list of endpoint information. | Executable |
| Web API / MVC | CSharp_WebApi_MethodAnnotation | Retrieves all the endpoints with API annotations. | General |
| Web API / MVC | CSharp_WebApi_MethodNoAnnotation | Retrieves all the endpoints without API annotations but with a defined route template. | General |
| Web API / MVC | CSharp_WebApi_Check_RouteTemplate | Retrieves the method’s parameters that are passed in a route template | |
| Web API / MVC | CSharp_WebApi_Create_Comment | Collects details for every endpoint and provides this information, including the URL, HTTP method, method name, method line, method row, response type, and request type. | General |
| Web API / MVC | CSharp_WebApi_RetrieveUrlHttpMethod | Retrieves the method's route path, name, location, and request type (GET, POST, PUT or DELETE). | General |
| Web API / MVC | CSharp_WebApi_RetrieveResponseType | Retrieves method details related to response type, structure, and HTTP status code. | General |
| Web API / MVC | CSharp_WebApi_RetrieveRequestInfo | Retrieves method parameters, their name, data type, data structure, and source code location (line and file name), and determines if they serve as framework arguments. | General |
| Web API / MVC | CSharp_WebApi_GetType | Retrieves parameter type and its type structure, particularly when dealing with custom classes. | General |
| Web API / MVC | CSharp_WebApi_ExtractProperties | Retrieves the fields of an unknown class. | General |

<details>

<summary>Limitations</summary>

This section aims to detail the limitations of the supported frameworks.

**Web API**

- At this time, to avoid excessive query performance overhead, if we encounter a class that invokes another class with fields and so forth, we will only fetch the fields during the initial iteration. As an example, see below:

```
public async Task<ActionResult<int>> Create([FromBody] CreateProductCommand command)
public class CreateProductCommand : IRequest<int>
{
    public string ProductName { get; set; }
    public Category ProductCategory { get; set; }
}
public class Category
{
    public string CategoryName { get; set; }
}
```

**JSON Result**

```
"requestInfo" : [{
 "ParamName" : "command",
"ParamType" : "CreateProductCommand",
  "typeStructure" : {
    "ProductName" : "string",
    "ProductCategory" : Category"
  },
"ParamLocation" : "bodyParam"
}]
```

</details>

This section provides relevant information about the current support for API security queries in the Python language.

| **Language** | **Framework** | **Framework Support Details** | **Details Needed** |
|---|---|---|---|
| Python | Django | • *urlpatterns* sequence variable in the URLconf module (this contains django.urls.path and/or django.urls.re_path instances)<br>• Path converters<br>• Registering custom path converters<br>• Regular expressions in paths and converters<br>• @require_http_methods() decoration | Each call to path/re_path and parameters |
| Python | Flask | • @app.route("/url") decoration<br>• @get/post/put/patch/delete("/url") shortcut decorations<br>• app.add_url_rule("/url", my_handler)<br>• Blueprint<br>• Werkzeug routing<br>• Custom decorators | The decoration and its parameter values.<br>The call parameters |

There are 12 queries to support Python in SAST. The table below provides a brief overview of them.

| **Framework** | **Query Name** | **Description** | **Category** |
|---|---|---|---|
| Django | Python_Django_WebApi_GetApiList | This is the main query and returns the list of endpoint information. | Executable |
| Django | Python_WebApi_Django | Retrieves all the endpoints in Django. | General |
| Django | Python_WebApi_Django_CreateComment | Collects details for every endpoint and provides this information, including the URL, HTTP method, method name, method line, method row, response type, and request type. | General |
| Django | Python_WebApi_Django_RetrieveURLAndMethodInfo | Retrieves the method's route path, name, location, and request type (GET, POST, PUT or DELETE). | General |
| Django | Python_WebApi_Django_RetrieveResponseType | Retrieves method details related to response type, structure, and HTTP status code. | General |
| Django | Python_WebApi_Django_RetrieveRequestInfo | Retrieves method parameters, their name, data type, data structure, and source code location (line and file name), and determines if they serve as framework arguments. | General |
| Flask | Python_Flask_WebApi_GetApiList | This is the main query and returns the list of endpoint information. | Executable |
| Flask | Python_WebApi_Flask | Retrieves all the endpoints in Flask. | General |
| Flask | Python_WebApi_Flask_CreateComment | Collects details for every endpoint and provides this information, including the URL, HTTP method, method name, method line, method row, response type, and request type. | General |
| Flask | Python_WebApi_Flask_RetrieveRequestInfo | Retrieves method parameters, their name, data type, data structure, and source code location (line and file name), and determines if they serve as framework arguments. | General |
| Flask | Python_WebApi_Flask_RetrieveResponseType | Retrieves method details related to response type, structure, and HTTP status code. | General |
| Flask | Python_WebApi_Flask_RetrieveURLAndMethodInfo | Retrieves the method's route path, name, location, and request type (GET, POST, PUT or DELETE). | General |

<details>

<summary>Limitations</summary>

This section aims to detail the limitations of supported frameworks.

**Django**

1. Django only considers specific imports, which are `from django.contrib import admin` and `from rest_framework import routers`.
2. Currently, we don’t support Generics with their own Generics for the method's response type. Therefore, in these cases, the response type is empty, for instance, `"type": ""`. See below example:

```
@app.route('/signup/', methods=['GET', 'POST'])
def signup(arr: List[Union[int, float]]) -> List[Union[int, float]:
```

</details>

This page provides relevant information about the current support for API security queries in the JavaScript language.

| **Language** | **Framework** | **Framework Support Details** | **Details Needed** |
|---|---|---|---|
| JavaScript | Express | • app.all()<br>• app.route()<br>• Route Paths, such as String Patterns, Regular Expressions, and Array.<br>• Route Handlers<br>• express.Router()<br>• app.get/post/put/delete() | The call and parameters |

Six queries support *Express* in SAST. The table below provides a brief overview of them.

| **Framework** | **Query Name** | **Description** | **Category** |
|---|---|---|---|
| Express | NodeJS_Express_WebApi_GetApiList | This is the main query and returns the list of endpoint information. | Executable |
| Express | NodeJS_WebApi_Express | Returns all the endpoints and their *url* (e.g., “url“: “api/Home“). | General |
| Express | NodeJS_WebApi_Express_CreateComment | Collects details for every endpoint and provides this information, including the URL, HTTP method, method name, method line, method row, response type, and request type. | General |
| Express | NodeJS_WebApi_Express_RetrieveURLandMethodInfo | Retrieves the method's route path, name, location, and request type (GET, POST, PUT or DELETE). | General |
| Express | NodeJS_WebApi_Express_RetrieveResponseType | Retrieves method details related to response type, structure, and HTTP status code. | General |
| Express | NodeJS_WebApi_Express_RetrieveRequestInfo | Retrieves method parameters, their name, data type, data structure, and source code location (line and file name), and determines if they serve as framework arguments. | General |

{% hint style="warning" %}
Due to a limitation in the SAST scanner, the default value *lazy_flow_max_depth_count* in projects where a single file contains many endpoints (e.g., 50 endpoints in a single file), endpoints past a certain point will not be shown. Please contact Checkmarx support to configure this default value to suit your needs.
{% endhint %}
