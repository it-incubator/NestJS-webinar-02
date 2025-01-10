# Декораторы в TypeScript

Декораторы в TypeScript — это функции, которые можно применять к классам, методам, 
свойствам и параметрам методов для их модификации. Они являются мощным инструментом, 
который позволяет добавлять дополнительную функциональность к элементам программы без изменения их исходного кода.

## Виды декораторов

- **Классовый декоратор**: применяется к классу и может изменять или заменять его.
- **Декоратор метода**: применяется к методу класса и позволяет изменить поведение метода.
- **Декоратор свойства**: применяется к свойствам класса.
- **Декоратор параметра**: применяется к параметрам метода.

## Пример использования

Рассмотрим простой пример декоратора, который будет логировать вызовы метода.

```typescript
function LogMethod(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
    const originalMethod = descriptor.value;

    descriptor.value = function (...args: any[]) {
        console.log(`Вызов метода ${propertyKey} с аргументами: ${JSON.stringify(args)}`);
        return originalMethod.apply(this, args);
    };

    return descriptor;
}

class Calculator {
    @LogMethod
    add(a: number, b: number): number {
        return a + b;
    }
}

const calculator = new Calculator();
console.log(calculator.add(2, 3)); // Вызов метода add с аргументами: [2,3]
                                   // 5
