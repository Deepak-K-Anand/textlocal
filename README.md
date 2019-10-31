## 📱 Textlocal API and External Services
Send SMS from Salesforce using **Textlocal API** and **External Services** with absolutely zero Apex!

![image](https://user-images.githubusercontent.com/3683725/67923343-951eb680-fbd3-11e9-86dc-382ae4dde69e.gif)

## 📝 Tasks: Textlocal
1.  Sign-up for a free Textlocal account. Visit - https://www.textlocal.in

2.  Generate an **API Key**.

3.  Visit the Developer Docs - https://api.textlocal.in/docs/sendsms to learn how you can send an SMS using a simple GET verb.

## 📝 Tasks: Salesforce
1.  Create a **Named Credential** with URL - `api.textlocal.in`

2.  Create a **Custom Setting** (_Hierarchy_) to store the _API Key_ and the name of the _Sender_: `TXTLCL` (_This is a constant_)

![image](https://user-images.githubusercontent.com/3683725/67922819-e8900500-fbd1-11e9-9253-abac9b5e7856.png)

3.  Register an **External Service** with below Swagger schema -
```json
{
  "swagger": "2.0",
  "info": {
    "title": "TextLocal Send SMS API",
    "description": "Send SMS from Salesforce using TextLocal",
    "version": "1.0.0"
  },
  "host": "api.textlocal.in",
  "schemes": [ "https" ],
  "paths": {
    "/send": {
      "get": {
        "produces": [ "application/json" ],
        "parameters": [
          {
            "in": "query",
            "name": "apikey",
            "type": "string",
            "required": true
          },
          {
            "in": "query",
            "name": "numbers",
            "type": "string",
            "required": true
          },
          {
            "in": "query",
            "name": "message",
            "type": "string",
            "required": true
          },
          {
            "in": "query",
            "name": "sender",
            "type": "string",
            "required": true
          }
        ],
        "responses": {
          "200": {
            "description": "Successful Operation",
            "schema": {
              "$ref": "#/definitions/Response"
            }
          }
        }
      }
    }
  },
  "definitions": {
    "Response": {
      "type": "object",
      "properties": {
        "balance": {
          "type": "integer",
          "format": "int64"
        },
        "status": {
          "type": "string"
        }
      }
    }
  }
}
```

> Note: To **validate** a Swagger Schema (_written by yourself_), visit - http://editor.swagger.io/

4.  Create a **Flow** to consume the External Service as an _Apex Action_: 
    ![image](https://user-images.githubusercontent.com/3683725/67922885-0fe6d200-fbd2-11e9-878f-888a81d11053.png)
    ![image](https://user-images.githubusercontent.com/3683725/67922913-2725bf80-fbd2-11e9-8f74-44f5dddef8d0.png)
    ![image](https://user-images.githubusercontent.com/3683725/67922934-373d9f00-fbd2-11e9-993a-ee88ceccc967.png)

5.  **Activate** the Flow.

## 📚 Resources
What if I want to learn more about **External Services**. Visit - https://trailhead.salesforce.com/en/content/learn/modules/external-services
