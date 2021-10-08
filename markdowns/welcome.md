 ## Propriedades (Atributos)
 ### Stored Properties
 - Uma constante (let) ou variável (var) que é parte de um instância de classe ou struct
 - Tipo mais simples, sendo possível atribuir um valor default

 <img src="https://www.dropbox.com/s/2lruwehx887jptd/classe.png?dl=0" alt="Atributos (Propriedades) e Métodos" width="600" height="480">

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

 ### Lazy Stored Properties
 
 * É uma propriedade a qual seu valor só é calculado quando é usada a primeira vez
 * Usada onde valores iniciais dependem de fatores externos
 * Usada quando existe uma inicialização custosa ou complexa
 * A palavra-chave (palavra-reservada) é `lazy`

 ==> Veja o exemploa abaixo. Você consegue pensanr em uma situação custosa computacionamente? Veja esse artigo: 
 
 Inglês: https://www.hackingwithswift.com/example-code/language/what-are-lazy-variables 

 Portugês (tradução google) : https://www-hackingwithswift-com.translate.goog/example-code/language/what-are-lazy-variables?_x_tr_sl=en&_x_tr_tl=pt&_x_tr_hl=pt-BR&_x_tr_pto=nui

 ==> Use sua criatividade e crie uma simulação (semelhante ao exemplo) em que se justifique um atributo lazy.

```swift runnable 
/* Esta classe é responsável por fazer o download de arquivos muito grandes. */
class DownloadFile {
    var fileName = "My Big File"
    var fileData = ["D1", "D2", "D3", "...","D1000000"]
}  

/* Esta classe é responsável por carregar e manipular os arquivos. */
class DataManager {
  //como o download pode demorar muito a inicialização desse atributo deve ser postergada (lazy)
  lazy var importer = DownloadFile ()
  var data: [String] = []
  func prepareData() {
    for str in importer.fileData {
      data.append("myPrefix_"+str) 
    }
  }

  func show() {
    print (importer.fileName)
    for str in data {
      print(str)
    }
  } 

}

let manager = DataManager()
manager.prepareData()
manager.show()
}
```

### Computed Properties (Propriedades Calculadas)
 
 * Não armazenam um valor propriamente dito, por exemplo, a densidade demográfica é por definição a razão de habitantes/km2. Logo se existir um atributo num de habitantes e área não é necessário ter um atributo que armazene um valor (densidade demográfica), mas que seja calculado quando precisar. 

* Provêm um getter (veja que tem um return) e um setter (veja que tem um parâmetro de entrada). Em alguns caso não o setter não é necessário. 

 * No exemplo abaixo o centro de um retângulo é calculado em função de sua posição (x,y => canto superior esquerdo => Top Left).

 ==> Faça um desenho esquemático para o exemplo abaixo, a ideia é exibir um plano carteziano e mostrar a dinâmica das estruturas

 ==> Faça um exemplo (use a criatividade) em que apareçam atributos calculados, sugestão densidade demográfica, força (f=ma), etc.



 */
```swift runnable
struct Ponto {
    var x = 0.0 , y = 0.0
}

struct Dimensao {
    //largura e altura
    var largura = 0.0, altura = 0.0
}

struct Retangulo {
    //ponto superior (y) esquerdo (x) =topLeft(x,y)
    var origem = Ponto()
    var dimensao = Dimensao()
    
    var centro: Ponto {
        get {
            let centroX = origem.x + (dimensao.largura/2)
            let centroY = origem.y + (dimensao.altura/2)
            return Ponto(x: centroX, y: centroY)
        }

        set (novoCentro) {
            origem.x = novoCentro.x - (dimensao.largura/2)
            origem.y = novoCentro.y - (dimensao.altura/2)
        }
    }
}

let p1 = Ponto (x:10,y:10)
let tamanho = Dimensao (largura:100, altura:100)

var quadrado = Retangulo(origem:p1, dimensao:tamanho)
print(quadrado.origem)
print(quadrado.centro)

quadrado.centro = Ponto (x:50,y:50)

print(quadrado.origem)
print(quadrado.centro)

```