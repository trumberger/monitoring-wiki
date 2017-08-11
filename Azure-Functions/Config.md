## Description
TODO.. 

## Retrieve Configuration item 
**Method: GET**
`https://fun-custint-{Service-ID}.azurewebsites.net/api/config?code={FunctionKey}`

|Name          |Value        |
|-------------|------------|
|Service-ID   |Unique ID that represents the Service. The Service ID is created during customer activation. |
|functionKey| Key used to authenticate requests. | 

**Request Body**
`{ "name": "{setting}" }`

**Return Body**
`{ "name": "{setting}", "value": "{result}" }`

## Set Configuration item 
**Method: POST**
`https://fun-custint-{Service-ID}.azurewebsites.net/api/config?code={FunctionKey}`

|Name          |Value        |
|-------------|------------|
|Service-ID   |Unique ID that represents the Service. The Service ID is created during customer activation. |
|functionKey| Key used to authenticate requests. | 

**Request Body**
`{ "name": "{setting}", "value": "{result}" }`

