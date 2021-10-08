## Propriedades (Atributos)
 ### Stored Properties
 - Uma constante (let) ou variável (var) que é parte de um instância de classe ou struct
 - Tipo mais simples, sendo possível atribuir um valor default

 <img src="https://www.dropbox.com/s/2lruwehx887jptd/classe.png" alt="Atributos (Propriedades) e Métodos" width="600" height="480">

==> Crie uma classe conforme a figura e exponha uma situação em que uma propriedade tem um valor default em tempo de execução. 

```swift runnable
class FixedLengthRange {
    var firstValue: Int
    var length: Int
    
    init(firstValue: Int, length: Int ) {
        self.firstValue = firstValue
        self.length = length
    }
}

var rangeOfThree = FixedLengthRange(firstValue: 0, length: 3)

```