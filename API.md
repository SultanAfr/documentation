* **Основной URL:**

http://api.afr.kz/api

* **Headers:**
  
  Обязательно указывайте:
  
  `Content-Type`: `application/x-www-form-urlencoded`
  
  `Accept`: `application/json` 

**Регистрация**
----

Регистрация и привязка к БИН-у.



* **URL**

    /auth/register

* **Method:**

  `POST`

*  **URL Params**

    none

* **Data Params**

  **Required:**
    
  `name[string]` - имя
  
  `email[string]` - email, будет использован при авторизации
  
  `password[string]` - пароль минимум 6 символов
  
  `c_password[string]` - повторный пароль
  
  `bin[integer]` - ваш БИН 12 цифр
  
  **Optional:**
  
  none

* **Success Response:**
  
  * **Code:** 200 <br />
    **Content:** `"data": {
                          "token": "eyJ0eXAiOiJKV1QiLC2YzY2Y2VkIn0.eyJhdWQiOiIxIiwianRp..."
                      }`
 
* **Error Response:**

  * **Code:** 422 UNPROCESSABLE ENTRY <br />
    **Content:** `"error": {
                          "bin": [
                              "The bin must be at least 12 characters."
                          ]
                      }`
                      
**Авторизация**
----

Логин. Используется JWT авторизация.

* **URL**

    /auth/login

* **Method:**

  `POST`

*  **URL Params**

    none

* **Data Params**

  **Required:**
  
  `email[string]`
  
  `password[string]`
  
  **Optional:**
  
  none

* **Success Response:**
  
  * **Code:** 200 <br />
    **Content:** `"data": {
                          "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0a..."
                      }`
 
* **Error Response:**

  * **Code:** 422 UNPROCESSABLE ENTRY <br />
    **Content:** `"error": "Incorrect email or password."`
    
* **Заметка:**

    Полученный токен используется при каждом запросе требующим аутентификацию. Его необходимо указывать в header-е:
    
    `Authorization`: `Bearer {ваш токен}`
    
**Logout**
----

* **URL**

    /auth/logout

* **Method:**

  `POST`

*  **URL Params**

    none

* **Data Params**
  
    none

* **Success Response:**
  
  * **Code:** 200 <br />
    **Content:** `"message": "Successfully logged out."`
 
* **Error Response:**

  * **Code:** 401 UNAUTHENTICATED <br />
    **Content:** `"error": "Unauthenticated."`
    
**Информация о пользователе**
----

* **URL**

    /auth/info

* **Header**

   `Authorization`: `Bearer {токен полученный при авторизации}`

* **Method:**

  `GET`

*  **URL Params**

    none

* **Data Params**
  
    none

* **Success Response:**
  
  * **Code:** 200 <br />
    **Content:** `"data": {
                          "api_user_id": 7,
                          "name": "Test2",
                          "email": "test2@mail.ru",
                          "created_at": "2018-08-06 08:16:31",
                          "updated_at": "2018-08-06 08:16:31"
                      }`
 
* **Error Response:**

  * **Code:** 401 UNAUTHENTICATED <br />
    **Content:** `"error": "Unauthenticated."`
    
**Список HAWB**
----

* **URL**

    /hawb

* **Header**

   `Authorization`: `Bearer {токен полученный при авторизации}`

* **Method:**

  `GET`

*  **URL Params**

    `page`

* **Data Params**
  
    none

* **Success Response:**
  
  * **Code:** 200 <br />
    **Content:** `"data": [
                          {
                              "hawb_num": 1000000,
                              "aircompany": "Air Astana",
                              "departure_airport": "Алматы",
                              "destination_airport": "Астана",
                              "sender": "Рога и Копыта",
                              "receiver": "Рога и Копыта",
                              "departure_date": "2018-05-29 09:50:00",
                              "weight": 20,
                              "place_count": 2,
                              "description": "курьерский материал",
                              "total_tax": 7000,
                              "track_number": "AF6CF7E1887930KZ",
                              "places": [
                                  {
                                      "number": 1,
                                      "status": "Принят на склад в аэропорту назначения",
                                      "date": "2018-05-29 15:27:55.294814",
                                      "barcode": "0004434831"
                                  },
                                  {
                                      "number": 2,
                                      "status": "Принят на склад в аэропорту назначения",
                                      "date": "2018-05-29 15:27:55.294814",
                                      "barcode": "0005434832"
                                  }
                              ]
                          }
                      ],
                      "links": {
                          "first": "http://api.afr.kz/api/hawb?page=1",
                          "last": "http://api.afr.kz/api/hawb?page=20",
                          "prev": null,
                          "next": "http://api.afr.kz/api/hawb?page=2"
                      },
                      "meta": {
                          "current_page": 1,
                          "from": 1,
                          "last_page": 20,
                          "path": "http://api.afr.kz/api/hawb",
                          "per_page": 15,
                          "to": 15,
                          "total": 300
                      }`
 
* **Error Response:**

  * **Code:** 401 UNAUTHENTICATED <br />
    **Content:** `"error": "Unauthenticated."`
    
**HAWB по номеру накладной**
----

* **URL**

    /hawb/{number}

* **Header**

   `Authorization`: `Bearer {токен полученный при авторизации}`

* **Method:**

  `GET`

*  **URL Params**

    `number`

* **Data Params**
  
    none

* **Success Response:**
  
  * **Code:** 200 <br />
    **Content:** `"data": [
                          {
                              "hawb_num": 1100000,
                              "aircompany": "Air Astana",
                              "departure_airport": "Алматы",
                              "destination_airport": "Актау",
                              "sender": "Logistic co",
                              "receiver": "Logistic co",
                              "departure_date": "2018-06-09 10:15:00",
                              "weight": 60,
                              "place_count": 2,
                              "description": "курьерский материал",
                              "total_tax": 21000,
                              "track_number": "AF812A14532669KZ",
                              "places": [
                                  {
                                      "number": 1,
                                      "status": "Принят на склад в аэропорту назначения",
                                      "date": "2018-06-09 16:09:36.074459",
                                      "barcode": "0007454299"
                                  },
                                  {
                                      "number": 2,
                                      "status": "Принят на склад в аэропорту назначения",
                                      "date": "2018-06-09 16:09:36.074459",
                                      "barcode": "0001424300"
                                  }
                              ]
                          }
                      ]`
 
* **Error Response:**

  * **Code:** 401 UNAUTHENTICATED <br />
    **Content:** `"error": "Unauthenticated."`
    
  * **Code:** 404 NOT FOUND <br />
    **Content:** `"error": "Not found."`