# Docs

**DAMP API**
----
  _The API provides access to creating new accounts in XOV database, fetching XOV deposit address for the requested account, checking whether account is restricted or not, and also adding additional inforamtion to the XOV account (which is then stored in mysql (MariaDB) table._

* **damp.xov.io/api**

  _/api/init_

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
  
  _Returns address_

  * **Code:** 200 
    **Content:** `{ address : <very very long hash address> }`
 
* **Error Response:**

  _The possible error responses:_

  * **Code:** THE ADDRESS ALREADY IN USE BY AN OTHER BTS ACCOUNT (5501)
    **Content:** `{ address : "out of addresses (error 5501)" }`

  OR

  * **Code:** NEW ADDRESSES ARE NOT AVAILBLE AT THE MOMENT (5502)
    **Content:** `{ error : "out of addresses (error 5502)" }`

* **Sample Call:**

  _ReactJS example._
  ```
          (() => {
            fetch(
                "http://<api-base>/api/init",
                {
                    method: "POST",
                    headers: {
                        Accept: "application/json, text/plain, */*",
                        "Content-Type": "application/json",
                        "X-Requested-With": "XMLHttpRequest",
                        'Access-Control-Allow-Origin': "<api-base>"
                    },
                    body: JSON.stringify({
                        name: AccountStore.getState().currentAccount
                    })
                }
            )
                .then(res => res.json())
                .then(response => {
                    let address = response.address;
                    console.log(address);
                    this.setState({ true_address: address })
                });
        })();
        ```

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
