---
layout: post
title: "scala cheat sheet"
date: 2017-02-26 22:29:00
comments:

---

#### scala cheat sheet
来源于网上教程[http://brenocon.com/scalacheat/](http://brenocon.com/scalacheat/)

|variables| |
|---|---|
|var x = 5| variable|
|val x = 5 <br/> [bad!] x = 6|constant|
|var x: Double = 5|explicit type|

|functionos| |
|---|---|
|[good] def f(x: Int) = { x*x } <br/> [bad!] def f(x: Int)   { x*x }|define function <br> hidden error: without = it's a Unit-returning procedure; causes havoc|
|[good] def f(x: Any) = println(x) <br/> [bad!] def f(x) = println(x)|  define function <br/> syntax error: need types for every arg.|
|type R = Double|type alias|
|def f(x: R)   vs <br/> def f(x: => R)|call-by-value   vs <br/> call-by-name (lazy parameters)|
|(x:R) => x*x   |anonymous function|
|(1 to 5).map( _*2 ) <br/> (1 to 5).reduceLeft( _+_ )|anonymous function: underscore is positionally matched arg. |
|(1 to 5).map( x => x*x )   |anonymous function: to use an arg twice, have to name it.|
|[good] (1 to 5).map(2*)<br/> [bad!] (1 to 5).map(*2)|anonymous function: bound infix method. Use 2*_ for sanity's sake instead. |
|(1 to 5).map { val x=_*2; println(x); x }  |anonymous function: block style returns last expression|
|(1 to 5) filter {_%2 == 0} map {_*2}   |anonymous functions: pipeline style. (or parens too)|
|def compose(g:R=>R, h:R=>R) = (x:R) => g(h(x))<br/> val f = compose({_*2}, {_-1})|anonymous functions: to pass in multiple blocks, need outer parens|
|val zscore = (mean:R, sd:R) => (x:R) => (x-mean)/sd    |currying, obvious syntax|
