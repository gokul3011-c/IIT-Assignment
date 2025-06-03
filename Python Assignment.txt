
from abc import ABC, abstractmethod

class SmartDevice(ABC):
    def __init__(self, name):
        self._name = name
        self.__is_on = False

    @abstractmethod
    def operate(self):
        pass

    def show_status(self):
        status = "ON" if self.__is_on else "OFF"
        print(f"{self._name} is currently {status}")

    def turn_on(self):
        self.__is_on = True

    def turn_off(self):
        self.__is_on = False

    def is_on(self):
        return self.__is_on


class SmartLight(SmartDevice):
    def __init__(self, name):
        super().__init__(name)
        self.__brightness = 70

    def operate(self):
        self.turn_on()
        print(f"{self._name} light is now ON at {self.__brightness}% brightness")

    def set_brightness(self, level):
        if 0 <= level <= 100:
            self.__brightness = level
        else:
            print("Brightness should be between 0 and 100")

    def get_brightness(self):
        return self.__brightness


class SmartFan(SmartDevice):
    def __init__(self, name):
        super().__init__(name)
        self.__speed = "Medium"

    def operate(self):
        self.turn_on()
        print(f"{self._name} fan is spinning at {self.__speed} speed")

    def set_speed(self, speed):
        if speed in ["Low", "Medium", "High"]:
            self.__speed = speed
        else:
            print("Speed should be 'Low', 'Medium', or 'High'")

    def get_speed(self):
        return self.__speed


class SmartAC(SmartDevice):
    def __init__(self, name):
        super().__init__(name)
        self.__temperature = 24

    def operate(self):
        self.turn_on()
        print(f"{self._name} AC is now ON, set to {self.__temperature}°C")

    def set_temperature(self, temp):
        if 16 <= temp <= 30:
            self.__temperature = temp
        else:
            print("Temperature should be between 16°C and 30°C")

    def get_temperature(self):
        return self.__temperature




light = SmartLight("Living Room Light")
fan = SmartFan("Bedroom Fan")
ac = SmartAC("Office AC")

light.operate()
light.show_status()

fan.operate()
fan.show_status()

ac.operate()
ac.show_status()

print("\nTrying to access private variables directly:")

try:
    print(light.__brightness)
except AttributeError:
    print("Cannot access '__brightness' directly.")

try:
    fan.__speed = "High"
    print("Directly set fan speed to:", fan.__speed)
except AttributeError:
    print("Cannot access '__speed' directly.")

print("\nUpdating values using setters:")

light.set_brightness(85)
print("Brightness is now:", light.get_brightness())

fan.set_speed("High")
print("Fan speed is now:", fan.get_speed())

ac.set_temperature(22)
print("AC temperature is now:", ac.get_temperature())
