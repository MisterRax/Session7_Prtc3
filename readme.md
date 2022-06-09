# Práctica de Innovaccion Sesión 7 No. 3

La práctica consiste en la realización de una plantilla de Azure mediante el uso de archivos .json e implementarlos en Azure usando el servicio de Azure CLI.

## Paso 1: VSC y creación de plantilla

Mediante Visual Studio Code, utilizando la extensión de Azure Resource Manager (ARM), creamos un documento con la extensión .json.

Una vez tenemos el archivo, escribimos el siguiente código: 

...
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": []
}
...

Una vez escritro el código, guardámos el archivo en una carpeta específica, en nuestro casso el archivo se llamará "azuredeploy.json".

## Paso 2: Azure CLI

El siguiente paso es abrir nuestro símbolo del sistema (en el caso de Windows) y movernos hasta llegar a la carpeta en dónde tengamos guardado el archivo .json que creamos en el paso anterior. ![][C2]

### **NOTA:** Es necesario iniciar sersión mediante el CLI con la extensión de Azure, esto se puede lograr mediante el comando:
... 
az login
...

Una vez estando en el CLI de Azure apuntando a la carpeta con el archivo .json, usamos la siguiente línea de comando para implementar la plantilla dentro del grupo de trabajo que queramos, en nuestro caso, el grupo se llama "Session7".

...
az deployment group create --name mi-primera-plantilla --resource-group Session7 --template-file azuredeploy.json
...

### **NOTA2:** Enseguida de "--name" cada uno puede asigar el nombre de la plantilla que guste. En "--resource-group" tenemos que escribir el grupo de recurso específico en donde lo queremos guardar. Por último, en "--template-file" escribimos el archivo de plantilla que queramos subir.
![][C3]

## Paso 3: Actualización

Una vez implementada la plantilla, tenemos que actualizarla, para ello vamos a cambiar el código del archivo .json para que quede de la siguiente maner:

...
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "apiVersion": "2021-09-01",
            "name": "ownstorage",
            "location": "Central US",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "StorageV2",
            "properties": {
                "supportsHttpsTrafficOnly": true
            }
        }
    ]
}
...

De esta forma, vamos a agregar una Storage Account a la plantilla para implementarla.

Después vamos a Azure CLI (en la misma ubicación anterior) y escribimos el siguiente comando:

...
az deployment group create --name mi-primera-plantilla --resource-group Session7 --template-file azuredeploy.json
...

Usando el nombre del archivo que modificamos anteriormente. ![][C5]

## **NOTA 3:** En el apartado "name": recueden usar un nombre original y que no haya sido tomado aún, esto evitará muchos errores. Además, se puede crear la plantilla del paso 3 directamente para después saltar al paso 2.


Como podemos ver, dentro de nuestro grupo de recursos de Azure, la plantilla ha sido creada correctamente. ![][Result]

Se puede acceder a ella desde el apartado Configuración -> Implementaciones.

[C2]: Images/Captura2.PNG
[C3]: Images/Captura3.PNG
[C5]: Images/Captura5.PNG
[Result]: Images/Captura6.PNG