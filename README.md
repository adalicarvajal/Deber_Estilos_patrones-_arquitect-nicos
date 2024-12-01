# Arquitectura y Patrones de Software

## Ejecución de los Ejemplos

### Abrir un Editor o Terminal
- Puedes usar cualquier editor como Visual Studio Code, PyCharm, o incluso un editor de texto básico.
- Abre el terminal en la carpeta donde guardarás los archivos.

### Crear Archivos para Cada Ejemplo
Guarda cada ejemplo en un archivo separado. Por ejemplo:
- `factory_method.py`
- `abstract_factory.py`
- `adapter.py`
- etc.

### Copiar y Pegar el Código en Cada Archivo
Copia el código de cada patrón en su respectivo archivo.

### Ejecutar los Archivos
1. Ve al terminal y navega hasta la carpeta donde guardaste los archivos.
2. Ejecuta cada archivo con el comando:

   ```bash
   python nombre_archivo.py


## Patrones Creacionales
### Factory Method

```python
from abc import ABC, abstractmethod
# Producto
class Vehicle(ABC):
    @abstractmethod
    def create(self):
        pass
# Productos concretos
class Car(Vehicle):
    def create(self):
        return "Car created!"
class Motorcycle(Vehicle):
    def create(self):
        return "Motorcycle created!"
# Fábrica
class VehicleFactory(ABC):
    @abstractmethod
    def get_vehicle(self):
        pass
class CarFactory(VehicleFactory):
    def get_vehicle(self):
        return Car()
class MotorcycleFactory(VehicleFactory):
    def get_vehicle(self):
        return Motorcycle()
# Uso
factory = CarFactory()
vehicle = factory.get_vehicle()
print(vehicle.create())  # Salida: "Car created!"
```
### Abstract Factory
```python
from abc import ABC, abstractmethod

# Abstract Factory
class FurnitureFactory(ABC):
    @abstractmethod
    def create_chair(self):
        pass
    
    @abstractmethod
    def create_table(self):
        pass

# Productos concretos
class ModernChair:
    def description(self):
        return "Modern Chair"

class ModernTable:
    def description(self):
        return "Modern Table"

class VictorianChair:
    def description(self):
        return "Victorian Chair"

class VictorianTable:
    def description(self):
        return "Victorian Table"

# Fábricas concretas
class ModernFurnitureFactory(FurnitureFactory):
    def create_chair(self):
        return ModernChair()
    
    def create_table(self):
        return ModernTable()

class VictorianFurnitureFactory(FurnitureFactory):
    def create_chair(self):
        return VictorianChair()
    
    def create_table(self):
        return VictorianTable()

# Uso
factory = ModernFurnitureFactory()
chair = factory.create_chair()
table = factory.create_table()
print(chair.description())  # Salida: "Modern Chair"
print(table.description())  # Salida: "Modern Table"
```
## Patrones Estructurales
### Adapter

```python
class OldSystem:
    def specific_request(self):
        return "From Old System"

class NewSystem:
    def request(self):
        pass

class Adapter(NewSystem):
    def __init__(self, old_system):
        self.old_system = old_system
    
    def request(self):
        return self.old_system.specific_request()

# Uso
old_system = OldSystem()
adapter = Adapter(old_system)
print(adapter.request())  # Salida: "From Old System"
```
### Composite
```python
from abc import ABC, abstractmethod

class Component(ABC):
    @abstractmethod
    def operation(self):
        pass

class Leaf(Component):
    def operation(self):
        return "Leaf"

class Composite(Component):
    def __init__(self):
        self.children = []
    
    def add(self, component):
        self.children.append(component)
    
    def operation(self):
        results = [child.operation() for child in self.children]
        return f"Composite({', '.join(results)})"

# Uso
leaf1 = Leaf()
leaf2 = Leaf()
composite = Composite()
composite.add(leaf1)
composite.add(leaf2)
print(composite.operation())  # Salida: "Composite(Leaf, Leaf)"
```
### Proxy

```python
class RealObject:
    def operation(self):
        return "Real Object Operation"

class Proxy:
    def __init__(self, real_object):
        self.real_object = real_object
    
    def operation(self):
        # Control adicional
        return f"Proxy: {self.real_object.operation()}"

# Uso
real = RealObject()
proxy = Proxy(real)
print(proxy.operation())  # Salida: "Proxy: Real Object Operation"
```
### Facade

```python
class SubsystemA:
    def operation_a(self):
        return "Subsystem A"

class SubsystemB:
    def operation_b(self):
        return "Subsystem B"

class Facade:
    def __init__(self):
        self.sub_a = SubsystemA()
        self.sub_b = SubsystemB()
    
    def operation(self):
        return f"{self.sub_a.operation_a()} + {self.sub_b.operation_b()}"

# Uso
facade = Facade()
print(facade.operation())  # Salida: "Subsystem A + Subsystem B"
```
## Patrones de Comportamiento
### Command
```python
class Command:
    def execute(self):
        pass

class LightOnCommand(Command):
    def execute(self):
        return "Light is ON"

class LightOffCommand(Command):
    def execute(self):
        return "Light is OFF"

class Invoker:
    def __init__(self):
        self.history = []
    
    def execute_command(self, command):
        self.history.append(command)
        return command.execute()

# Uso
invoker = Invoker()
print(invoker.execute_command(LightOnCommand()))  # Salida: "Light is ON"
```
### Observer
```python
class Subject:
    def __init__(self):
        self._observers = []
    
    def add_observer(self, observer):
        self._observers.append(observer)
    
    def notify(self, data):
        for observer in self._observers:
            observer.update(data)

class Observer:
    def update(self, data):
        print(f"Observer received: {data}")

# Uso
subject = Subject()
observer = Observer()
subject.add_observer(observer)
subject.notify("Event Occurred!")  # Salida: "Observer received: Event Occurred!"
```
### Strategy
```python
class Strategy:
    def execute(self, data):
        pass

class ConcreteStrategyA(Strategy):
    def execute(self, data):
        return f"Strategy A with {data}"

class ConcreteStrategyB(Strategy):
    def execute(self, data):
        return f"Strategy B with {data}"

class Context:
    def __init__(self, strategy):
        self.strategy = strategy
    
    def set_strategy(self, strategy):
        self.strategy = strategy
    
    def execute_strategy(self, data):
        return self.strategy.execute(data)

# Uso
context = Context(ConcreteStrategyA())
print(context.execute_strategy("data"))  # Salida: "Strategy A with data"
context.set_strategy(ConcreteStrategyB())
print(context.execute_strategy("data"))  # Salida: "Strategy B with data"
```

