`In this article, we are going to learn about different return types that we can use with ASP.NET Core Web API controller actions.`

`ASP.NET Core Web API allows us to return different types from the controller action methods:`

1. **Specific Types**
2. **IActionResult**
3. **ActionResult<T>** 
  
### 1. Specific Return Types
  
`In its simplest form, an ASP.NET Core Web API controller action can just return a specific type like a string or a custom entity. Let’s consider a simple controller action method that returns the list of all Customer:`

**Example 1:**
  
<pre>
  [HttpGet]
public List<Customer> Get() =>
    _repository.GetCustomers();
 </pre>

`This action will return a 200 Ok status code along with a collection of Customer objects when it runs successfully. Of course, in case of errors, it will return a 500 Error status code along with error details. Even while generating API documentation using tools like Swagger, it will generate this possible successful outcome in the Responses section.  Since the action doesn’t have any validations or multiple return paths, returning a specific type work well here.`


**Example 2:**

<pre>
        [HttpGet]
        [Route("[action]")]
        public async Task<ResponseMessage> GetMessageUsersByUserId(int id)
        {
            try
            {
                return new ResponseMessage(HttpStatusCode.OK, true, "Success", await _chatServices.GetMessageUsers(id));
            }
            catch (Exception ex)
            {
                Log.Error("An error occurred while seeding the database  {Error} {StackTrace} {InnerException} {Source}", ex.Message, ex.StackTrace, ex.InnerException, ex.Source);
                return new ResponseMessage(HttpStatusCode.NotAcceptable, false, ex.Message, null);
            }
        }
</pre>


### 2. 
