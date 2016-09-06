# Create DreamFactory services for accessing MapQuest APIs

The purpose of this repo is to help you quickly get up and running using DreamFactory to access MapQuest APIs. This repo contains Swagger 2.0 service definitions for the MapQuest geocoding and search-ahead APIs. Adding these as services to your DreamFactory instance allows you to call and manage MapQuest APIs using DreamFactory’s REST API.  DreamFactory provides user and role management, so you can easily limit which users have access to which services. You can also add pre and post-processing scripts to any endpoint using V8js, Node.js, PHP, or Python. Please visit the [wiki](http://wiki.dreamfactory.com/Main_Page) for answers to common questions such as how to authenticate and make API calls.

To get started, first you need to create a DreamFactory instance.  It can be installed on any machine using the [Bitnami](https://bitnami.com/stack/dreamfactory/installer) installers, or you can create an instance using the hosted [sandbox environment](https://dashboard.vz2.dreamfactory.com) This system runs on the Verizon cloud and is the quickest way to try out DreamFactory. Some server side scripting types are disabled on the sandbox instances, but otherwise they are fully functional instances.

Click the ‘Sign Up’ button and complete the form. Click the ‘Register’ button, and you’ll be taken to the dashboard UI. You are now logged in as a Dashboard user. The Dashboard is your own personal workspace where you can create as many DreamFactory instances as you like.  To create a new instance, enter the desired instance name and click ‘Create Instance’. The instance name you enter will be part of the URL for your instance. For example if the instance name is ‘foo’ the instance URL will be https://foo.vz2.dreamfactory.com.

The new instance will show up in the dashboard UI. Click the ‘Launch’ button to launch the new instance. The first time you launch it there are no users, so you’ll be prompted to create your first admin user.  Admin users have full access to all aspects of the instance, and are not limited by role assignments. Regular users, meaning those who sign up for your app, will have a role assigned that limits what they can do. Complete the admin user form and click the ‘Create’ button. This takes you to the admin console, which is where you manage everything about your DreamFactory instance. If you create another instance, it could have a totally different set of users.  The dashboard user manages all instances, and each instance has its own set of users.

Next you need to create the DreamFactory services for MapQuest. DreamFactory refers to these as ‘Remote HTTP’ services.  Import the package file named mapquest_services.zip from this repo. This will create the services you need to access the MapQuest APIs. You can clone the repo to your local machine, then go to the Packages tab in the admin console. Select ‘Import Package’ then find the file mapquest_services.zip.

Click the ‘Import’ button then go to the Services tab and you should see the two MapQuest services listed.  Go to the ‘API Docs’ to try out the services. You’ll need an API key, which can be obtained [here](https://developer.mapquest.com/plan_purchase/steps/business_edition/business_edition_free/register).

Click the mapquest_geocoding service then click the first GET option to expand. The API key is marked as optional because it can be stored as part of the DreamFactory service by editing the service to define a parameter named ‘key’, with ‘Outbound’ checked.  This tells DreamFactory to add this parameter to every incoming request before calling the MapQuest API. If you don’t want to do that, then just include the key as normal with each client call. Set the location field to whatever you want and click the ‘Try it out!’ button.

It shows the complete cURL request. The DreamFactory API key is a unique identifier for each DreamFactory app. It and the session token are added as headers to each request.

```
curl -X GET --header 'Accept: application/json' --header 'X-DreamFactory-Api-Key: 36fda24fe5588fa4285ac6c6c2fdfbdb6b6bc9834699774c9bf777f706d05a88' --header 'X-DreamFactory-Session-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOjEsInVzZXJfaWQiOjEsImVtYWlsIjoidGVzdGVyQGRyZWFtZmFjdG9yeS5jb20iLCJmb3JldmVyIjpmYWxzZSwiaXNzIjoiaHR0cDpcL1wvdG9kZC52ejIuZHJlYW1mYWN0b3J5LmNvbVwvYXBpXC92Mlwvc3lzdGVtXC9hZG1pblwvc2Vzc2lvbiIsImlhdCI6MTQ3MTk1OTY3NSwiZXhwIjoxNDcxOTYzMjc1LCJuYmYiOjE0NzE5NTk2NzUsImp0aSI6Ijk2YzI4ZjFiYWUzY2M3ZmI2ZTdjMzNjZWY3MGM0ZmVlIn0.T2NJ5b5vlKRMrjaNQPjuGXM50XRqwtwQGGJfJsluEBw' 'http://foo.vz2.dreamfactory.com/api/v2/mapquest_geocoding/address?key=N8CLhlwOrCoZ3A0AqC3zRe56WWj68P9w&location=dallas%2Ctx'
```

It also shows the request URL. This is how your app will call the services. You app would add the DreamFactory API key and session token as headers X-DreamFactory-API-Key and X-DreamFactory-Session-Token.

```
GET http://foo.vz2.dreamfactory.com/api/v2/mapquest_geocoding/address?key=N8CLhlwOrCoZ3A0AqC3zRe56WWj68Pw&location=dallas%2Ctx
```

The other endpoints can be accessed from the API Docs in the same manner. Of course you can also use any HTTP client to make the API calls.
