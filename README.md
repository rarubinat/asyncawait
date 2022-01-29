# async await en Jquery y ajax



Función mediante ajax:
```
function myAjax() {
  $.ajax({
    url: ajaxurl,
    type: 'POST',
    data: {
      stuff: 'here',
    },
    success: function (data) {
      //Las locas respuestas de las peticiones anidadas van aquí
      var response = data
    },
    error: function (jqXHR, textStatus, errorThrown) {
      // Vacio casi siempre 😆
    },
  })
  return response
}
```
Si partimos del anterior código, un ejemplo de async/await con ajax podría ser:
```
async function myAjax(param) {
  const result = await $.ajax({
    url: ajaxurl,
    type: 'POST',
    data: param,
  })
  return result
}
```
Y es en el return donde devolvemos el resultado de la petición si no hubiera errores. Para capturar los errores podemos hacer lo siguiente:
```
async function myAjax(param) {
  let result
  try {
    result = await $.ajax({
      url: ajaxurl,
      type: 'POST',
      data: param,
    })
    return result
  } catch (error) {
    console.error(error)
  }
}
```
¿Como se resume esta función? Así:
```
// En otra parte del código, dentro de una función asíncrona
const data = await myAjax()
```
Otra opción sería usar promesas:
```
myAjax().then((data) => {
  console.info('Response:', data)
})
```
