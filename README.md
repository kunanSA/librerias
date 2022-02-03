
# API v8 de SuiteCrm
![Image text](https://suitecrm.com/wp-content/uploads/2017/12/logo.png)

Proyecto con SuiteCrm incluido a modo de prueba para integraciones con paquetes y integraciones 

## Tecnologias utilizadas
Listado de lenguajes utilizados para la integracion de API v8:
* [PHP](https://example.com): Version 7.3.+
* [Lib. Slim](https://www.slimframework.com): Version ^3.8

## Tabla de contenidos
1. [Autenticacion](#1-autenticacion)
2. [Consumo](#2-consumo)
* [Endpoints](#21-endpoints)

#### 1. Autenticacion
La API de SuiteCRM requiere que un cliente tenga una sesión activa para consumir la API. Las sesiones se adquieren mediante la autenticación con el Servidor OAuth 2, utilizando uno de los tipos de subvención disponibles. SuiteCRM Api permite dos tipos de subvenciones:

- Credencial de cliente `client_credentials`
- Contraseña `password`

##### Concesión de credenciales de cliente
Una concesión de credenciales de cliente es el más simple de todos los tipos de concesión, esta concesión se utiliza para autenticar una máquina o servicio. Es decir, la clave es asociada a un usuario del crm (puede tener reglas de seguridad con sus roles especificos), y el mismo por cada inicio de sesion. Generara una sesion de token, que perdura 1 h de tiempo.
> Este metodo es ideal para sistemas automatizados que deban ingresar al crm y realizar lectura o cambios en los modulos, segun lo solicitado
> Se puede crear un usuario de tipo *Usuario de Grupo*, la cual consiste en tener un usuario de maquina sin contraseña. Solo para tareas especificas de acceso maquina, con sus respectivas autorizaciones.

##### Concesión de contraseña
Se utiliza una concesión de contraseña para permitir que los usuarios inicien sesión en SuiteCRM con un nombre de usuario y una contraseña. Esto quiere decir que un token de contraseña es generado para que todos los usuarios de crm, utilicen un unico token de acceso sin renovación, para loguearse a suite las veces necesarias que crean correspondientes.

#### 2. CONSUMO
Para realizar el consumo de este metodo y probar el primer login, se debera realizar un envio de parametros al siguiente link.

>**LOGIN**
>```http
> https://[URL_WEB]/Api/access_token
>```
Metodo `POST`: _(Datos a modo de ejemplo)_
```json
{
    "grant_type" : "client_credentials",
    "client_id" : "530a0594-5742-f077-edd0-60e72ad3aa95",
    "client_secret" : "bmk123"
}
```

**Consumo habilitado**
- [x]  Todos los modulos
- [x]  Modulos custom
- [ ]  Consumos personalizados _(Endpoints custom se debe solicitar)_

#### 2.1 Endpoints
| Modulo | Metodos | Url | Filtro |
| ------ | ------ | ------ | ------ |
| Ver todos los modulos | GET | ` {{suiteCRM.url}}/Api/V8/meta/modules ` | - |
| Ver campos de un modulo | GET | ` {{suitecrm.url}}/V8/meta/fields/Accounts ` | - |
| Ver por id en Modulo | GET | ` {{suitecrm.url}}/Api/V8/module/{moduleName}/{id} ` | `Api/V8/module/Accounts/11a71596-83e7-624d-c792-5ab9006dd493?fields[Accounts]=name,account_type` |






## API Referencias
### A tener en cuenta!
Antes de relizar cualquier peticion, se debera enviar a de la siguiente formma:
```http
'Content-type: application/vnd.api+json',
'Accept: application/vnd.api+json',
'Authorization: Bearer {CLAVE_TOKEN_RECIBIDA}'
```


#### Crear un registro

```http
  POST {{suitecrm.url}}/V8/module
```

| Parametros | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `Bearer` | `string` | **Requerido**. Tu clave de sesion |

Cuerpo a enviar `JSON`
```json
{
  "data": {
    "type": "Accounts",
    "attributes": {
      "name": "Muhahaha"
    }
  }
}
```
Los campos contenidos en `attributes`, pueden ser cualquier campo que contenga el modulo. En caso de la carga de relaciones, se trata de otro modo.

#### > _Respuesta_
Al enviar el cuerpo de informacion, se recibira como respuesta un formato similar con la diferencia que recibira el `id` del registro creado y los `attributes` enviados y precargados que contiene el registro. Dicho registro tambien crea los registros de modulos relacionados:
```json
{
    "data": {
        "type": "Account",
        "id": "6222e8e6-bf0a-2495-3c37-61fbf50c49a6",
        "attributes": {
            "name": "Muhahaha",
            "date_entered": "2022-02-03T15:32:00+00:00",
            "date_modified": "2022-02-03T15:32:00+00:00",
            "modified_user_id": "2c530fe4-f235-9ad2-9398-611ff623aa1b",
            "modified_by_name": "Demo",
            "created_by": "2c530fe4-f235-9ad2-9398-611ff623aa1b",
            "created_by_name": "Demo",
            "description": "",
            "deleted": "0",
            "created_by_link": "",
            "modified_user_link": "",
            "assigned_user_id": "",
            "assigned_user_name": "",
            "assigned_user_link": "",
            "SecurityGroups": "",
            "account_type": "",
            "industry": "",
            "annual_revenue": "",
            "phone_fax": "",
            "billing_address_street": "",
            "billing_address_street_2": "",
            "billing_address_street_3": "",
            "billing_address_street_4": "",
            "billing_address_city": "",
            "billing_address_state": "",
            "billing_address_postalcode": "",
            "billing_address_country": "",
            "rating": "",
            "phone_office": "",
            "phone_alternate": "",
            "website": "",
            "ownership": "",
            "employees": "",
            "ticker_symbol": "",
            "shipping_address_street": "",
            "shipping_address_street_2": "",
            "shipping_address_street_3": "",
            "shipping_address_street_4": "",
            "shipping_address_city": "",
            "shipping_address_state": "",
            "shipping_address_postalcode": "",
            "shipping_address_country": "",
            "email1": "",
            "email_addresses_primary": "",
            "email_addresses": "",
            "email_addresses_non_primary": "",
            "parent_id": "",
            "sic_code": "",
            "parent_name": "",
            "members": "",
            "member_of": {},
            "email_opt_out": "",
            "invalid_email": "",
            "cases": "",
            "email": "",
            "tasks": "",
            "notes": "",
            "meetings": "",
            "calls": "",
            "emails": "",
            "documents": "",
            "bugs": "",
            "contacts": "",
            "opportunities": "",
            "project": "",
            "leads": "",
            "campaigns": "",
            "campaign_accounts": {},
            "campaign_id": "",
            "campaign_name": "",
            "prospect_lists": "",
            "aos_quotes": "",
            "aos_invoices": "",
            "aos_contracts": "",
            "accounts_contacts_1": "",
            "jjwg_maps_address_c": "",
            "jjwg_maps_lng_c": "0.00000000",
            "botmaker_canal_c": "crm",
            "telefono_wap_c": "",
            "jjwg_maps_lat_c": "0.00000000",
            "jjwg_maps_geocode_status_c": "",
            "test_c": ""
        },
        "relationships": {
            "AOS_Contracts": {
                "links": {
                    "related": "V8/module/6222e8e6-bf0a-2495-3c37-61fbf50c49a6/relationships/aos_contracts"
                }
            },
            "AOS_Invoices": {
                "links": {
                    "related": "V8/module/6222e8e6-bf0a-2495-3c37-61fbf50c49a6/relationships/aos_invoices"
                }
            },
            "AOS_Quotes": {
                "links": {
                    "related": "V8/module/6222e8e6-bf0a-2495-3c37-61fbf50c49a6/relationships/aos_quotes"
                }
            },
            "Accounts": {
                "links": {
                    "related": "V8/module/6222e8e6-bf0a-2495-3c37-61fbf50c49a6/relationships/members"
                }
            },
            "Bugs": {
                "links": {
                    "related": "V8/module/6222e8e6-bf0a-2495-3c37-61fbf50c49a6/relationships/bugs"
                }
            },
            "Calls": {
                "links": {
                    "related": "V8/module/6222e8e6-bf0a-2495-3c37-61fbf50c49a6/relationships/calls"
                }
            },
            "CampaignLog": {
                "links": {
                    "related": "V8/module/6222e8e6-bf0a-2495-3c37-61fbf50c49a6/relationships/campaigns"
                }
            },
            "Cases": {
                "links": {
                    "related": "V8/module/6222e8e6-bf0a-2495-3c37-61fbf50c49a6/relationships/cases"
                }
            },
            "Contacts": {
                "links": {
                    "related": "V8/module/6222e8e6-bf0a-2495-3c37-61fbf50c49a6/relationships/accounts_contacts_1"
                }
            },
            "EmailAddress": {
                "links": {
                    "related": "V8/module/6222e8e6-bf0a-2495-3c37-61fbf50c49a6/relationships/email_addresses"
                }
            },
            "Emails": {
                "links": {
                    "related": "V8/module/6222e8e6-bf0a-2495-3c37-61fbf50c49a6/relationships/emails"
                }
            },
            "Leads": {
                "links": {
                    "related": "V8/module/6222e8e6-bf0a-2495-3c37-61fbf50c49a6/relationships/leads"
                }
            },
            "Meetings": {
                "links": {
                    "related": "V8/module/6222e8e6-bf0a-2495-3c37-61fbf50c49a6/relationships/meetings"
                }
            },
            "Notes": {
                "links": {
                    "related": "V8/module/6222e8e6-bf0a-2495-3c37-61fbf50c49a6/relationships/notes"
                }
            },
            "Opportunities": {
                "links": {
                    "related": "V8/module/6222e8e6-bf0a-2495-3c37-61fbf50c49a6/relationships/opportunities"
                }
            },
            "Project": {
                "links": {
                    "related": "V8/module/6222e8e6-bf0a-2495-3c37-61fbf50c49a6/relationships/project"
                }
            },
            "ProspectLists": {
                "links": {
                    "related": "V8/module/6222e8e6-bf0a-2495-3c37-61fbf50c49a6/relationships/prospect_lists"
                }
            },
            "SecurityGroups": {
                "links": {
                    "related": "V8/module/6222e8e6-bf0a-2495-3c37-61fbf50c49a6/relationships/SecurityGroups"
                }
            },
            "Tasks": {
                "links": {
                    "related": "V8/module/6222e8e6-bf0a-2495-3c37-61fbf50c49a6/relationships/tasks"
                }
            },
            "Users": {
                "links": {
                    "related": "V8/module/6222e8e6-bf0a-2495-3c37-61fbf50c49a6/relationships/modified_user_link"
                }
            }
        }
    }
}
```

```http
  GET /api/items/${id}
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `string` | **Required**. Id of item to fetch |

#### add(num1, num2)

Takes two numbers and returns the sum.

## Autor

- [@gassalta](https://github.com/gassalta)


## Documentacion
Links oficiales de documentacion que se utilizo de referencia para elaborar la actual información.

[API V8 Documentacion](https://docs.suitecrm.com/developer/api/developer-setup-guide/)

[API V8 Custom](https://docs.suitecrm.com/developer/api/developer-setup-guide/customization/)

