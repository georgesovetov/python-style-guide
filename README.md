# Python Style Guide (stricter PEP 8 extension)

## About This Document

This style guide is written with respect and appreciation of [PEP 8](https://www.python.org/dev/peps/pep-0008/) and, basically, is its stricter extension.

Code formatted according to PEP 8 recommendations and even someone's good sense is still ugly and unreadable, line-wise diffs might reveal real changes more clearly. This guide is created for those who need more certainty in code style, who frequently ask themselves how to format their code, who strive for perfection in what they produce.

This document contains only difference from PEP 8. Here are only those requirements that are not mentioned there or those that are stricter or more prohibitive.

Key insigts:
- Code is read much more ofter then written. (Cited from PEP 8.)
- Line-wise diffs are always read and should be as clear as possible.
- The less you think how to format the code the more you think about your task.
- Formatting is checked or even performed automatically.
- Interactive debugging is used frequently.
- Immutability is blissful, `None` is malicious.
- Errors must be exposed as early as possible.


## Feedback, Changes and Contibution

This document is subject to revision, refinment and improvements. It will not change dramatically.

Please leave feedback, ask, comment and contribute if you
- think you can make this style guide better,
- have faced some formatting or code style challenge,
- have any good or bad examples of formatting or code style,
- have any other questions or comments.

Leave feedback here under lines of code, create issues and pull requests or contact me directly. You're welcomed.


## Code Formatting


### Multiline Statements

Try to introduce new variables, functions and classes first.

Expression or statement MUST be multilined
 - if it
   - doesn't fit single line or
   - is too complex to comprehend at first sight;
   - ends with part that is multilined (`(...)`, `[...]` or `{...}`);
 - if it is:
   - container variable definition (tuple, dictionary, set, frozenset or similar),
   - function call,
   - function definition,
   - list comprehension,
   - string formatting with `%` operator.

#### Yes: Closing parens without indent — good for diffs
```
xformsdata = {'schema':{
    '@xmlns':'',
    'systemInformation': {
        '@progress': '',
    },
}}
```
#### Yes: Closing parens with indent — good for diffs
```
xformsdata = {'schema':{
    '@xmlns':'',
    'systemInformation': {
        '@progress': '',
        },
    }}
```
#### Yes: Closing parens on same line (Lisp style) — dense
```
xformsdata = {'schema':{
    '@xmlns':'',
    'systemInformation': {
        '@progress': ''}}}
```

#### No: Statement doesn't end with multilined parentheses
```
timeModified = datetime.strptime(
	time.ctime(os.path.getmtime(
		os.path.join(pathTo, 'logs/%s' % fileName)
	)),
	'%a %b %d %H:%M:%S %Y',
).date()  # .date() is hardly noticable: easy to overlook.
```
#### No: Arithmetic expression multilined
```
urlpatters = admin_urlpatterns + patterns(  # 
    '',
    url(r'^robokassa/', include('robokassa.urls', 'robokassa')),
    url(r'^$', IndexView.as_view(), name='index'),
    url(r'^map/', include('map.urls', namespace='map')),
    url(r'^main/', include('main.urls', namespace='main')),
    url(r'^reviews/', include('reviews.urls', namespace='reviews')),
    url(r'^events/', include('events.urls', namespace='events')),
)
```


#### Sequences, Function Arguments and Parameters, Class Parents

- All container elements, parameters, arguments and class parents must be written
   - one per line,
   - followed by comma,
   - indented by 1 level relative to first line of statement.
- First element must be on separate line, next to the first line of statement.
- Do not group several elements on single line.
- Last element must be followed by comma.
- Closing parenthesis, bracket or brace must be
   - on next line to last element
   - with same indent as first line of statement;
   - if needed, it's immediately followed by one or more colon or comma, parenthesis, bracket or brace.

Yes:
```
log_file_path = os.path.join(  # No argument on this line
	base_directory_path,
	'logs',
	today_dir_name,
	log_file_name,  # Trailing comma
)
```
```
downloadLogs(  # No argument on this line
    session,
	PATH_TO_TOMCAT,
	['coreLogs', 'pluginLogs', 'systemLogs'],  # Argument is one-line
	tomcatLoggingInterval,
	'Tomcat',  # Trailing comma
)
```
```
def get_log_file_path(  # No parameter on this line
    base_directory_path,
    today,
    log_file_name,  # Trailing comma
):
    # ...
# Closing parethesis and semicolon are next line:
# parameters and body are visually distinguishable.
```
```
class LoggerDownloader(  # No parent on this line
	Downloader,
    ConnectionMixin,
    LoggingMixin,
    CryptoMixin,  # Trailing comma
):
    pass
```

No:
```
# Aligned with opening delimiter.
os.path.join(base_directory_path, 'logs',
			 today_dir_name, log_file_name)
# Allowed by PEP 8. Disallowed by this guide. Downsides
#  - Need to be reformatted if function is renamed.
#  - May need to be reformatted if first argument is renamed.
#  - Obscure diff in case of any changes.
#  - Hard to reorder arguments.
#  - Indentation is not always divisible by 4:
#    to start new line of arguments
#    several Tabs ans several spaces should be pressed.
```
```
# More indentation included to distinguish this from the rest.
def get_log_file_path(
	    base_directory_path,
	    today,
	    log_file_name):
    # ...
# Allowed by PEP 8. Disallowed by this guide. Downsides:
#  - Hard to reorder parameters.
#  - Obscure diff if new parameter is added on last line.
#  - Closing expression is not on the same level as first line.
```
```
# Hanging indents should add a level.
os.path.join(
	base_directory_path, 'logs',
	today_dir_name, log_file_name)
# Allowed by PEP 8. Disallowed by this guide. Downsides:
#  - Hard to reorder parameters.
#  - Obscure diff if new parameter is added on last line.
#  - Closing expression is not on the same level as first line.
```
```
timeModified = datetime.strptime(time.ctime(os.path.getmtime(
											os.path.join(pathTo,
														 'logs',
														 fileName))), 
                                 '%a %b %d %H:%M:%S %Y').date()
                                
# Allowed by PEP 8. Disallowed by this guide.
# Similar formatting was reviewed above.
# In this case we have piece of expression 
# settled on right side where.
# Level of nesting doesn't correlate with indent.
```
```
# Arguments on first line forbidden when not using vertical alignment.
os.path.join(base_directory_path, 'logs',
	today_dir_name, log_file_name)
# Disallowed by PEP 8. Disallowed by this guide.
```
```
# Further indentation required as indentation is not distinguishable.
def get_log_file_path(
    base_directory_path,
    today,
    log_file_name):
    # ...
# Disallowed by PEP 8. Disallowed by this guide. Downsides:
#  - Closing parethesis and semicolon should be on next line
#    to delimit parameters and function body.
```

#### List Comprehensions

Always consider transforming list comprehension into generator function with `yield`. Avoid appending to list because it violates immutability and, effectively, is not same as list comprehension: it's list, not generator.

- `for` clause is written on separate line.
- If `in` clause is not trivial or there is not enough space on line, it's written on separate line.
- `if` clause, if presented, is written on separate line.

Yes:
```
odd_apples = (
    fruit
    for index, fruit in enumerate(fruits)
    if index % 2 == 1 and fruit.name.startswith('apple')
)
```
```
even_oranges = (
    fruit
    for index, fruit 
    in enumerate(fetch_fruits(  # Non-trivial in clause
        'api.example.com/fruits',
        limit=100,
    ))
    if index % 2 == 0 and fruit.name.startswith('orange')
)
```


#### Lambdas

Lambda body can be easily split into multiple lines if enclosed in parentheses.
 - Opening parenthesis is on first line of `lambda`.
   - It's the last symbol on this line.
 - Closing parenthesis is on separate line with same indent as line with `lambda`.

Yes:
```
uploader_url = url(
    r'^helper/ajax-upload/$',
    AjaxFileUploader(
        update_filename=lambda request, filename: (  # Nothing after paren
            '%s.%s%s' % (
                os.path.splitext(os.path.basename(filename))[0],
                get_random_string(
                	length=32,
                	allowed_chars=string.ascii_uppercase,
                ),
                os.path.splitext(filename)[1],
            )
        ),
    ),
    name="ajax_uploader"
)
```


#### Nesting

- If statement is multiline and it's not last element of its parent, parent must also be multiline according to rules above.  
- If statement is multiline and it is last element of its parent, statement may start on same line as parent and immediately followed without line break by parents closing parenthesis, bracket or brace.

Yes:

```
foo(
    ['a', 'b'],
    (
        'a',
        'b',
        'c',
    ),
    (
        'd',
        'e',
    ),
)
```
```
bar(
    map(int, (
        '1',
        '2',
        '3',
    )),  # Extra Parethesis because map here is not multiine
    4,
    5,
)
```
```
make_picture(
    map(dress, (
        (a, b),
        for a, b, c 
        in fetch_threesomes(
            url='example.com/api/threesomes',
            limit=100,
            order='avg_age',
            timeout=100,
        )
        if all((
            any(x.sex == 'female' for x in (a, b, c))),
            any(x.sex == 'male' for x in (a, b, c))),
        ))
    )),  # Extra Parethesis because map here is not multiine
    4,
    5,
)
```
```
uploader_url = url(
    r'^helper/ajax-upload/$',
    AjaxFileUploader(
    	# In this case, lambda is not multilined
    	# but expression returned from lamdba is multilined.
        update_filename=lambda request, filename: '%s.%s%s' % (
            os.path.splitext(os.path.basename(filename))[0],
            get_random_string(
            	length=32,
            	allowed_chars=string.ascii_uppercase,
            ),
            os.path.splitext(filename)[1],
        ),
    ),
    name="ajax_uploader"
)
```

It's easy for eye to find element looking from top to bottom. Number of elements is simply number of rows.

Think of diffs. With this style, diffs are as clear as possible. Otherwise, how would line-wise diff look like if:
- function name were changed,
- new element were added:
   - before first element,
   - after last element,
- there were removed:
   - first element,
   - last element,
- order of elements were changed, including:
   - first element,
   - last element?


### Single and Double Quotes

- Use single quotes if string is meant to be read by machine.
- Use double quotes if string is meant to be read by human.

Yes:
```
some_fruit = {
    'type': 'apple',
    'name': "New Apple 2016",
}
```


### Names

- Abbreviations are discouraged. Use them sparingly.
  - If code readability could benefit from using particular abbreviations,
    - document them well,
    - limit their scope,
    - maintain consistency.
- If specific names are used in document, book, convention, use them.
  - For scientific formulas, it's acceptable to use one-letter names (`P` or `phi`) if they are common.
- Avoid underscore suffix to resolve clashed with built-in names. Use more specific names and synonyms.
- Avoid methods starting methods with `get_` and `set_`. 
  - Use properties or, in case of heavy computation, make name reflect it, e.g. `calculate_`.
- Use consitent prefix for named initializers, e.g. `from_` or `make_`.


### Comments and Docstrings

- Include links to documentation, scientific articles, places that code is taken from.
- Ask yourself if better name can replace comment. If so, rename amd remove comment.


### Resources (`with` and `try ... finally` Clauses)

Here the word *resource* has a very wide meaning. Everything that must be closed, released or finalized is *resource*. Examples: files, sockets, mutexes, threads, any devices.

- Enforce resource releasing.
- Use
  - `with` with context manager:
    - if resource is acquired and released more than once or
    - if resource acquisition and releasing aren't logially coupled with code where resource is used.
  - `try ... finally`
    - if acquisition and releasing are essentially part of surrounding code where resource is used.
- If 3rd party code doesn't offer context manager but acquisition and releasing method instead, create context manager wrapper.
- Prefer `contextmanager` decorator over context manager classes with `__enter__` and `__exit__`.
- When writing classes with `__enter__` and `__exit__`, keep in mind:
  - `__init__` must be light-weight initializer, there must be no resourse initialization in it;
  - `__enter__` is solely resource acquisition;
  - `__exit__` is solely resource releasing;
  - context manager object can be reused.

`with` is preferred because it doesn't leave possibility to forget to release resource. `finally` clause can be forgotten. Context manager can be tested separately.


### Exceptions (`raise` Clause) and Exception Handling (`try ... except ... else` Clause)

- Use `raise ... from` in Python 3.
- If some data is acquired in `try` clause, it must be either
  - returned immediately from `try` clause or
  - passed as argument of exception raised from `try` clause or
  - used in `else` clause.
- Use `else` clause.
- Reraise expected exceptions as special classes with descriptive messages.

Variables defined in `try` clause, are not guaranteed to be defined in after `try ... except ... else` clause. Even if `except` catches exceptions raised when before variables are defined, it creates very unobvious coupling between possible exceptions and variable definition. Please, follow advice given above.

Yes:
```
def retrieve_cats():
    url = 'example.com/api/cats'
    try:
        return fetch_data(url, limit=100, order='name asc')
    except TimeoutError as e:
        message = "Network problem, check connection to %s" % url
        raise CatsRetrievalError(message) from e
    # Not required,
    # to show explicitly that control flow cannot reach here
    assert False
```
```
def print_cats():
    url = 'example.com/api/cats'
    try:
        cats = fetch_data(url, limit=100, order='name asc')
    except TimeoutError as e:
        print("Network problem, check connection to %s" % url)
    else:
        print(cats)
```
No:
```
def print_cats():
    try:
        url = 'example.com/api/cats'  # No need to place here
        cats = fetch_data(url, limit=100, order='name asc')
    except TimeoutError as e:
        print("Network problem, check connection to %s" % url)
    print(cats)  # May be undefined
```
```
def retieve_cats():
    cats = None
    url = 'example.com/api/cats'
    try:
        cats = fetch_data(url, limit=100, order='name asc')
    except TimeoutError as e:
        raise CatsRetrievalError(message) from e
    return cats
```

### Sequences

- Use list unpacking instead of zero element.

Yes:
```
single_result, = results
print(single_result)
```
```
first_result, *other_results = results  # Python 3 only
```
No:
```
print(results[0])
```

List unpacking can serve as extra assertion that exactly one result is acquired. As any other assertion, it reveals errors earlier.


## Recipes


### Arithmetic expressions

Never split arithmetic into multiple lines.

 - Use `sum(...)` if you want to add or subtract values.
 - Use `reduce(operator.mul, ...)` for product. (Rarely needed.)
 - Introduce more variables and functions, which help:
   - to understand formula having parts of it explicitly named,
   - to debug formuals.


### Logical expressions

Never split logic into multiple lines. Multiline `if` or `while` condition is very ulgy and its first (or last, depending on formatting) member always differ from others.

 - Use `all(...)` or `any(...)`.
 - Introduce more variables and functions, which help:
   - to understand formula having parts of it explicitly named,
   - to debug formuals.
