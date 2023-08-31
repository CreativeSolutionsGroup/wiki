# Cloudflare Worker Documentation

This is probably the simplest part of the entire thing. There is not much to say here.

## Technical

At the most basic level, we receive the data from a client submitting a form. We then transfer the data from this connector to the basecamp endpoints. 

We store the keys for connecting to basecamp in a cloudflare KV store so that we have easy access to all that we need.

Once we have all the information we send it over to the create card/list endpoint. This will return a response with a status code, and if that status code is 201, then we have successfully created our card. 