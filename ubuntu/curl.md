GET:

with JSON:

    curl -i -H "Accept: application/json" -H "Content-Type: application/json" http://hostname/resource

with XML:

    curl -H "Accept: application/xml" -H "Content-Type: application/xml" -X GET http://hostname/resource

POST:

For posting data:

    curl --data "param1=value1&param2=value2" http://hostname/resource

For file upload:

    curl --form "fileupload=@filename.txt" http://hostname/resource

RESTful HTTP Post:

    curl -X POST -d @filename http://hostname/resource

For logging into a site (auth):

    curl -d "username=admin&password=admin&submit=Login" --dump-header headers http://localhost/Login
    curl -L -b headers http://localhost/

