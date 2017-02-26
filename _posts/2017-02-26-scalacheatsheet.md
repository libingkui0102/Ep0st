---
layout: post
title: "scala cheat sheet"
date: 2017-02-26 22:29:00
comments:

---

####scala cheat sheet
来源于网上教程[http://brenocon.com/scalacheat/](http://brenocon.com/scalacheat/)

var x = 5   variable
val x = 5 
[bad!] x = 6    constant
var x: Double = 5   explicit type
functions
[good] def f(x: Int) = { x*x }
[bad!] def f(x: Int)   { x*x }  define function 
hidden error: without = it's a Unit-returning procedure; causes havoc
[good] def f(x: Any) = println(x)
[bad!] def f(x) = println(x)    define function 
syntax error: need types for every arg.
type R = Double type alias
def f(x: R)   vs
def f(x: => R)  call-by-value   vs
call-by-name (lazy parameters)
(x:R) => x*x    anonymous function
(1 to 5).map( _*2 )
(1 to 5).reduceLeft( _+_ )  anonymous function: underscore is positionally matched arg.
(1 to 5).map( x => x*x )    anonymous function: to use an arg twice, have to name it.
[good] (1 to 5).map(2*)
[bad!] (1 to 5).map(*2) anonymous function: bound infix method. Use 2*_ for sanity's sake instead.
(1 to 5).map { val x=_*2; println(x); x }   anonymous function: block style returns last expression
(1 to 5) filter {_%2 == 0} map {_*2}    anonymous functions: pipeline style. (or parens too)
def compose(g:R=>R, h:R=>R) = (x:R) => g(h(x))
val f = compose({_*2}, {_-1})   anonymous functions: to pass in multiple blocks, need outer parens
val zscore = (mean:R, sd:R) => (x:R) => (x-mean)/sd currying, obvious syntax
def zscore(mean:R, sd:R) = (x:R) => (x-mean)/sd currying, obvious syntax
def zscore(mean:R, sd:R)(x:R) = (x-mean)/sd currying, sugar syntax. but then:
val normer = zscore(7, 0.4)_    need trailing underscore to get the partial, only for the sugar version.
def mapmake[T](g:T=>T)(seq: List[T]) = seq.map(g)   generic type
5.+(3); 5 + 3
(1 to 5) map (_*2)  infix sugar
def sum(args: Int*) = args.reduceLeft(_+_)  varargs
TODO    default args
TODO    named args
packages
import scala.collection._   wildcard import
import scala.collection.Vector
import scala.collection.{Vector, Sequence}  selective import
import scala.collection.{Vector => Vec28}   renaming import
package pkg at start of file
package pkg { ... } declare a package
data structures
(1,2,3) tuple literal (Tuple3)
var (x,y,z) = (1,2,3)   destructuring bind: tuple unpacking via pattern matching
[bad!] var x,y,z = (1,2,3)  hidden error: each assigned to the entire tuple
var xs = List(1,2,3)
list (immutable)
xs(2)   paren indexing (slides)
1 :: List(2,3)  cons
1 to 5   same as   1 until 6
1 to 10 by 2    range sugar
()   (empty parens) sole member of the Unit type (like C/Java void)
control constructs
if (check) happy else sad   conditional
if (check) happy   same as
if (check) happy else ()    conditional sugar
var x = 0
while (x < 5) { println(x); x += 1} while loop
do { println(x); x += 1} while (x < 5)  do while loop
import scala.util.control.Breaks._
breakable { 
    for (x <- xs) {
        if (Math.random < 0.1) break
    } 
}   break (slides)
val xs = List.range(1,11)
val ys = List.range(1,11)
for (x <- xs if x%2 == 0) yield x*10   same as
xs.filter(_%2 == 0).map(_*10)   for comprehension: filter/map
for ((x,y) <- xs zip ys) yield x*y   same as
(xs zip ys) map { case (x,y) => x*y }   for comprehension: destructuring bind
for (x <- xs; y <- ys) yield x*y   same as
xs flatMap {x => ys map {y => x*y}} for comprehension: cross product
for (x <- xs; y <- ys) {
    println("%d/%d = %.1f".format(x,y, x*y))    
}   for comprehension: imperative-ish
sprintf-style
pattern matching
[good] (xs zip ys) map { case (x,y) => x*y }
[bad!] (xs zip ys) map( (x,y) => x*y )  use case in function args for pattern matching
TODO case classes, match...
object orientation
class C(x: R)   same as
class C(private val x: R)
var c = new C(4)    constructor params - private
class C(val x: R)
var c = new C(4)
c.x
constructor params - public
class C(var x: R) {
  assert(x > 0, "positive please")
  var y = x
  val readonly = 5
  private var secret = 1
  def this = this(42)
}   
constructor is class body
declare a public member
declare a gettable but not settable member
declare a private member 
alternative constructor
new { ... } anonymous class (TODO extension syntax)
abstract class D { ... }    define an abstract class. (non-createable)
class C extends D { ... }   define an inherited class.
class D(var x: R)
class C(x: R) extends D(x)  inheritance and constructor params. (wishlist: automatically pass-up params by default)
object O extends D { ... }  define a singleton. (module-like)
trait T { ... }
class C extends T { ... }
class C extends D with T { ... }    traits.
interfaces-with-implementation. no constructor params. mixin-able.
trait T1; trait T2
class C extends T1 with T2
class C extends D with T1 with T2   multiple traits
class C extends D { override def f = ...}   must declare method overrides
new java.io.File("f")   create object
[bad!] new List[Int]
[good] List(1,2,3)  type error: abstract type
instead, convention: callable factory shadowing the type
TODO    self types
classOf[String] class literal
x.isInstanceOf[String]  type check (runtime)
x.asInstanceOf[String]  type cast (runtime)
more
implicit    TODO conversions
TODO    try/catch
<s>hi {name}</s>    xml literal with expression interpolation
TODO Option guarded type-safe nulls (like Maybe or andand)
TODO    unapply
advanced generics
TODO tricky esoteric stuff