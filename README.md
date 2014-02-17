# Hydra Javascript Client 

Hydra client is a js file that should be included in a client project. 

In a website: 
```
 <script type="text/javascript" src="http://innotech.github.io/hydra/client/hydra.js"></script>
```

It provides two functions:

## hydra.config([<server list>], options)
* [<server list>] - the initial server urls we want to use to access Hydra.
* options - (optional) object containing the following fields:
	* hydraTimeOut - timeout for updating Hydra Servers. Minimum of 60 seconds
	* appTimeOut - timeout for updating an app server in the internal cache. Minimum 20 seconds
	* retryOnFail - retry timeout in case the hydra we are requesting an app or new Hydra servers fail to answer. Minimum 500ms

By default on the browser, the initial Hydra server will be the host serving the hydra.js client file, making this function call optional, although it’s recommended to set up the servers.
The node client have no initial servers, throwing an exception if <code>hydra.config</code> is not call prior to <code>hydra.get</code> 
Calling <code>hydra.config</code> without parameters will return the current hydra servers list.

## hydra.get(appID, [nocache], callback)
This function will call to callback(error, [servers]) function with the url of the server that provides the given appID.
* appID - id of the application requested
* nocache - boolean, optional, if set to true will ask the hydra server for the application servers ignoring the internal cache, defaults to false.
* callback(error, [servers]) - function callback that will receive the app server or an error in case the app does not exist

Internally, it will ask to the first Hydra server or use the internal cache in order to get the corresponding server url for the app and then it will call to callback function. If the application exist, the servers are sent back and served through the callback function (if the application exist, but there are no servers available, it will return an empty array). If the application does not exist, the callback will receive an error and the list will be set to null.

In case an Hydra server fails to answer (when requesting an app or new Hydra servers), the client will try again (based on the retryOnFail timeout) using the next server and moving the one that failed to the end of the list until one of the Hydra servers replies.

# License

(The MIT License)

Authors:  
Germán Ramos &lt;german.ramos@gmail.com&gt;  
Pascual de Juan &lt;pascual.dejuan@gmail.com&gt;  
Jonas da Cruz &lt;unlogic@gmail.com&gt;  
Luis Mesas &lt;luismesas@gmail.com&gt;  
Alejandro Penedo &lt;icedfiend@gmail.com&gt;  
Jose María San José &lt;josem.sanjose@gmail.com&gt;

Contributors:  
Gonzalo Ruiz de Villa &lt;gonzaloruizdevilla@gmail.com&gt;
Alberto Tena &lt;alberto.tena@adesis.com&gt;

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
