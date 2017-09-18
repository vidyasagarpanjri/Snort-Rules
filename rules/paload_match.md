
content:
  Content is searched using Boyer-Moore algorithm.
  matching is case sensetive.
  if matiching data is found in the packet payload rule triggers.
  it can serach both binary|00| and text data "text".
  multiple content rules can be used in one rule. they will be "and" i.e all must be ture
  negation can also be used 
  
  format:  
  
  content:"google";content:"|2f|";
  
  modifiers: which will control the behavious of content match.
  
  1. nocase : it will make the match case insensitive.
    content:"href";nocase;content:"co.in";
    here "href" match will be case insensetive i.e it will macth on HREF or href or Href ... but "co.in" is case sensetive i.e it  will fail on "CO.in" 
  
  2. rawbytes : it will match againts the undecoded/ normalised payload. mostly all payload data is decoded by engine but if we have to match on raw content we can use it.
  
  content:"google";rawbytes;)
  3. depth: it will look for the match upto specified number of bytes from starting of payload.
  for eg if curl  www.google.com and 
  check the cache-control header. using   content:"cache";nocase;depth:25;

  4. offset :  it will look for the match after the number of bytes specified in offset in payload
      eg. we want to look only for html code in html response which is after 80 bytes in 
      curl  www.google.com
      content:"html";nocase;offset:80;
  5. distance : it will start searching after the match of previous content ( if present else from starting )   
like if we want to search "href" after html in :  curl  www.google.com 
we use : content:"html";nocase;content:"href";nocase;distance:1;
      
  6. within: it will look for a text , between end byte of last match and the number of bytes specified in rule.
    content:"html";nocase;content:"href";nocase;within:1000;
    it will search for href, between end of html and html+1000 bytes.
  
  7.  http_client_body: we hav eto configure the http_inspect preprocessor for this 
