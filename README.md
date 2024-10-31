# RequestApis
A collection of files allowing you to request the API of your choice.

## Presentation
The goal of this repository is to centralize useful resources for developers working with APIs in various programming languages.

## Structure
Each language has its own folder containing:

- A README file with language-specific explanations
- Code examples for different types of requests (GET, POST, PUT, PATCH, DELETE)

## Functionnalities
- Request any APIs
- Add different auth system (Basic Auth, Apikey, BearerToken)
- Simple use

## Example
```go

func main() {
    

    // Without auth
    apiNoAuth := NewApi("https://api.example.com")
    

    // ------ With Basic Auth ------
    apiBasicAuth := NewApi("https://api.example.com")
    apiBasicAuth.AddBasicAuth("username", "password")


    // ------------------------------------------- //


    // Example Data to login
    data := map[string]interface{}{
        "email": "john.doe@example.com",
        "password": "AZERTY",
    }

    // ------ With apiKey ------
    apiApiKey := NewApi("https://api.example.com")
    resultString := apiApiKey.POST("/login", data) // Use the request method expected by the API
    // Parse the resultString, to extract the apikey and put it inside the following function
    apiApiKey.AddApiKey("apikey")
    

    // ------ With Bearer Token ------
    apiBearerToken := NewApi("https://api.example.com")
    resultString := apiBearerToken.POST("/login", data)  // Use the request method expected by the API
    // Parse the resultString, to extract the bearer token and put it inside the following function
    apiBearerToken.AddBearerToken("bearer-token")
    

    // ------------------------------------------- //


    // Using the package
    response, err := api.GET("/endpoint")
    if err != nil {
        log.Fatal(err)
    }
    fmt.Println(response)
}

```


```go
func main() {
    
    // Init login data // Like a JSON
    data := map[string]interface{}{
        "email": "john.doe@example.com",
        "password": "qwerty123",
    }

    api := NewApi("https://api.example.com")

    apikey := api.POST("/login", data)
    apiApiKey.AddApiKey(apikey)

    data = map[string]interface{}{
        "name": "Doe",
        "firstname": "John",
        "phone":"0000000000"
    }

    // Call any request with any METHOD
    response, err := api.PUT("/users", data)
    if err != nil {
        log.Fatalf("Error when requesting users : %v", err)
    }

    fmt.Println("API response :", response)
}

```

## License
This project is under the MIT License.
