Activity Dialog
===============

A method for third-party sites to invoke an activity dialog on the users website to allow the user to perform an activity (like, follow, comment, share, etc.) on the third-party owned URI addressable resource.

Third-party sites will allow actions (follow, like, comment, share) on their resources by asking for your converspace URI which in turn will return an ActivityDialogURI (via HTTP header or HTML link tag) that they can popup in a separate window passing in the required parameter (resource, activity, etc.). Since this URI is on the users website, it will authenticate the user and the action therefore will happen on the users site and send an [Activity Pingback](https://github.com/sandeepshetty/converspace/blob/master/ActivityPingback.md) to the thrid-party site about it. This is kinda like a bookmarklet to a URI on your site but invoked by a third-party sites.