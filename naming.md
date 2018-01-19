# Naming

## Functions: verbs in imperative form, lowercased, underscores
Even if function is passed as variable.

## Classes: nous, camel case
Even if class is passed as variable.

## Bool variables: positive affirmative sentences, lowercased, underscores
### Yes: with `if` and `and` it reads naturally
```
if user_agrees and conditions_are_met:
    make_offer()
```
### Yes: with `while` and `not` it reads naturally
```
while not tests_are_passed:
    tests.setup()
    tests_are_passed = tests.run()
```
### Yes: subject is obvious from context
```
if form.is_valid:
    Model.from_raw(form.to_raw()).save()
```
### Yes: subject is obvious from context
```
if is_disconnected:
    reconnect()
```

## Contenxt managers: verb in past form
### Yes: `contextmanager` decorator
```
@contextmanager
def opened_connection(address):
    connection_handle = open_connection(address)
    try:
        yield connection_handle
    finally:
        close_connection(connection_handle)


def ask_peer(address):
    with opened_connection(address) as connection_handle:
        send_question_to_peer(connection_handle)
        return receive_answer_from_peer(connection_handle)
```
### Yes: class context manager
```
class OpenedConnection:
    def __init__(self, address):
        self._connection_handle = None
	self._address = address

    def __enter__():
        self._connection_handle = open_connection(self._address)
	return self._connection_handle

    def __exit__():
        close_connection(self._connection_handle)


def ask_peer(address):
    with OpenedConnection(address) as connection_handle:
        send_question_to_peer(connection_handle)
        return receive_answer_from_peer(connection_handle)
```
