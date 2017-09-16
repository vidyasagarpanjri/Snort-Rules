
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
3.   depth: it will look for the match upto specified number of bytes from starting of payload.
  for eg if curl  www.google.com and 
  check the cache-control header. using   content:"href";nocase;depth:25;
