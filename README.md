# Mongodb Polymer CRUD
This is the second presentation covering google polymer.  At this point, I am expecting you understand how to get the polymer project and Mongolab database setup.

#Polymer 1.0
Setup the polymer project 1.0 (*link below*)

#Iron Ajax 
Add the utility element from the polymer catalog (*link below*)

#MongoLab
Setup an account with Mongolab (*link below*)


##Overview of iron-ajax 	

Google states that iron-ajax makes it easy to make ajax calls and parse the response.

The iron-ajax element exposes *XMLHttpRequest* network request functionality.

**Include import for the iron-ajax web component to your custom element **

```
  <link rel="import" href="../iron-ajax.html">
```

**Add the iron-ajax web component to your html document**

```html
  <iron-ajax 
        auto
        url="https://www.googleapis.com/youtube/v3/search"
        params='{"part":"snippet", "q":"polymer", "key": "AIzaSyAuecFZ9xJXbGDkQYWBmYrtzOGJD-iDIgI", "type": "video"}'
        handle-as="json"
        last-response="{{ajaxResponse}}"></iron-ajax>
```



###Highlighting Key Attributes
These are the basic attributes I need to get an ajax request to succeed or the web page will not validate requests correctly without it.

--------
* url

>String default: ''
The URL target of the request.

>> **auto**
Boolean default: false

>If true, automatically performs an Ajax request when either url or params changes.

>You can trigger a request explicitly by calling generateRequest on the element.

>> **generateRequest()**

>>Performs an AJAX request to the specified URL.



------
* handleAs

>String default: json

>Specifies what data to store in the response property, and to deliver as event.detail.response in response events.

>One of:

>text: uses XHR.responseText.

>xml: uses XHR.responseXML.

>json: uses XHR.responseText parsed as JSON.

>arraybuffer: uses XHR.response.

>blob: uses XHR.response.

>document: uses XHR.response.

------
* Body or Params

>**Body** content to send with the request, typically used with "POST" requests.

>If body is a string it will be sent unmodified.

>**Params** content to send with the request, typically used with "POST" requests.

>An object that contains query parameters to be appended to the specified url when generating a request. If you wish to set the body content when making a POST request, you should use the body property instead.

-------
* method

>The HTTP method to use such as 'GET', 'POST', 'PUT', or 'DELETE'. 

>Default is 'GET'.

----------
* on-response

>iron-ajax will notify return data through *on-response* attribute that is readOnly  

>on-response will be set to the most recent response received by a request that originated from this iron-ajax element. The type of the response is determined by the value of handleAs at the time that the request was generated.

>You can trigger a request explicitly by calling **generateRequest** on the element.

##Overview of CRUD operations
----------
###C*reate*
```
            setajaxCreate: function () {
                var xtransaction = new crudCreate(this.email);
                this.$.ajax.url = "https://api.mongolab.com/api/1/databases/clubajax/collections/crudLab?apiKey=mongolabApiKey";
                with(xtransaction) this.$.ajax.body = {
                    recId: recId,
                    date: date,
                    recIndex: recIndex,
                    email: email,
                    action: action,
                    active: active
                };
                this.$.ajax.generateRequest();
            }

```
----------
###R*ead*
```
         <iron-ajax auto url="https://api.mongolab.com/api/1/databases/clubajax/collections/crudLab?s={'recIndex': -1}&apiKey=mongolabApiKey" handle-as="json" on-response="tasksLoaded"></iron-ajax>
            <template is="dom-repeat" items="{{todos}}">
                <div class="paper-font-body2 paperSweetSpace">
                    <div>
                        Email:: <span>{{item.email}}</span>
                        <br>
                        Action:: <span>{{item.action}}</span>
                        <br>
                        Date:: <span>{{item.date}}</span>
                        <br>
                        Index:: <span>{{item.recIndex}}</span>
                        <br>                    
                        MongoLab Id:: <span>{{item._id.$oid}}</span>
                        <hr>
                    </div>
                </div>
            </template>

```
----------
###U*pdate*
```
            setajaxUpdate: function () {
                var xtransaction = new crudUpdate(this.greeting);                
                this.$.ajax.url = "https://api.mongolab.com/api/1/databases/clubajax/collections/crudLab/"+this.MongoLabId+"?apiKey=mongolabApiKey";
                with(xtransaction) this.$.ajax.body = {
                    "$set": {
                        date: date,
                        recIndex: recIndex,
                        action: action
                    }
                };
                console.log(this.$.ajax.body);
                this.$.ajax.generateRequest();
            }

```
----------
###D*elete*
```
            setajaxDelete: function () {
                this.$.ajax.url = "https://api.mongolab.com/api/1/databases/clubajax/collections/crudLab/"+this.MongoLabId+"?apiKey=mongolabApiKey";
                this.$.ajax.generateRequest();
            }

```

----------
####Links

[Github SiliconHacker Mongodb Polymer Crud](https://github.com/siliconhacker/MongodbPolymerCrud)

[MongoLab](https://mongolab.com/)

[Google Polymer 1.0](https://www.polymer-project.org/1.0/)

[iron-ajax 1.0.4](https://elements.polymer-project.org/elements/iron-ajax)

[iron-ajax… wat?! -- Polycasts #26](https://www.youtube.com/watch?t=3&v=k1eR_3KqJms)


