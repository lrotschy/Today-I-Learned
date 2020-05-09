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
      
      # Ruby `Kernel#format`
[Idiosyncratic Ruby: What the Format?](https://idiosyncratic-ruby.com/49-what-the-format.html)

#### Basics
`sprintf` shortcut = `%`

Use a string template and bind it to data via `%` method:
``` ruby
v = 42
"!!! %s !!!" %v
# => "!!!42!!!"
```

- separates the string's format (template) from data 
- template contains references: `%x` or `%<name>x`


- named format strings take a hash parameter

``` ruby
"items a = %<v>s , item b = %<z>s " % {v:1, z:2}
# => "items a = 1 , item b = 2 " 
```

- unnamed format strings take an array or a single value

``` ruby
"items a = %s , item b = %s" % ['cat', 'dog']
#=> "items a = cat , item b = dog"
```

``` ruby
"The most important factor is %s" %'effort'
#=> "The most important factor is effort"
``` 

#### Other types of formatting
`%<name>AB.CX`
- `%` required 
- `<name>` optional, for named reference 
- `A` flags optional 
 a number not preceded by `.` or `$` is interpreted as padding width, i.e. minimum string length. Empty spaces added at beginning of string.
``` ruby
"%20s" % "la la"
 #=> "               la la"
```
 a minus adds spaces after:
``` ruby
"%-20s" % "la la"
 #=> "la la               " 
```
 `*` is dynamic padding with another arg. 
 
  `0` flag with `i` pads with initial zeros:
  ``` ruby
"%02i" % 1
  #=> "01"
``` 
  will not work for other formats, returns string, will not work with `-` (right pad)
  `+` coerces positive or negative sign for integers
  ` ` leaves empty space to left of integers
- `B` Width optional 
- `.C` Precision optional 
  length limit
- `X` Formatting type required 
- `%s` calls to_s on object, precision gives length limit
``` ruby 
"%4.8s" % 12 # = at least four, not more than 8
#=> "  12"
"%4.8s" % 1223342424634563456
# => "12233424" 
