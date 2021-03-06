Network
=======

Various functions to do network communication

- `Mail`_
- `HTTP`_

Mail
----

Allows sending mails

API
^^^

.. c:function:: userdata pilight.network.mail()

   Creates a new mail object

.. c:function:: userdata getUserdata()

   Returns a persistent userdata table for the lifetime of the mail object.

.. c:function:: string getFrom()

   Returns the sender.

.. c:function:: string getHost()

   Returns the mail server host.

.. c:function:: string getMessage()

   Returns the mail message.

.. c:function:: string getPassword()

   Returns the mail server password.

.. c:function:: number getPort()

   Returns the mail server port.

.. c:function:: number getSSL()

   Returns the mail server ssl.

.. c:function:: boolean getStatus()

   After the mail was sent this function can be used in the callback to check if the mail was sent successfully to the server.

.. c:function:: string getTo()

   Returns the recipient.

.. c:function:: string getUser()

   Returns the mail server user.

.. c:function:: boolean setCallback(string callback)

   The name of the callback being triggered by the mail library. The mail object will be passed as the only parameter of this callback function.

.. c:function:: boolean setUserdata(userdata table)

   Set a new persistent userdata table for the lifetime of the mail object. The userdata table cannot be of another type as returned from the getData functions.

.. c:function:: boolean setFrom()

   Sets the sender.

.. c:function:: boolean setHost()

   Sets the mail server host.

.. c:function:: boolean setMessage()

   Sets the mail message.

.. c:function:: boolean setPassword()

   Sets the mail server password.

.. c:function:: boolean setPort()

   Sets the mail server port.

.. c:function:: boolean setSSL()

   Sets the mail server ssl.

.. c:function:: boolean setTo()

   Sets the recipient.

.. c:function:: boolean setUser()

   Sets the mail server user.

.. c:function:: boolean send()

   Send the mail

Example
^^^^^^^

.. code-block:: lua

   local M = {}

   function M.callback(mail)
     print(mail.getStatus());
   end

   function M.run()
     local mailobj = pilight.network.mail();

     mailobj.setSubject("foo");
     mailobj.setFrom("order@pilight.org");
     mailobj.setTo("info@pilight.nl");
     mailobj.setMessage("bar");
     mailobj.setHost("127.0.0.1");
     mailobj.setPort(25);
     mailobj.setUser("pilight");
     mailobj.setPassword("test");
     mailobj.setSSL(0);
     mailobj.setCallback("callback");
     mailobj.send();

     return 1;
   end

   return M;

HTTP
----

Do HTTP GET or POST requests

API
^^^

.. c:function:: userdata pilight.network.http()

   Creates a new http object

.. c:function:: userdata getUserdata()

   Returns a persistent userdata table for the lifetime of the mail object.

.. c:function:: string getMimetype()

   Returns the mimetype of the received data. This means it does not returns the mimetype set by the setMimetype() function.

.. c:function:: string getData()

   Returns the data received from the url. This means it does not returns the data set by the setData() function.

.. c:function:: string getUrl()

   Returns the url.

.. c:function:: number getCode()

   After the HTTP request was sent this function can be used in the callback to check if the return HTTP code.

.. c:function:: number getSize()

   After the HTTP request was sent this function can be used in the callback to get the size of the received content.

.. c:function:: boolean setCallback(string callback)

   The name of the callback being triggered by the http library. The http object will be passed as the only parameter of this callback function.

.. c:function:: boolean setUserdata(userdata table)

   Set a new persistent userdata table for the lifetime of the http object. The userdata table cannot be of another type as returned from the getUserdata functions.

.. c:function:: boolean setUrl(string url)

   Sets the request URL. Examples:

     | http://127.0.0.1/
     | https://127.0.0.1/
     | http://127.0.0.1:8080/
     | http://127.0.0.1/index.php?page=foo
     | https://username:password@www.pilight.org:8080/index.php

.. c:function:: boolean setMimetype(string mimetype)

   Sets the mimetype of the data being posted.

.. c:function:: boolean setData(string data)

   Sets the data to be posted.

.. c:function:: boolean get()

   Send a GET request to the URL.

.. c:function:: boolean post()

   Send a POST request to the URL with the data set.

Example
^^^^^^^

.. code-block:: lua

   local M = {}

   function M.callback(http)
     print(http.getCode());
     print(http.getMimetype());
     print(http.getSize());
     print(http.getData());
   end

   function M.run()
     local httpobj = pilight.network.http();

     httpobj.setUrl("http://127.0.0.1:10080/")
     httpobj.setCallback("callback");
     httpobj.get();

     return 1;
   end

   return M;