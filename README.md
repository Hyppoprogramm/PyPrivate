# Python private

This package is adding [private/protected/public fields](https://en.wikipedia.org/wiki/Access_modifiers) to Python.

**Without PyPrivate:**
```python
class Foo():
	__x = 7 # Private "x"
	def baz(self):
		self.__x += 7

def bar(f, n):
	try:
		getattr(f, n)
	except:
		print('"' + n + '" not found')
	else:
		print('"' + n + '" found')

myfoo = Foo()
myfoo.baz()
bar(myfoo, "__x")     # "__x" not found
bar(myfoo, "_Foo__x") # "_Foo__x" found
```
**With PyPrivate**
```python
from privatefields import privatefields

@privatefields
class Foo():
	private_x = 7 # Private "x"
	def baz(self):
		self.private_x += 7

def bar(f, n):
	try:
		getattr(f, n)
	except:
		print('"' + n + '" not found')
	else:
		print('"' + n + '" found')

myfoo = Foo()
myfoo.baz()
bar(myfoo, "private_x") # "private_x" not found
print(dir(myfoo)) # no "x"
```

## How to use

PyPrivate is easy to use. To use private/protected fields import "privatefields":
```python
from privatefields import privatefields
```
Next, use it with your classes:
```python
@privatefields
class Foo():
	pass
```
And add prefixes private_/protected_ to your variables/methods names:
```python
self.z           # Public
self.protected_y # Protected
self.private_x   # Private
```

### Friends

You can declare "friend" [classes](https://en.wikipedia.org/wiki/Friend_class)/[functions](https://en.wikipedia.org/wiki/Friend_function). For this add this line to your class:
```python
class Baz(): # This class can use "x"
	pass
class Bar(): # This class can't use "x"
	pass
@privatefields
class Foo():
	friends = [Baz]
	private_x = "Secret data" # Private "x"
```
