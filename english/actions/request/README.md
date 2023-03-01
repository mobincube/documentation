# Action REQUEST
  
Makes a https request. It can be used to send and or receive data from a server, access 3rd party APIs, etc.
    
## Parameter
  
For making straight forward GET request, you can just use a URL as a parameter, which accepts parameters. You can use variables inside the URL to replace with some app's value:
  
**Example:**

    https://myserver.com?name={var.name}
    
<br>
  
You can also make more complex requests. In that case, the parameter must be a JSON object with the following structure:


    {
        "request": {
            "method": "GET|POST",
            "url": "[url]",
            "token": "[bearer_token_in_case_of_needed]]",
            "body": {
                ...
            }
        },
        "result": "[route_inside_the_json_response_where_the_expected_result_is]",
        "into": "[var_or_cookie_where_to_store_the_result",
        "onsuccess": {
            "action": "[action_to_perform_if_the_request_was_successful]",
            "parameter": "[parameter_of_the_action]"
        },
        "onerror": {
            "action": "[action_to_perform_if_the_request_was_erroneous]",
            "parameter": "[parameter_of_the_action]"
        }
    }

  
<br>
<br>
<br>
  
**Examples:**

Using the Doyo API to get the country from a IP address:  

    {
        "request": {
            "method": "POST",
            "url": "https://api.doyo.tech",
            "token": "[insert_your_doyo_api_key_here]",
            "body": {
                "provider": "countryis",
                "method": "fromIp",
                "parameters": {
                    "ip": "123.456.78.90"
                }
            }
        },
        "result": "result",
        "into": "var.country",
        "onsuccess": {
            "action": "section",
            "parameter": "main menu"
        },
        "onerror": {
            "action": "section",
            "parameter": "country not found"
        }
    }

<br>
  

Using the Doyo API to get data from a remote MySQL database:
  
    {
        "request": {
            "method": "POST",
            "url": "https://api.doyo.tech",
            "token": "[insert_your_doyo_api_key_here]",
            "body": {
                "provider": "mysql",
                "method": "select",
                "parameters": {
                    "select": "*",
                    "table": "players",
                    "order_by": "name",
                    "order_direction": "ASC"
                }
            }
        },
        "result": "result",
        "into": "db.players",
        "onsuccess": {
            "action": "section",
            "parameter": "playerlist"
        },
        "onerror": {
            "action": "section",
            "parameter": "loaderro"
        }
    }

<br>
  

Using the Doyo API to write data into a remote MySQL database:
  
    {
        "request": {
            "method": "POST",
            "url": "https://api.doyo.tech",
            "token": "[insert_your_doyo_api_key_here]",
            "body": {
                "provider": "mysql",
                "method": "insert",
                "parameters": {
                    "table": "players",
                    "values": {
                        "{}": "{}",
                        "name": "{var.name}",
                        "team": "{var.team}",
                        "country": "{var.country}"
                    }
                }
            }
        },
        "result": "result",
        "onsuccess": {
            "action": "section",
            "parameter": "playerlist"
        },
        "onerror": {
            "action": "section",
            "parameter": "loaderro"
        }
    }