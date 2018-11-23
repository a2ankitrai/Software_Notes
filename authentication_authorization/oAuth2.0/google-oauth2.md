# Using OAuth 2.0 to Access Google APIs
----

[Link](https://developers.google.com/identity/protocols/OAuth2)



1. Obtain OAuth 2.0 credentials from the Google API Console.

Visit the Google API Console to obtain OAuth 2.0 credentials such as a client ID and client secret that are known to both Google and your application

2. Obtain an access token from the Google Authorization Server.

3. Send the access token to an API.

After an application obtains an access token, it sends the token to a Google API in an HTTP authorization header.

---

# Steps to create a Google app for Oauth2 social login

1. Go to https://console.developers.google.com and create a new application.

2. Go to Credentials section and create an oauth client

for this example:  
  Web Client 1

  client-id: 44684615755-t3v4e43nacg77ac7ctpa5ki9vkrab2b5.apps.googleusercontent.com
  client-secret: OHu9tJ-9XUjl-Gx86We5olRD

  Web Client 2

    clientId: 44684615755-g4kn7rbev3shlbdu2n943i0c1jb4nv4n.apps.googleusercontent.com
    client-secret: 9xaWk1bCbzy_gYVvj-D_y-io
