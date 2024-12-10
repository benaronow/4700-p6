# 4700-p6
1. Approach:
When approaching this project, we mainly followed the steps given in the project description
in order until our `4700dns` file passed all of the tests. In doing so, we first created a
function to respond to a DNS request using the local authoritative zone. We then created a 
function which served as our recursive resolver, and attempted to get a response from an external
DNS server. We then used the concurrent.futures library to run the given receive function
asynchronously, at which point we could pass all tests except for bailiwick checking and caching.
We then created a function for bailiwick checking which cut out certain response records if necessary,
and lastly created functions to add to and look through a cache which is initialized when the server
is created.

2. Challenges:
One challenge we faced was getting the the receive function to run asynchronously. We tried a few
libraries that did not seem to have any affect until settling on concurrent.futures. Additionally,
we spent a lot of time on test 16 as we could not figure out how to implement recursion when it came
to CNAME records. We eventually landed on a correct implementation that recursively called our
external resolver until all of the answers had been added. Finally, we had trouble getting caching
to work, as our initial implementation didn't take into account the IP address of the request, but
once we learned why that was crucial, we were able to get it working.

3. Good features/properties:
We believe that we implemented the simulated DNS server in a relatively performant manner where there
isn't much, if any, unnecessary behavior that would slow it down. The simplicity of our receive function
(try local -> try external -> return NXDomain) is a positive feature and aided in our development of
more complex features like caching. Our "recursive resolver" is also relatively minimalistic, simply
updating the response by making new requests until it is valid, and made the integration of bailiwick
checking and caching into our server very easy.

4. Testing:
We used the `run` executuable with the provided config files to test our code, occasionally adding
temporary print statements for debugging when we were unsure what was wrong.
