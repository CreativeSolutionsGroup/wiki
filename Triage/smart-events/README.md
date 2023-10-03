# Smart Events Triage

## Problem: `admin.cusmartevents.com` redirects to `/register`.

This is likely an issue to do with Lightsail's certificate renewal. These expire every year and you have to redo them. To renew the Lightsail certificate for Smart Events API, go to the `container` > `smart-events-api` > `Custom domains`. 
1. Detach the old cert
2. Create a new cert with `kiosk-backend.cusmartevents.com`
3. It will fail auto verification. Add the CNAME record to `Route 53` with the proper value.
4. Once this is created, it will take a minute. Refresh until it appears under "Attach Certificate (1 available)". Do this.

Once this is done you've verified the cert and it's ready to use again!