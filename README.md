## Introduction ##

pycloc is a Python-based OAuth 1.0a client, aimed at being straightforward to use, in the same way as cURL.

### Requirements ###

pycloc requires Python 2.5+ (possibly 2.4, but untested), [python-oauth2](http://github.com/simplegeo/python-oauth2) and [PyYAML](http://pypi.python.org/pypi/PyYAML).

## Twitter Quickstart ##

 1. [Register your application with Twitter](http://dev.twitter.com/apps) to get a consumer key and secret.
 2. Obtain your request token:

        pycloc 'https://api.twitter.com/oauth/request_token&oauth_callback=oob' --request-token -k $CONSUMER_KEY -K $CONSUMER_SECRET

 4. This will then give you a requst token and secret.
 5. Visit `https://api.twitter.com/oauth/authorize?oauth_token=$TOKEN`
    to authorize the application and obtain a verifier PIN.
 6. Obtain your access token:

        pycloc https://api.twitter.com/oauth/access_token --access-token -V $VERIFIER_PIN

 7. Make requests against the API:

        pycloc 'http://api.twitter.com/1/statuses/home_timeline.xml'
        pycloc 'http://api.twitter.com/1/statuses/update.xml' -p -a 'status=Testing pycloc now. Does it work?'


## Basic Walkthrough ##

 1. Register your application and get a consumer key and secret
 2. Do one of the following:
     1. Include `-k $CONSUMER_TOKEN -K $CONSUMER_SECRET` in the first call for a
        host (e.g. the request_token call). pycloc will save them thereafter.

     2. Place them into your `~/.pyclocrc` using the hostname of the target API.

            hosts:
              api.example.com:
                consumer-secret: $MY_CONSUMER_SECRET
                consumer-token: $MY_CONSUMER_TOKEN

 3. Obtain your request token:

        pycloc http://api.example.com/oauth/request_token --request-token

 4. This will then give you a request token and secret, and an authorize URL (based on the request_token URL -- adapt as necessary).
 5. Visit the authorize URL, authorize the application and obtain a verifier.
 6. Obtain your access token:

        pycloc http://api.example.com/oauth/access_token --access-token -V $VERIFIER

 7. Make requests against the API:

        pycloc http://api.example.com/v1/get_data
        pycloc http://api.example.com/v1/post_something -p -a 'foo=bar' -a 'bz=quux'

