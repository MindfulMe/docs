# Docs

**DAMP API**
----
  _The API provides access to creating new accounts in XOV database, fetching XOV deposit address for the requested account, checking whether account is restricted or not, and also adding additional inforamtion to the XOV account (which is then stored in mysql (MariaDB) table._

* **damp.xov.io/api**

  <_/api/init_>

* **Method:**
  
  <_The request type_>

  `POST`
  
*  **URL Params**

   _The request bundle is sent via post request body, no url params._ 

   **Required:**
 
   `no required parameters`

   **Optional:**
 
   `no optional parameters`

* **Data Params**

  _The request bundle is sent via post request body._
  
    **Required:**
 
   `name: [string]`

   **Optional:**
 
   `no optional parameters`


* **Success Response:**
  
  <_What should the status code be on success and is there any returned data? This is useful when people need to to know what their callbacks should expect!_>

  * **Code:** 200 <br />
    **Content:** `{ id : 12 }`
 
* **Error Response:**

  <_Most endpoints will have many ways they can fail. From unauthorized access, to wrongful parameters etc. All of those should be liste d here. It might seem repetitive, but it helps prevent assumptions from being made where they should be._>

  * **Code:** 401 UNAUTHORIZED <br />
    **Content:** `{ error : "Log in" }`

  OR

  * **Code:** 422 UNPROCESSABLE ENTRY <br />
    **Content:** `{ error : "Email Invalid" }`

* **Sample Call:**

  <_Just a sample call to your endpoint in a runnable format ($.ajax call or a curl request) - this makes life easier and more predictable._> 

* **Notes:**

  <_This is where all uncertainties, commentary, discussion etc. can go. I recommend timestamping and identifying oneself when leaving comments here._> 
  
  
  
**Show User**
----
  Returns json data about a single user.

* **URL**

  /users/:id

* **Method:**

  `GET`
  
*  **URL Params**

   **Required:**
 
   `id=[integer]`

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 <br />
    **Content:** `{ id : 12, name : "Michael Bloom" }`
 
* **Error Response:**

  * **Code:** 404 NOT FOUND <br />
    **Content:** `{ error : "User doesn't exist" }`

  OR

  * **Code:** 401 UNAUTHORIZED <br />
    **Content:** `{ error : "You are unauthorized to make this request." }`

* **Sample Call:**

  ```javascript
    $.ajax({
      url: "/users/1",
      dataType: "json",
      type : "GET",
      success : function(r) {
        console.log(r);
      }
    });
  ```
