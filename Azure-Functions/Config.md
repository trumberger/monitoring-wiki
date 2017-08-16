## Description
todo

## Retrieve Configuration item
todo

**Method: GET**
`https://fun-custint-{Service-ID}.azurewebsites.net/api/config?code={FunctionKey}`

|Name          |Value        |
|-------------|------------|
|Service-ID   |Unique ID that represents the Service. The Service ID is created during customer activation. |
|functionKey| Key used to authenticate requests. | 

**Parameter**
`{setting}`

**Return Body**
`{result}`

## Set Configuration item
todo

**Method: POST**
`https://fun-custint-{Service-ID}.azurewebsites.net/api/config?code={FunctionKey}`

|Name          |Value        |
|-------------|------------|
|Service-ID   |Unique ID that represents the Service. The Service ID is created during customer activation. |
|functionKey| Key used to authenticate requests. | 

**Request Body**
`{ "name": "{setting}", "value": "{result}" }`

