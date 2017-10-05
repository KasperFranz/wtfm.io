# Always Be Commenting



> Good code doesn’t need documentation.

What a crock of shit.

The problem with the “good code = documentation” sentiment is that good code is_entirely_subjective, while documentation is not. Developers come in all experience levels, and think in many different ways, which leaves undocumented code completely up to interpretation. Just because the reasons for using that GOTO there are clear to you, does not mean those reasons will be clear to the next person who sees your code.

Now, the best way to document code is entirely up to debate \(a debate nobody will ever win\) but, at a bare minimum, clear comments should be a requirement of any organization. Sure, a beautifully organized wiki would be fantastic, but managing something like a wiki can be detrimental to your productivity \(especially when you’re already neck-deep in code\) so let’s stick with comments for now.

Unfortunately, writing comments is super easy, but writing_quality_comments take a little more time and effort. Exactly what “quality” means in this context is dependent on the organization but, at a high level, comments should explain the “why” and the “how” of the code. A codebase filled with one-liners saying things like “this loop iterates through the data” is far from useful; which is exactly the reason that documentation standards like[PHPDoc](https://www.phpdoc.org/)and[Ruby-Doc](http://ruby-doc.org/)exist. They keep code and documentation together in a commonly accepted standard and encourage more thorough breakdowns of how and why a piece of code works.

I think, as developers, we like to think of code as a recipe. All the steps are written out, so understanding code is as simple as reading the steps, but that’s not the way code works. Programming is an art form, and programmers each have their own unique style and thought process, so it is important to remember that what is clear and intuitive to one may be disorganized and confusing to another.

  
While there are countless tools that add more value to code comments \(these will be addressed in the Tools of the Trade section later\), the main purpose of code comments is to explain _how_ a particular piece of code works, and _why_ it was written that way.

A common mistake many junior developers make is to document what a piece of code does. This, unfortunately, doesn’t add any value because in most cases, what the code is doing is pretty self-evident. On the flip side, just because you can identify what a piece of code is doing, that doesn’t mean how it works or why it was written that way is obvious.

