# BBC3004---Eng.-de-Software
Atividades e projetos da matéria de Engenharia de Software - 2024.1

Para a atividade de principios SOLID foi escolhidos os seguintes 4 principios: S - Single Responsibility Principle, O - Open-Closed Principle, L - Liskov Substitution Principle, D - Dependency Inversion Principle. Eles estão detalhados com O que é?, Para que Serve?, e os exemplos em Python. 
Demais exemplos estão na pasta 'exemplos_atividade_solid'.

### 1. S - Single Responsibility Principle
**O que é?**  
O SRP afirma que uma classe deve ter apenas uma responsabilidade.

**Para que serve?**  
Ele ajuda a manter o código modular, facilitando a manutenção, teste e reutilização.

**Exemplo em Python:**
```python
class FileManager:
    def read_file(self, file_name):
        with open(file_name, 'r') as file:
            return file.read()

    def write_file(self, file_name, data):
        with open(file_name, 'w') as file:
            file.write(data)

class DataProcessor:
    def process_data(self, data):
        # Process data here
        return processed_data

    def save_processed_data(self, processed_data):
        file_manager = FileManager()
        file_manager.write_file('processed_data.txt', processed_data)

# Exemplo de uso
data = FileManager().read_file('data.txt')
processed_data = DataProcessor().process_data(data)
DataProcessor().save_processed_data(processed_data)
```
Neste exemplo, a classe FileManager tem a responsabilidade de lidar com arquivos (leitura e escrita), enquanto a classe DataProcessor é responsável por processar dados e salvar o resultado. Cada classe tem uma única responsabilidade, seguindo o SRP.

### 2. O - Open-Closed Principle
**O que é?**  
O OCP afirma que uma classe deve ser aberta para extensão, mas fechada para modificação.

**Para que serve?**  
Isso permite que novos comportamentos sejam adicionados sem modificar o código existente.

**Exemplo em Python:**
```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14 * self.radius ** 2

# Exemplo de uso
shapes = [Rectangle(5, 4), Circle(3)]
for shape in shapes:
    print(f"Área da forma: {shape.area()}")
```
Neste exemplo, a classe Shape é abstrata e define um método area() que deve ser implementado pelas subclasses. As classes Rectangle e Circle são subclasses de Shape e fornecem implementações específicas para calcular a área de um retângulo e um círculo, respectivamente. Isso demonstra a extensibilidade sem modificar o código existente, conforme exigido pelo OCP.

### 3. L - Liskov Substitution Principle
**O que é?**  
O LSP afirma que os objetos de uma classe derivada devem poder substituir os objetos de sua classe base sem interromper o funcionamento do programa.

**Para que serve?**  
Isso garante que o código que usa as classes base continue funcionando corretamente quando objetos de subclasses são passados para ele.

**Exemplo em Python:**
```python
class Bird:
    def fly(self):
        return "Flying"

class Ostrich(Bird):
    def fly(self):
        return "Can't fly"

def bird_fly(bird):
    return bird.fly()

# Exemplo de uso
bird = Bird()
ostrich = Ostrich()

print(bird_fly(bird))   # Saída: "Flying"
print(bird_fly(ostrich))  # Saída: "Can't fly"
```
Neste exemplo, a classe Ostrich é uma subclasse de Bird que redefine o método fly() para indicar que avestruzes não podem voar. No entanto, a função bird_fly() ainda funciona corretamente quando um objeto Ostrich é passado para ela, demonstrando o princípio de substituição de Liskov.

### 4. D - Dependency Inversion Principle
**O que é?**  
O DIP afirma que módulos de alto nível não devem depender de módulos de baixo nível. Ambos devem depender de abstrações.

**Para que serve?**  
Isso permite que os módulos de alto nível sejam independentes das implementações específicas dos módulos de baixo nível, facilitando a substituição e o teste.

**Exemplo em Python:**
```python
class PaymentProcessor:
    def process_payment(self, payment_provider):
        return payment_provider.process()

class PaymentProvider:
    def process(self):
        pass

class CreditCardPaymentProvider(PaymentProvider):
    def process(self):
        return "Processing credit card payment"

class PayPalPaymentProvider(PaymentProvider):
    def process(self):
        return "Processing PayPal payment"

# Exemplo de uso
payment_processor = PaymentProcessor()
credit_card_provider = CreditCardPaymentProvider()
paypal_provider = PayPalPaymentProvider()

print(payment_processor.process_payment(credit_card_provider))
print(payment_processor.process_payment(paypal_provider))
```
Neste exemplo, a classe PaymentProcessor depende da abstração fornecida pela classe PaymentProvider, em vez de depender de implementações concretas como CreditCardPaymentProvider ou PayPalPaymentProvider. Isso permite que diferentes provedores de pagamento sejam facilmente substituídos sem modificar o código do PaymentProcessor, seguindo o DIP.
