# Docs

**DAMP API**
----

**Get new address**
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
  
  ```javascript
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
        


* **Notes:**

  _The endpoint is supposed to be used to get new address for the reuqest bitshares account name in order to deposit new XOV tokens._
  
  
  
**Profile details**
----

  _The endpoint provides access to adding accounts details in XOV database._

* **damp.xov.io/api**

  _/api/details_

* **Method:**
  
  _The request type_

  `POST`

* **Sample Call:**

  _ReactJS example._
  
  ```javascript
         (async () => {
            const rawResponse = await fetch(
                "http://<api-origin>/api/details",
                {
                    method: "POST",
                    headers: {
                        Accept: "application/json, text/plain, */*",
                        "Content-Type": "application/json",
                        "X-Requested-With": "XMLHttpRequest",
                        'Access-Control-Allow-Origin': "<api-origin>"
                    },
                    body: JSON.stringify({
                        details: {
                            email: this.state.email,
                            birth: this.state.birth,
                            job: this.state.job,
                            income: this.state.income,
                            currency: this.state.favorite,
                            telegram: this.state.telegram,
                            country: this.state.country
                        }
                    })
                }
            );

            console.log(rawResponse);
        })();
        
        
**Limited accounts**
----

  _The endpoint provides access to limited accounts info from XOV database._

* **damp.xov.io/api**

  _/api/limited

* **Method:**
  
  _The request type_

  `POST`

* **Sample Call:**

  _ReactJS example._
  
  ```javascript
        (() => {
            fetch(
                "<origin>/api/limited",
                {
                    method: "POST",
                    headers: {
                        Accept: "application/json, text/plain, */*",
                        "Content-Type": "application/json",
                        "X-Requested-With": "XMLHttpRequest",
                        'Access-Control-Allow-Origin': "<origin>"
                    }
                }
            )
                .then(res => res.json())
                .then(response => {
                    console.log(response.accounts);
                    let accountsLength = response.accounts.length;
                    for (var i = 0; i < accountsLength; i++) {
                        if (
                            AccountStore.getState().currentAccount ==
                            response.accounts[i].account_name
                        ) {
                            this.setState({limited: true});
                        }
                    }
                }).catch((error) => console.log(error));
        })();
        

