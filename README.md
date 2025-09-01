# Snippetbox Notes

## Wild Cards
- Try to avoid route overlaps like `/post/new/{id}` and `/post/{author}/latest` the http servemux will choose the most specific route but if it can't determine it will panic
- A wildcard at the end of a path with a trailing `...` will match everything at the end of the path
-   `/post/{path...}` will match `/post/a/b` etc. And can be accessed at `r.PathValue("path")`

## Method-based routing
- You can restrict routes by http Method by adding the method to the beginning of the route `mux.HandleFunc("POST /snippet/create", snippetCreatePost)`

## Customizing Responses
- Use `w.WriteHeader(201)` to change the header of the response. Normally, it is always 200.
- You can only use this method once per response.
- net/http has constants for status codes that we can use, like http.StatusCreated.
-  Any changes you make to the response header map after calling w.WriteHeader() or w.Write() will have no effect on the headers that the user receives.
-  Any functions where you see an io.Writer parameter, you can pass in your http.ResponseWriter and it can write to the HTTP response.
- Go content sniffs the response body with `http.DetectContentType()` function but it can't distinguish JSON from text/plain. So, you have to set it manually.
- The header map has Set(), Add(), Del(), Get() and Values() methods but it will always convert your value to Uppercase. If you don't want this you can 
edit the header directly as it is a `map[string][]string` like so `w.Header()["X-XSS-Protection"] = []string{"1; mode=block"}`

## Project Structure and Organization
