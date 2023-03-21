# Chapter 2

## Command line
- Debug
  - auto reload
  - debug mode
- host
- port
- with-threads

## Request-Response cycle
- Application context
  - current_app
    - Application instance of the active application
  - g
    - Application temporary storage
  - request
    - encapsulates the contents of an HTTP request sent by the client
  - session
    - Dictionary that the application can use to store values that are "remembered" between requests

## Request Dispatching
- app.url_map (A mapping of URLs to the view functions that handle them)
  - Map([<Rule '/' (HEAD, OPTIONS, GET) -> index>,
        <Rule '/static/<filename>' (HEAD, OPTIONS, GET) -> static>,
        <Rule '/user/<name>' (HEAD, OPTIONS, GET) -> user>])
  - '/static/<filename>' is a special route added by Flask to give access to static files

## Request Object
- form
  - A dictionary with all the form fields submitted with the request.
- args
  - A dictionary with all the arguments passed in the query string of the URL.
- values
  - A dictionary that combines the values in form and args.
- cookies
  - A dictionary with all the cookies included in the request.
- headers
  - A dictionary with all the HTTP headers included in the request.
- files
  - A dictionary with all the file uploads included with the request.
- get_data()
  - Returns the buffered data from the request body.
- get_json()
  - Returns a Python dictionary with the parsed JSON included in the body of the request.
- blueprint
  - The name of the Flask blueprint that is handling the request.
- endpoint
  - The name of the Flask endpoint that is handling the request. Flask uses the name of the view function as the endpoint name for a route.
- method
  - The HTTP request method, such as GET or POST.
- scheme
  - The URL scheme (http or https).
- is_secure()
  - Returns True if the request came through a secure (HTTPS) connection.
- host
  - The host defined in the request, including the port number if given by the client.
- path
  - The path portion of the URL.
- query_string
  - The query string portion of the URL, as a raw binary value.
- full_path
  - The path and query string portions of the URL.
- url
  - The complete URL requested by the client.
- base_url
  - Same as url, but without the query string component.
- remote_addr
  - The IP address of the client.
- environ
  - The raw WSGI environment dictionary for the request.


# Request Hooks
## Code execution before or after each request

- `before_request`: Registers a function to run before each request.
- `before_first_request`: Registers a function to run only before the first request is handled. This can be a convenient way to add server initialization tasks.
- `after_request`: Registers a function to run after each request, but only if no unhandled exceptions occurred.
- `teardown_request`: Registers a function to run after each request, even if unhandled exceptions occurred.

## Responses
- `make_response`: Takes one, two, or three arguments, the same values that can be returned from a view function, and returns an equivalent response object.

### Response Object
- `status_code`: The numeric HTTP status code.
- `headers`: A dictionary-like object with all the headers that will be sent with the response.
- `set_cookie()`: Adds a cookie to the response.
- `delete_cookie()`: Removes a cookie.
- `content_length`: The length of the response body.
- `content_type`: The media type of the response body.
- `set_data()`: Sets the response body as a string or bytes value.
- `get_data()`: Gets the response body.
- `abort`
- `redirect`

# Chapter 3 - Templates

## Business logic
Talks to the database.

## Presentation logic
Presents the data gathered to the browser.

## Rendering
The process that replaces the variables in the template file with actual values and returns a final response string.

## Filters
Mechanisms to modify the variables when rendering a page. For example: `Hello, {{ name|capitalize }}`.

- `safe`: Renders the value without applying escaping.
- `capitalize`: Converts the first character of the value to uppercase and the rest to lowercase.
- `lower`: Converts the value to lowercase characters.
- `upper`: Converts the value to uppercase characters.
- `title`: Capitalizes each word in the value.
- `trim`: Removes leading and trailing whitespace from the value.
- `striptags`: Removes any HTML tags from the value before rendering.



Control structures
    - if
        {% if user %}
            Hello, {{ user }}!
        {% else %}
            Hello, Stranger!
        {% endif %}

    - for
        <ul>
            {% for comment in comments %}
                <li>{{ comment }}</li>
            {% endfor %}
        </ul>

    - macros (similar to functions in Python)
        {% macro render_comment(comment) %}
            <li>{{ comment }}</li>
        {% endmacro %}
        
        <ul>
            {% for comment in comments %}
                {{ render_comment(comment) }}
            {% endfor %}
        </ul>

        # Macros stored in a file
        {% import 'macros.html' as macros %}
        <ul>
            {% for comment in comments %}
                {{ macros.render_comment(comment) }}
            {% endfor %}
        </ul>

    - include
    template inheritance








