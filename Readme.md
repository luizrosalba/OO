# Orientação a Objetos e Solid para ninjas 

## Coesão 

Coesão = SRP 

Uma classe coesa é aquela que possui uma única responsabilidade 

Toda Classe que não é coesa não para de crescer nunca 

## Segregando responsabilidades 

Se quebramos um método grande em vários pequenos métodos privados não teremos reuso 
daquele comportamento isolado 

Se precisamos ficar buscaando todos os pontos onde a função é usada o código pode melhorar

O código deve estar amarrado ou seja, deve-se deixar claro os pontos que devem ser 
alterados no código ao se adicionar um comportamento (encapsulamento do problema )

## SRP 

Uma classe deve ter uma e apenas uma razão para mudar 

## Acoplamento 

Classes devem ser coesas e pouco acopladas

A partir do momento que uma classe depende de muitas outras classes, todas elas podem propagar problemas para a classe principal

Interfaces ajudam a criar módulos estáveis 

Acoplamento não é um problema se ocorre dependência de uma interface estável

## Princípio da inversão de dependência (DIP)

Sempre que uma classe for depender de outra ela deve depender sempre de outro módulo mais estável que ela mesma 


## Abstração 

A abstração consiste em um dos pontos mais importantes dentro de qualquer linguagem Orientada a Objetos. 
Como estamos lidando com uma representação de um objeto real (o que dá nome ao paradigma), 
temos que imaginar o que esse objeto irá realizar dentro de nosso sistema.

1) O primeiro ponto é darmos uma identidade ao objeto que iremos criar. Essa identidade deve ser única dentro do sistema para que não haja conflito. Na maior parte das linguagens, há o conceito de pacotes (ou namespaces). Nessas linguagens, a identidade do objeto não pode ser repetida dentro do pacote, e não necessariamente no sistema inteiro.
2) A segunda parte diz respeito a características do objeto. Como sabemos, no mundo real qualquer objeto possui elementos que o definem. Dentro da programação orientada a objetos, essas características são nomeadas propriedades. Por exemplo, as propriedades de um objeto “Cachorro” poderiam ser “Tamanho”, “Raça” e “Idade”.
3) Por fim, a terceira parte é definirmos as ações que o objeto irá executar. Essas ações, ou eventos, são chamados métodos. Esses métodos podem ser extremamente variáveis, desde “Acender()” em um objeto lâmpada até “Latir()” em um objeto cachorro.

EX: 
1) Implementação : gato cachorro e passaro Abstração: Animal 
2) Implementação : ISS, IPVA e IPTU Abstração: Imposto
3) Implementação : homem e mulher Abstração: Humanos

Módulos de alto nível não devem depender de módulos de baixo nível. Ambos devem depender de abstrações 

Abstrações não devem depender de detalhes. Detalhes devem depender de abstrações 

## Princípio aberto-fechado (OCP) 

Classes devem ser abertas para extensão e fechadas para modificação 

Uma classe não deve ser modificada o tempo todo 

Não há razão para mudar a classe abaixo, para mudar seu comportamento basta passarmos diferentes implementações de suas dependências no construtor.

As interfaces (abstracoes) TabelaDePreco e ServicoDeEntrega devem ser estáveis

```
public class CalculadoraDePrecos { 
    private TabelaDePreco tabela;
    private ServicoDeEntrega entrega;

    public CalculadoraDePrecos(
        TabelaDePreco tabela, 
        ServicoDeEntrega entrega){

        this.tabela = tabela; 
        this.entrega = entrega;
    }
    // Nao instanciamos as deps apenas usamos

    public double calcula (Compra produto) {
        double desconto = 
            tabela.descontoPara(produto.getValor());
        double frete = entrega.para(produto.getCidade());
        return produto.getValor() * (1-desconto) + frete; 

    }

}
```

Poderiamos também injetar as dependecias usando métodos get e set entretanto usar o 
construtor obriga a passagem de dependências no momento da criação do objeto

## Encapsulamento 

A classe deve esconder os detalhes da implementação, ou seja como o método faz o seu trabalho. 


Ex: A classe ProcessadorDeBoletos não deve ter lógica de nota fiscal (intimidade inapropriada). Toda lógica de nota fiscal deve ficar na classe NotaFiscal

## Tell don't ask

Devemos dizer ao objeto o que fazer e não perguntar algo a ele para depois decidir. 

```
NotaFiscal nf = new NotaFiscal();
double valor = nf.calculaValorImpostos();
```

pág 70

## Padrões de projeto 


### Decorator 

### Observer

### Visitor 

### Factory 







