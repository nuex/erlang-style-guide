Erlang Coding Style Guide
=========================

## Theory

Easy to maintain code should:

* look like it was written by a single entity
* follow community best-practices and idioms
* lend itself to testing, metrics gathering, and other scrutiny/verification
* make it easy to find code dealing with a particular concern of the system

We write code for other developers, not the interpreter.
We have tools to help us manage and create good code.

## Practice

### See also:

* http://www.erlang.se/doc/programming_rules.shtml
* http://www.erlang.org/doc/apps/edoc/chapter.html

### File Composition

* Use 2 space indent, no tabs.
* Use Unix-style line endings.
* Each file should have a newline as its last character.
* Keep lines fewer than 80 characters, count \n as part of that line.
* Avoid trailing whitespace on lines (.git/hooks/pre-commit can help).

### Functions

* Functions either express a workflow or perform a single task.
* Task-type functions should not call other task-type functions: everything 
terminates at a single, isolated, testable task method.
* Match variables in the head over the body when possible.
* Avoid lists or proplists of optional parameters. For task-type functions 
it probably means the task function is doing too much or branching to call 
other functions.
* Avoid many arguments. For task functions, look at related arguments that 
could be represented as a component module or record and pass that in 
instead.

### General Code Style

* Use single spaces around operators (`+`, `-`, `*`, etc).
* No spaces after `{`, `(`, `[` and before `]`, `)`, `}`.
* No spaces around curly brackets or `=` in record assignments.
* Prefer list comprehensions over `lists:map` or `lists:filter`.

      % Yes
      1 + 1.
      {ok, Database} = database:connect(Hostname, Password). 
      User = #user{firstname=FirstName}.
      Portals = [portal_gun:fire(X, Y, Z) || {X, Y, Z} <- Targets].

      % No
      6+5.
      Chefs = [ "Joe","Gordon","Graham" ],
      Client = #client{ client_id = ClientId }.

* Line up a call with lots of arguments by putting arguments indented to the 
level of the first argument on the top line. Where not possible, indent 4 four 
spaces into the function being called.
* Closing `)`, `}`, and `]` should not be on a line by themselves.

### Naming

* Use names prefixed with `_` for unused variables, for example when you implement a callback to an API that gives you more than you care about.
* Do not pass bare objects (strings, lists, true, false, nil) into functions if their use is not clear. Instead make a variable (called _SkipProcessing=true, for example) and pass the named variable in instead.

### Testing

* Integration tests should not look at the database, they should observe the changes visible from the front-end.

### Optimization

* Do not optimize for performance.
* Do not make use of advanced features of our infrastructure or backend servies.
* When optimization becomes necessary: measure, implement a fix for a single code path, measure in testing, release, measure.

### Misc Engineering

* Avoid needless metaprogramming. Avoid dependencies that encourage it.
* Avoid forking dependencies. Write wrappers for dependencies that don't work as expected. Otherwise avoid the dependency.
* Do not program defensively. See [Erlang Style Guide](http://www.erlang.se/doc/programming_rules.shtml#HDR11).
* Fail fast and loud.

### General

* Keep the code simple.
* Don't overdesign.
* Don't underdesign.
* Avoid bugs.
* Read other style guides and apply the parts that don't dissent with this list. Recommended: PEP-8, PEP-257.
* Be consistent with your team and community idioms.
* Use common sense.
