# Always Be Commenting

> While there are countless tools that add more value to code comments \(these will be addressed in the Tools of the Trade section later\), the main purpose of code comments is to explain _how_ a particular piece of code works, and _why_ it was written that way.
>
> A common mistake many junior developers make is to document what a piece of code does. This, unfortunately, doesn’t add any value because in most cases, what the code is doing is pretty self-evident. On the flip side, just because you can identify what a piece of code is doing, that doesn’t mean how it works or why it was written that way is obvious.

In an industry filled with flame wars like VIM versus Emacs and PHP versus... well... everyone, one of the most surprising hot button issues that won't die is whether or not developers should write code comments. To sum it up, the "no comment" camp advocates against writing code comments because they clutter up the code, have a tendency to become outdated, and are redundant – because you can just read the code to find out what it does; to all of which, I say "grow up."

Look, I get it, properly commenting your code isn't always fun, but when it comes down to it, those comments aren't for you; they're for the next person. Despite the cliche of the scruffy, basement-dwelling programmer, software development doesn't happen in a vacuum. It involves a significant amount of collaboration and education to be successful, and even then finding common ground on difficult issues is an exercise in patience, empathy, and compromise.

But, don't take what I'm writing at face value. While I don't agree with the conclusion the "no comment" camp has come to, I'll be the first one to admit that the issues they've highlighted have some merit.

```php
/**
 * Return the remainder of a string after a given value.
 *
 * @param  string  $subject
 * @param  string  $search
 * @return string
 */
public static function after($subject, $search)
{
    return $search === '' ? $subject : array_reverse(explode($search, $subject, 2))[0];
}
```



