## Presentation
This package is named `requestapigo`

## Example

### How to instanciate a new API connexion
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

### Full example
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

### "Special feature"
```go
// To have a full compatibility with old API, you can pass map[string]interface{} (like a JSON) to a GET request
func main() {
    // Full example

    // Init login data // Like a JSON
    data := map[string]interface{}{
        "email": "john.doe@example.com",
        "password": "qwerty123",
    }

    api := NewApi("https://api.example.com")

    apikey := api.GET("/login", &data)
    if(apikey == ""){
        fmt.Printf("Something went wrong")
        return
    }
    apiApiKey.AddApiKey(apikey)
}

```