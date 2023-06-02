# adm-devsec-test

Здравствуйте, в данном тестовом задание выполнено все, кроме создания и редактирования через API.
Как можно заметить запросы на создания и редактирования созданны корректно и по примеру, но от сервера приходит ошибка.

# Код запроса 
```Запрос для создания приложения
$.ajax({
                type: "POST",
                url: "http://checkstatus.website:8099/Face/New_app",
                contentType: "application/json; charset=utf-8",
                data: JSON.stringify({
                    "app_id": appAlias,
                    "app_name": appName,
                    "policy_id": appPolicy,
                    "agent_js_config": "123123",
                    "correlations_config": "321321"
                }),
                success: function (data) {
                    if (data.error === "0") {
                        $("#modalAdd").modal("hide");
                        getAppList();
                    } else {
                        $("#add-error").text("Ошибка при добавлении приложения");
                    }
                },
                error: function (xhr, status, error) {
                    console.log("Ошибка при выполнении запроса:", error);
                }
            });
```
вот что отправляет данный зарос 
```
{"app_id":"abc123","app_name":"example_name","policy_id":"14","agent_js_config":"123123","correlations_config":"321321"}
```
пример API в тестовом задание 
```
POST /Face/New_app HTTP/1.1
Host: checkstatus.website:8099
Content-Type: application/json; charset=utf-8
Content-Length: 124

'{"app_id": "abc", "app_name": "test_app", "policy_id": 10, "agent_js_config": "123123", "correlations_config": "321321"}'
```
вот какую ошибку отправляет сервер
```
{
   "errors":{
      "":[
         "Unexpected character encountered while parsing value: {. Path '', line 1, position 1."
      ]
   },
   "type":"https://tools.ietf.org/html/rfc7231#section-6.5.1",
   "title":"One or more validation errors occurred.",
   "status":400,
   "traceId":"00-ae65d3d8b86a499d6bc0bf5baa0eef52-d16e2f0f5dcb2cc8-00"
}
```
точно также и с запросом на редактирование
```
   $.ajax({
                type: "POST",
                url: "http://checkstatus.website:8099/Face/Update_app",
                contentType: "application/json; charset=utf-8",
                data: JSON.stringify({
                    "app_id": appAlias,
                    "app_name": appName,
                    "policy_id": appPolicy,
                    "agent_js_config": "123123",
                    "correlations_config": "321321"
                }),
                success: function (data) {
                    if (data.error === "0") {
                        $("#modal").modal("hide");
                        getAppList();
                    } else {
                        alert("Ошибка при изменении приложения");
                    }
                },
                error: function (xhr, status, error) {
                    console.log("Ошибка при выполнении запроса:", error);
                }
            });
```
что отправляет данный запрос 
```
{"app_id":"abc","app_name":"test_app_123","policy_id":"122","agent_js_config":"123123","correlations_config":"321321"}
```
пример API в тестовом задание 
```
POST /Face/Update_app HTTP/1.1
Host: checkstatus.website:8099
Content-Type: application/json; charset=utf-8
Content-Length: 124

'{"app_id": "abc", "app_name": "test_app", "policy_id": 11, "agent_js_config": "123123", "correlations_config": "321321"}'
```
ответ такой же как и при запросе на создание 
```
{
   "errors":{
      "":[
         "Unexpected character encountered while parsing value: {. Path '', line 1, position 1."
      ]
   },
   "type":"https://tools.ietf.org/html/rfc7231#section-6.5.1",
   "title":"One or more validation errors occurred.",
   "status":400,
   "traceId":"00-ae65d3d8b86a499d6bc0bf5baa0eef52-d16e2f0f5dcb2cc8-00"
}
```
