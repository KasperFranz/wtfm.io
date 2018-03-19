# \# Always Be Commenting

As developers, we like to think of source code as a recipe. All the steps are written out, so understanding code is as simple as reading those steps. But that’s not the way it really works, is it? Programming is an art form, and programmers each have their own unique style and thought process, so it is important to remember that what is clear and intuitive to one may be disorganized and confusing to another.

Rather than treating code like a recipe, we should instead treat it like literature. The code itself is prose, written for the computer to read. While we as developers can speak the language of the computer, we sometimes need a little help understanding it. This is where the gloss—or comments—provide value. Like annotations, the intended purpose of code comments isn't to summarize the code itself, but to provide clarity about the thought process _behind_ the code.

## A Brief History of Code Comments

Believe it or not, code comments used to be handwritten or typed notes that accompanied hard-copy coder sheets and punch cards in early decades of the computing industry. These comment cards—acting exactly as one would expect—were ignored by the compiler, but provided context to the code in the same way comments are used today. While the utility of writing notes within a pile of 500+ hand-punched cards is immediately obvious, the ability to explain how a piece of code works and what it does has carried its way through every major programming language since the 1950s, and is a convention that predates the existence of nearly every modern aspect of computing we take for granted today.

## Commenting Is as Commenting Does

A good rule of thumb for code comments is that they shouldn't be necessary to get a good idea of what a piece of code does. But while code design is important for reducing the onboarding time for developers to a new codebase, they aren't without merit. As we'll see in future chapters, while there are countless tools that extract a significant amount of value from code comments \(see [Part IV: Tools of the Trade](//13-tools-of-the-trade.md)\), the primary purpose of code comments is to explain _how_ a particular piece of code works, _why_ it was written that way, and—in some cases—_what_ it does.

### The How

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

### The Why

Sometimes, as programmers, we have to do things the "hacky" way—also known as the "wrong" way, in some circumstances. But as codebases evolve and projects grow beyond their original scope, writing software becomes a balancing act between building new features and properly deprecating legacy code. Without proper comments, it is nearly impossible to identify the "gotchas" in seemingly inefficient or unintuitive code. To illustrate this, let's look at Ruby on Rails' `ActiveRecord::DefineCallbacks` module:

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

In a perfect world, the above module wouldn't exist, but as the comments explain, it _has_ to for now. Without the clear explanation provided by these comments, this module might be inadvertently removed, which would cause all kinds of havoc for the sake of "clarity." Explaining _why_ a piece of code exists is crucial, especially if the reason isn't immediately obvious. As much as we like to pretend all good software is clear and easy to read, that assertion simply doesn't coincide with the reality of the _business_ of software development. Plans change, goals shift, and good code today couldeasily become legacy code tomorrow.

### The What

Generally speaking, documenting what every line of code does is bad practice. Comments are intended to provide clarity, but when _everything_ needs clarity, _nothing_ is every actually clear. That said, there are some cases where the most efficient or streamlined way to write a piece of code isn't always the most intuitive. This is the perfect use case for _what_ comments. When it comes right down to it, not every method or class can have an intuitive name. Whether the functionality itself is too complex, or there simply isn't a way to come up with a succinct name, it is sometimes necessary to use a simple method name and preface it with a short description of what that method does.

A great example of this can be found in the source code for the Laravel PHP framework. The `after()` method takes a string, and returns everything after a given search value. Unfortunately, because of the highly specific nature of the method itself, a method name like `returnEverythingAfter()` adds unnecessary verbosity to a codebase without exactly providing an immediately clear indication about what the method does.

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

While many developers would encourage simply looking directly at the function code to understand what it does, this isn't always practical. As you can see above, the most efficient code isn't always the most intuitive code. By adding a simple comment before the function declaration, understanding what the method does becomes immediately clear without having to do a line-by-line analysis.

## The Code Comment Controversy

In an industry filled with flame wars like VIM versus Emacs and PHP versus... well... everyone, one of the most surprising hot button issues is whether or not developers should write code comments. To sum it up, the "no comment" camp advocates against writing code comments because they clutter up the code, have a tendency to become outdated, and are redundant—because you can just read the code to find out what it does; to all of which, I say "grow up."

Look... I get it, properly commenting your code isn't always fun, but when it comes down to it those comments aren't for you; they're for the next person—who, let's face it, might actually _be_ you. Despite the cliche of the scruffy, basement-dwelling programmer, software development doesn't happen in a vacuum. It involves a significant amount of collaboration and education to be successful, and even then finding common ground on difficult issues is an exercise in patience, empathy, and compromise.

But I don't expect anyone to take my opinion at face value. While I don't agree with the conclusion the "no comment" camp has come to, I'll be the first to admit that the issues they've highlighted are worth discussing.

### Point 1: Comment Clutter

One person's clutter is another person's clarity. Dismissing the value of comments because they clutter up the code is an entirely subjective—and selfish—assertion that is no different than downplaying the value of graphical user interfaces because you personally prefer to use the command line. While viewing comments as a roadblock towards reading a block of code is understandable, there are countless of plugins for nearly every editor that can be used to fold or hide comments without removing them entirely. This allows you to easily parse code while also leaving information that other developers may find valuable.

### Point 2: Stale Comments

If someone told you that they prefer not to write unit tests because they take effort to keep up to date, how would you respond? Keeping code comments up to date is a responsibility no different than keeping unit tests up to date. Bemoaning the value of comments because they get stale indicates a systemic problem at the organization level, not in the comments themselves. Like any best practice, it requires discipline to extract value out of it, because without discipline all you are doing is adding complexity without order.

### Point 3: Comment Redundancy

Not all code is created equal, because not all developers are created equal. We all have different experiences and habits that guide us to slightly different ways to solve the same problems. This difference in thought processes is the primary benefit of code comments. While it may seem redundant to explain your code when "it's already right there," this information could be incredibly valuable to new developers, or even experienced developers who are unfamiliar with the language or framework you are using.

## Conclusion

## Questions & Exercises



