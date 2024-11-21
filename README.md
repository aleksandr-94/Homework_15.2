# Homework_15.2



from math import gcd

class Fraction:
    def __init__(self, a, b):
        if b == 0:
            raise ValueError("Denominator cannot be zero")
        self.a = a
        self.b = b
        self._reduce()

    def _reduce(self):
        """Приведение дроби к упрощенному виду."""
        common = gcd(self.a, self.b)
        self.a //= common
        self.b //= common

    def __mul__(self, other):
        if isinstance(other, Fraction):
            return Fraction(self.a * other.a, self.b * other.b)
        return NotImplemented

    def __add__(self, other):
        if isinstance(other, Fraction):
            numerator = self.a * other.b + other.a * self.b
            denominator = self.b * other.b
            return Fraction(numerator, denominator)
        return NotImplemented

    def __sub__(self, other):
        if isinstance(other, Fraction):
            numerator = self.a * other.b - other.a * self.b
            denominator = self.b * other.b
            return Fraction(numerator, denominator)
        return NotImplemented

    def __eq__(self, other):
        if isinstance(other, Fraction):
            return self.a == other.a and self.b == other.b
        return False

    def __gt__(self, other):
        if isinstance(other, Fraction):
            return self.a * other.b > self.b * other.a
        return NotImplemented

    def __lt__(self, other):
        if isinstance(other, Fraction):
            return self.a * other.b < self.b * other.a
        return NotImplemented

    def __str__(self):
        return f"Fraction: {self.a}, {self.b}"

f_a = Fraction(2, 3)
f_b = Fraction(3, 6)
f_c = f_b + f_a
assert str(f_c) == 'Fraction: 21, 18'

f_d = f_b * f_a
assert str(f_d) == 'Fraction: 6, 18'

f_e = f_a - f_b
assert str(f_e) == 'Fraction: 3, 18'

assert f_d < f_c  # True
assert f_d > f_e  # True
assert f_a != f_b  # True

f_1 = Fraction(2, 4)
f_2 = Fraction(3, 6)
assert f_1 == f_2  # True

print("Все тесты пройдены!")
