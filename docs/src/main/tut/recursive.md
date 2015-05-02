Typeclasses may be defined recursively. Here's an example.

```tut
/**
 * A typeclass for nested structures.
 */
trait Nested[M[_], E] {
  def elem: M[Xor[E, M[Nested[M, E]]]]
}
```
This class says that given a one parameter typeclass `M`, we can 
construct a generalization of `M` consisting of a nested `M` structure.

For example, this can be used to implement a nested set structure of 
integers, having instances such as
{1, {2, 3} {{4}, 5, 6}}

In the case that `M` is a monad, `Nested[M[_], E] is also a monad.

```tut
object Nested { implicit def hasMonad[M[_]: Monad, E]: Monad[Nested[M, E]] = ??? }
```
