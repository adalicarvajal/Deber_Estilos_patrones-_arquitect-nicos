# Arquitectura y Patrones de Software

## Patrones Creacionales
### Factory Method

''' ejemplo 
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
'''


