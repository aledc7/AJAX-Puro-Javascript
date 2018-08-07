# AJAX-Puro-Javascript
###### código de ejemplo de uso de AJAX utilizando solo Javascript, sin hacer uso de jquery.


###### A continuación les comparto un ejemplo probado y funcionando de AJAX con Javascript PURO.

-[x] AleDC
-[x] SAP-TFI UAI



```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Ajax - Puro Javascript - AleDC</title>


    <script>
        // declaro la variable Global donde voy a instanciar el XMLHttpPequest.
        var peticionHTTP;


        // esta funcion inicializa el objeto XMLHttpRequest en la variable llamada "PeticionHTTP", declarada globalmente antes de esta función.

        function inicializar_XMLHttpRequest() {
            if (window.XMLHttpRequest)
                peticionHTTP = new XMLHttpRequest();
            // este else es para navegadores viejos que no soporten XMLHttpRequest, en ese caso se usará ActiveXObject.    
            else peticionHTTP = new ActiveXObject("Microsoft.XMLHTTP");
        }



        // esta funcion necesita 3 parametros: la URL, el METODO, y la Funcion de Respuesta
        function realizarPeticion(url, metodo, funcion) {

            //aca verifico el cámbio de estado y si está ok se procede con alguna funcion.
            peticionHTTP.onreadystatechange = funcion;

            // aca abro la peticion a la api, pasandole como mínimo, la URL y el Método HTTP, que siempre va a ser true de "Asyhnchronous".
            peticionHTTP.open(metodo, url, true);

            //esto no lo explicó aún.
            peticionHTTP.send(null);
        }


        //hace una llamada a la funcion realizarPeticion(url,método,funcion)
        function descargarArchivo() {

            //inicializa el objeto para usar el XMLHttpRequest
            inicializar_XMLHttpRequest();

            //aca hace el llamado a la supuesta API, que en este caso es un archivo.txt
            realizarPeticion('http://chatbot.baitsoftware.com/api/DialogMessages', 'GET', funcActuadora);
        }



        function funcActuadora() {

            alert('Actuando FuncActuadora');

            //verifico el estado de la peticion, tiene que ser 4.  [1 = CargaNdo] , [2 = Cargado!] , [3 = Interactivo] , [4 = Copmpleto]
            if (peticionHTTP.readyState == 4)


                // verifica el código del status HTTP, tiene que dar 200. [200 = OK] , [300 = Redirección] , [400 = Not Found] , [500 = Error Servidor]
                if (peticionHTTP.status == 200)

                    // si los dos if anteriores son verdaderos recién ahora ejecuta la sentencia de abajo que registra en el console log la respuesta de la API.
                    console.log(peticionHTTP.responseText);
        }


        // la funcion descargaArchivo es la que dispara todas las acciones, se ejecuta cuando la página terminó de cargar, usando windows.onload.
        window.onload = descargarArchivo;
    </script>



</head>
<body>
</body>

</html>

```
