# Always Be Commenting

As developers, we like to think of source code as a recipe. All the steps are written out, so understanding code is as simple as reading those steps. But that’s not the way it really works, is it? Programming is an art form, and programmers each have their own unique style and thought process, so it is important to remember that what is clear and intuitive to one may be disorganized and confusing to another.

While there are countless tools that extract a significant amount of value from code comments \(see [Part IV: Tools of the Trade](//13-tools-of-the-trade.md)\), the primary purpose of code comments is to explain _how_ a particular piece of code works, _why_ it was written that way, and – in some cases – _what_ it does.

## The How

When it comes to commenting code, there's a common misconception that explaining _how_ a piece of code works is the same as explaining _what_ it does. While they are similar in nature, the _how_ is a much more nuanced method of documentation. While the _what_ focuses only on the intended function of a method, the _how_ details its side-effects, caveats, and gotchas. This helps prevent information that can be lost through software design patterns that obfuscate functionality.

Take, for example, the following method found within the source code of the Go programming language:

```go
// Buffered returns a reader of the data remaining in the Decoder's
// buffer. The reader is valid until the next call to Decode.
func (dec *Decoder) Buffered() io.Reader {
    return bytes.NewReader(dec.buf[dec.scanp:])
}
```

_Source: Go \(_[_https://github.com/golang/go_](https://github.com/golang/go)_\)_

While the _what_ of this method is simply `Buffered returns a reader of the data remaining in the Decoder's buffer,`  the _how_ is established in the next part by detailing how long the buffered reader is valid: `The reader is valid until the next call to Decode.`

## The Why

```ruby
module ActiveRecord
  # This module exists because ActiveRecord::AttributeMethods::Dirty needs to
  # define callbacks, but continue to have its version of +save+ be the super
  # method of ActiveRecord::Callbacks. This will be removed when the removal
  # of deprecated code removes this need.
  module DefineCallbacks
    extend ActiveSupport::Concern

    module ClassMethods # :nodoc:
      include ActiveModel::Callbacks
    end

    included do
      include ActiveModel::Validations::Callbacks

      define_model_callbacks :initialize, :find, :touch, only: :after
      define_model_callbacks :save, :create, :update, :destroy
    end
  end
end
```

_Source: Ruby on Rails \(_[_https://github.com/rails/rails_](https://github.com/rails/rails)_\)_

## The What

Generally speaking, documenting what every line of code does is bad practice, but there are some cases when the most efficient or streamlined way to write a piece of code isn't always the most intuitive. This is the perfect use case for _what_ comments. Not every method or class can have an intuitive name. Whether the functionality itself is too complex, or there simply isn't a way to come up with a succinct name, it is sometimes necessary to use a simple method name and preface it with a short description of what that method does.

A great example of this can be found in the source code for the Laravel PHP framework. The `after()` method take a string, and returns everything after a given search value. Unfortunately, because of the highly specific nature of the method itself, a method name like `returnEverythingAfter()` adds unnecessary verbosity to a codebase without exactly providing a more clear indication about what the method does.

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

_Example: Laravel \(_[_https://github.com/laravel/framework_](https://github.com/laravel/framework)_\)_

While many developers would encourage simply looking directly at the function code to understand what it does, as you can see above it isn't the most intuitive line of code in the world. By adding a simple comment before the function declaration, identifying what the method does becomes immediately clear without having to walk through the code.

## The Code Comment Controversy

In an industry filled with flame wars like VIM versus Emacs and PHP versus... well... everyone, one of the most surprising hot button issues is whether or not developers should write code comments. To sum it up, the "no comment" camp advocates against writing code comments because they clutter up the code, have a tendency to become outdated, and are redundant – because you can just read the code to find out what it does; to all of which, I say "grow up."

Look, I get it, properly commenting your code isn't always fun, but when it comes down to it those comments aren't for you; they're for the next person – which, let's face it, might actually _be_ you. Despite the cliche of the scruffy, basement-dwelling programmer, software development doesn't happen in a vacuum. It involves a significant amount of collaboration and education to be successful, and even then finding common ground on difficult issues is an exercise in patience, empathy, and compromise.

But I don't expect anyone to take my opinion at face value. While I don't agree with the conclusion the "no comment" camp has come to, I'll be the first to admit that the issues they've highlighted are worth discussing.

### Point 1: Comment Clutter

One person's clutter is another person's clarity. Dismissing the value of comments because they clutter up the code is an entirely subjective –and selfish –assertion that is no different than downplaying the value of graphical user interfaces because you personally prefer to use the command line. While viewing comments as a roadblock towards reading a block of code is understandable, there are countless of plugins for nearly every editor that can be used to fold or hide comments without removing them entirely. This allows you to easily parse code while also leaving information that other developers may find valuable.

### Point 2: Stale Comments

If someone told you that they prefer not to write unit tests because they take effort to keep up to date, how would you respond? Keeping code comments up to date is a responsibility no different than keeping unit tests up to date. Bemoaning the value of comments because they get stale indicates a systemic problem at the organization level, not in the comments themselves. Like any best practice, it requires discipline to extract value out of it, because without discipline all you are doing is adding complexity without order.

### Point 3: Comment Redundancy

Not all code is created equal, because not all developers are created equal. We all have different experiences and habits that guide us to slightly different ways to solve the same problems. This difference in thought processes is the primary benefit of code comments. While it may seem redundant to explain your code when "it's already right there," this information could be incredibly valuable to new developers or even experienced developers who are unfamiliar with the language or framework you are using.

## Conclusion

## Questions & Exercises



