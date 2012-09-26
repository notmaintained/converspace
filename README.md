Converspace
===========

A personal publishing and distributed conversation/activity platform where you own all your data and all activity on it. Kinda like what blogs should have evolved into.


What Twitter got right that blogs are missing:
----------------------------------------------
* The no-admin, simplicity and immediacy of the textarea publishing.
  * Even meta data like tags, mentions and replies required no special interface, just syntax.
* The activity stream


What blogs got wrong:
---------------------
* All content was temporal, which makes editing feel dirty and elevates the value of new content over editing existing content.
  * Addind a stream to the personal publishing platform allows for content to be treated as being non-temporal (URIs do not have a time component) and actions on them as the temporal items (addressable via a URI that has a time component) that populate the stream. Kinda like a wiki.
* Missing real-time publishing
  * Pubsubhubbub to the resque.


Converspace is:
---------------
* Like a blog that allows publishing of content of any size or type (long-form, mirco-updates, videos & photos using oembed, links, quotes) via a single textarea.
  * Titles are optional and are part of the syntax (markdown?)
  * #tags are part of the syntax and can be present anywhere in the content (like twitter)
  * Any URI mentioned in the content will be sent a notification (see below). Is agnostic to the types of things being mentioned. Which means even other users are mentioned via URIs (kinda like linking to the other users blog when you wrote about them, in the good old days of blogging).
* Like twitter/facebook in that it will show an ActivityStream.
* Centered around resources (addressable using a URI), not users and/or content. 
  * You can follow any resource for updates. Resource could be hierarchical. e.g. subscribing to a category will send updates to any posts in it, subscribing to the whole site will send updates to any post on it. 
  * Creation of or updates to a resource sends out Pubsubhubbub notifications to anyone that is subscribed (following).
  * Followers will see a stream of all updates to resource they are following.
    * So a user has 3 views
      * All their content (flat list with a search filter)
      * Thier own activity stream.
        * Third-party sites will allow actions (like liking, commenting, sharing) on their resources by asking for your converspace URI which in turn will return an ActivityDialogURI (via HTTP header or HTML link tag) that they can popup in a separate window passing in the required parameter (resource, activity, etc.). Since this URI is on your website, it will authenticate you and the action therefore will happen on your site and sned a notification to the thrid-party site about it (see below). This is kinda like a bookmarklet to a URI on your site but invoked by a third-party sites.
      * Activity stream of resources they are following.
  * Followers can comment on or mention resources in their content or like/share resources in their following activity stream.
    * This will send out a notification to each of the resources in the content with an ActivityStream payload describing the activity (comment, mention, like, share, etc.)
      * This notification will be kinda like a Pingback post request to the resources ActivityURI (specified via a HTTP header or HTML Link element) with an ActivityStream Payload and an auth token + TokenVerifcationURI in the header.
        * The Pingback receiver (ActivityURI) will make a POST request to the TokenVerifcationURI along with the token to confirm that the pingback originated from the said TokenVerifcationURI.
        * This Pingback like notification system could also be used for private/group messaging in the future. 


TODO
----
* Apps. Haven't thought about this yet but might need oAuth to support this.
