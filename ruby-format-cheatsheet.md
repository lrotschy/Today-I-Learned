Kernel#format Cheat Sheet 

For time: 
`sprintf("%02d:%02d", 2, 3)`  # => "02:03"

For decimal places:
  `sprintf("%.3f", 4)` # => "4.000"
  
For leading zeros: 
  `sprintf("%.2d", 1)` # => "01"
  
For string interpolation with a single string: 
 ` "items a = %s" % 'cat'`
      # = >  "items a = cat" 

For string interpolation with an array: 
 ` "items a = %s, b = %s" % ['cat', 'dog']`
      # = >  "items a = cat, b = dog" 

For string interpolation with a hash: 
 ` "items a = %<x>s, b = %<y>s" % {x:'cat', y:'dog'}`
      # = >  "items a = cat, b = dog"
