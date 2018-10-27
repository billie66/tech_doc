## Common Options

`-#, --progress-bar`
        Make curl display a simple progress bar instead of the more
informational standard meter.

`-b, --cookie <name=data>`
        Supply cookie with request. If no `=`, then specifies the cookie file
to use (see `-c`).

`-c, --cookie-jar <file name>`
        File to save response cookies to.

`-d, --data <data>`
        Send specified data in POST request. Details provided below.

`-f, --fail`
        Fail silently (don't output HTML error form if returned). 

`-F, --form <name=content>`
        Submit form data.

`-H, --header <header>`
        Headers to supply with request.

`-i, --include`
        Include HTTP headers in the output.

`-I, --head`
        Fetch headers only.

`-k, --insecure`
        Allow insecure connections to succeed.

`-L, --location`
        Follow redirects.

`-o, --output <file>`
        Write output to <file>. Can use `--create-dirs` in conjunction with
this to create any directories
        specified in the `-o` path.

`-O, --remote-name`
        Write output to file named like the remote file (only writes to
current directory).

`-s, --silent`
        Silent (quiet) mode. Use with `-S` to force it to show errors.

`-v, --verbose`
        Provide more information (useful for debugging).

`-w, --write-out <format>`
        Make curl display information on stdout after a completed transfer.
See man page for more details on
        available variables. Convenient way to force curl to append a newline
to output: `-w "\n"` (can add
        to `~/.curlrc`).

`-X, --request`
        The request method to use.


## POST

When sending data via a POST or PUT request, two common formats (specified via
the `Content-Type` header) are:
  * `application/json`
  * `application/x-www-form-urlencoded`

Many APIs will accept both formats, so if you're using `curl` at the command
line, it can be a bit easier to use the form urlencoded format instead of json
because
  * the json format requires a bunch of extra quoting
  * curl will send form urlencoded by default, so for json the `Content-Type`
    header must be explicitly set

This gist provides examples for using both formats, including how to use
sample data files in either format with your `curl` requests.

## curl usage

For sending data with POST and PUT requests, these are common `curl` options:

 * request type
   * `-X POST`
   * `-X PUT`

 * content type header
  * `-H "Content-Type: application/x-www-form-urlencoded"`
  * `-H "Content-Type: application/json"`

* data
  * form urlencoded: `-d "param1=value1&param2=value2"` or `-d @data.txt`
  * json: `-d '{"key1":"value1", "key2":"value2"}'` or `-d @data.json`

## Examples

### POST application/x-www-form-urlencoded

`application/x-www-form-urlencoded` is the default:

    curl -d "param1=value1&param2=value2" -X POST http://localhost:3000/data

explicit:

    curl -d "param1=value1&param2=value2" -H "Content-Type:
application/x-www-form-urlencoded" -X POST http://localhost:3000/data

with a data file

    curl -d "@data.txt" -X POST http://localhost:3000/data

### POST application/json

    curl -d '{"key1":"value1", "key2":"value2"}' -H "Content-Type:
application/json" -X POST http://localhost:3000/data

with a data file

    curl -d "@data.json" -X POST http://localhost:3000/data


