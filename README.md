# Taller-de-parcial-POO
solución al taller propuesto en POO
por David Sotelo  



## Ejercicio 1

```python
class A:
    x = 1
    _y = 2
    __z = 3
a = A()

print("a.x" , a.x)
print("a._y" , a._y)
print("a._A__z" , a._A__z)

print("a.__z" , a.__z) 
#No existe a.__z.
```

## Ejercicio 2
```python
class A:
    def __init__(self):
        self.__secret = 42
a = A()
print(hasattr(a, '__secret'), hasattr(a, '_A__secret'))
#Se imprime: False True.
```

## Ejercicio 3

a) El prefijo _ impide el acceso desde fuera de la clase.
❌ Falso, se puede acceder:

```python
class Gafas:
    _dioptria = 2.5

a = Gafas()
print(a._dioptria)
```
b) El prefijo __ hace imposible acceder al atributo.
❌ Falso, se puede acceder con name mangling:

```python
class Animal:
    __mascota = "perro"

a = Animal()
print(a._Animal__mascota)
```
c) El name mangling depende del nombre de la clase.
✔️ Verdadero, ya que __algo pasa a _NombreDeLaClase__algo.

## Ejercicio 4
```python
class Base:
    def __init__(self):
        self._token = "abc"
class Sub(Base):
    def reveal(self):
        return self._token
print(Sub().reveal())
```
Imprime "abc" porque Sub hereda _token de Base.

## Ejercicio 5
```python
class Base:
    def __init__(self):
        self.__v = 1
class Sub(Base):
    def __init__(self):
        super().__init__()
        self.__v = 2
    def show(self):
        return (self.__v, self._Base__v)
print(Sub().show())
```
Salida: (2, 1).

## Ejercicio 6
```python
class Caja:
    __slots__ = ('x',)

c = Caja()
c.x = 10
c.y = 20
```
❌ Da error, porque y no está en __slots__.

## Ejercicio 7
Código incorrecto:

```python
class B:
    def __init__(self):
        self ______ = 99
```
Debe corregirse a:
```python
class B:
    def __init__(self):
        self._Nombre = 99
```

## Ejercicio 8
```python
class M:
    def __init__(self):
        self._state = 0
    def _step(self):
        self._state += 1
        return self._state
    def __tick(self):
        return self._step()
m = M()
print(hasattr(m, '_step'), hasattr(m, '__tick'), hasattr(m, '_M__tick'))
```
Salida: True False True.

## Ejercicio 9
```python
class S:
    def __init__(self):
        self.__data = [1, 2]
    def size(self):
        return len(self.__data)
s = S()

print(s._S__data)
```

Ejercicio 10
```python
class D:
    def __init__(self):
        self.__a = 1
        self._b = 2
        self.c = 3
d = D()
names = [n for n in dir(d) if 'a' in n]
print(names)
```
Salida: ['_D__a'].

## Ejercicio 11
```python
class Cuenta: 
    def __init__(self, saldo): 
        self._saldo = 0 
        self.saldo = saldo
    @property 
    def saldo(self): 
        return self._saldo
    @saldo.setter 
    def saldo(self, value): 
        if value < 0: 
            raise ValueError("El saldo no puede ser negativo")
        self._saldo = value
```

## Ejercicio 12
```python
class Termometro: 
    def __init__(self, temperatura_c): 
        self._c = float(temperatura_c) 
 
    @property
    def temperatura_f(self):
        return self._c * 9/5 + 32
```

## Ejercicio 13
```python
class Usuario:
    def __init__(self, nombre):
        self.nombre = nombre

    @property
    def nombre(self):
        return self._nombre
    @nombre.setter
    def nombre(self, value):
        if not isinstance(value, str):
            raise TypeError("El nombre debe ser de tipo str")
        self._nombre = value
```

## Ejercicio 14
```python
class Registro: 
    def __init__(self): 
        self.__items = [] 
 
    def add(self, x): 
        self.__items.append(x)

    @property
    def items(self):
        return tuple(self.__items)
```
