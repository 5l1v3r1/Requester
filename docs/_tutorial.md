## Getting Started
~~~py
requests.get('https://jsonplaceholder.typicode.com/albums')
requests.post('https://jsonplaceholder.typicode.com/albums')

get('https://jsonplaceholder.typicode.com/posts')
post('https://jsonplaceholder.typicode.com/posts')
~~~

Place your cursor on one of the lines and hit <kbd>ctrl+r</kbd>. Or, look for __Requester: Run Requests__ in the command palette and hit Enter. A response tab will appear, with a name like __GET: /albums__.

Head to the response tab and check out the response. Hit <kbd>ctrl+r</kbd> or <kbd>cmd+r</kbd> to replay the request. You can edit the request, which is at the top of the file, before replaying it.

Now, come back and use [multiple selection](https://www.sublimetext.com/docs/3/multiple_selection_with_the_keyboard.html) to select all 5 lines, and once again hit <kbd>ctrl+r</kbd>.

Tabs will open for all 4 requests (Requester conveniently ignores the blank line). Before checking out these tabs, hit <kbd>ctrl+r</kbd> yet again. Duplicate response tabs will close before reopening, so that you don't have multiple tabs for each request.

Prefixing your requests with __requests.__ is optional. If you want to close all open tabs, look for __Requester: Close All Response Tabs__ in the command palette.


### Environment Variables
In the same directory as this tutorial is a file called `requester_env.py`, which defines a few variables, including one called `base_url`.

~~~py
base_url = 'https://jsonplaceholder.typicode.com'

import requests
jar = requests.cookies.RequestsCookieJar()
jar.set('tasty_cookie', 'yum', domain='httpbin.org', path='/cookies')
~~~

When you run your requests, __Requester__ looks for a requester env file with the name `requester_env.py` in the same directory as the requester file. It includes the variables defined in this file with your requests.

Go ahead and run these requests.

~~~py
env_file = 'requester_env.py'
# env_file = 'relative/path/to/env.py'

requests.get(base_url + '/albums')
requests.post(base_url + '/albums')

get(base_url + '/posts')
post(base_url + '/posts')
~~~

If you wanted to change the name or location of the env file, you could simply define a new `env_file` in your requester file, e.g. by commenting out the top line and uncommenting the one below.

Requester would now look for the env file at `relative/path/to/env.py`, which is relative to the location of the requester file.


### Request Body, Query Params, Custom Headers, Cookies
~~~py
get('http://httpbin.org/headers', headers={'key1': 'value1', 'key2': 'value2'})

get('http://httpbin.org/get', params={'key1': 'value1', 'key2': 'value2'})

get('http://httpbin.org/cookies', cookies={'key1': 'value1', 'key2': 'value2'})
get('http://httpbin.org/cookies', cookies=jar) # `jar` is defined in env vars file

get('http://httpbin.org/redirect-to?url=foo') # response tab shows redirects
~~~

Body, Query Params, and Headers are passed to __requests__ as dictionaries. Cookies can be passed as a dict or an instance of `requests.cookies.RequestsCookieJar`. If you want to pass cookies in this way, they must be instantiated in your env vars file.

If you execute the last request, you'll notice the response tab shows the series of redirects followed by the browser.

If you don't know how to do something, just have a look at the [Requests Quickstart](http://docs.python-requests.org/en/master/user/quickstart/).


## Commands
Commands defined by this package, in case you want to change key bindings.

- __requester__
- __requester_replay_request__
- __requester_close_response_tabs__
- __requester_show_tutorial__


## Settings
- __env_file__: relative path from requester files to env files
  + this can be overridden by defining the `env_file` variable in an individual requester file
- __timeout__: default timeout in seconds for all requests
  + if you want to change this for a single request, __do so directly in the response tab__, not in your requester file


## Gotchas
Requester automatically includes the `timeout` argument in requests executed from your requester file. If you include this arg in your requests, __Requester will raise a SyntaxError__.

That's it.