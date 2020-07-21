# Braze-mock-server

This offers a very simple way to setup a local Braze mock server with all the Braze endpoints mocked and the ability to send back custom responses if necessary.

## Setup

You'll need to install the [prism npm package](https://meta.stoplight.io/docs/prism/README.md) by

```bash
npm install -g @stoplight/prism-cli
```

And clone this repository locally and run

```bash
prism mock braze_swagger.json
```

If everything goes well, you should have a Braze mock server running locally.

Note that the braze_swagger.json file is based on the one provided by Braze at https://www.braze.com/docs/assets/js/swagger/braze_swagger.json

## Add custom responses

In order to add custom responses for various HTTP status codes, you'll need to edit the braze_swagger.json file and here are some simple examples:

* add a 200 response
```
  "200": {
    "description": "Sometimes seen as `success`, this code indicates that the request was successfully made.",
    "content": {
      "application/json": {
        "examples": {
          "success": {
            "value": {
              "message": "success"
            }
          }
        }
      }
    }
  }
```
* add a 400 response
```
  "400": {
    "description": "Simulating failure cases",
    "content": {
      "application/json": {
        "examples": {
          "failure": {
            "value": {
              "message": "Bad Request",
              "errors": [
                "required field `first_name` not present"
              ]
            }
          }
        }
      }
    }
  }
```

Since it confirms to the OpenAPI 3.0 specification, please refer to [the official documentation for OpenAPI](https://swagger.io/docs/specification/describing-responses/) for more information.
