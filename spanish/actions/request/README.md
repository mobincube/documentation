# Acción REQUEST
  
Realiza una llamada https. Puede usarse para intercambiar información con un servidor, acceder a APIs de terceros, etc.
    
## Parámetro
  
Para realizar llamadas GET de forma sencilla, simplemente introduce la URL. Se aceptan parámetros en la propia URL. Pueden usarse variables para sustituirse con información de la app.
  
**Ejemplo:**

    https://miservidor.com?nombre={var.name}



Puedes realizar llamadas más complejas. En ese caso, el parámetro debe ser un objeto JSON con la siguiente estructura:


    {
        "request": {
            "method": "GET|POST",
            "url": "[url]",
            "token": "[bearer_token_opcional]]",
            "body": {
                ...
            }
        },
        "result": "[ruta_dentro_del_json_de_respuesta_donde_se_encuentra_el_valor]",
        "into": "[var_o_cookie_donde_guardar_el_resultado",
        "onsuccess": {
            "action": "[action_a_ejecutar_si_la_llamada_es_exitosa]",
            "parameter": "[parámetro_de_la_action]"
        },
        "onerror": {
            "action": "[action_a_ejecutar_si_la_llamada_es_errónea]",
            "parameter": "[parámetro_de_la_action]"
        }
    }

  
<br>
<br>
<br>
  
**Ejemplo:**
  

Uso de Doyo API para obtener el país a partir de una dirección IP:

    {
        "request": {
            "method": "POST",
            "url": "https://api.doyo.tech",
            "token": "abcdefghijk123456",
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
  

Uso de Doyo API para obtener datos de una base de datos remota MySQL:
  
    {
        "request": {
            "method": "POST",
            "url": "https://api.doyo.tech",
            "token": "[pon_tu_doyo_api_key_aqui]",
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