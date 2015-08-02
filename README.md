# Summary of the book Clean Code: A Handbook of Agile Software Craftsmanship by Robert C. Martin

## Meaningful names

### Use Intention-Revealing Names

```java
/* Ruim */
int d; // elapsed time in days

/* Bom */
int elapsedTimeInDays;
int daysSinceCreation;
int daysSinceModification;
int fileAgeInDays;
```

```java
/* Ruim */
public List<int[]> getThem() {
	List<int[]> list1 = new ArrayList<int[]>();
	for (int[] x : theList)
		if (x[0] == 4)
			list1.add(x);
	return list1;
}

/* Bom */
public List<Cell> getFlaggedCells() {
	List<Cell> flaggedCells = new ArrayList<Cell>();
	for (Cell cell : gameBoard)
		if (cell.isFlagged())
			flaggedCells.add(cell);
	return flaggedCells;
}
```

### Avoid Disinformation
* Evite usar variáveis com nomes referindo a uma estrutura de dados, por exemplo, accountList. Prefira accountGroup, bunchOfAccounts ou accounts.
* Evite L minúsculo e O maiúsculo. Confunde com 1 e 0.

* Evite number-series
```java
public static void copyChars(char a1[], char a2[]) {
	for (int i = 0; i < a1.length; i++) {
		a2[i] = a1[i];
	}
}
```
Ficaria bem melhor se a1 fosse source e a2 fosse destination.

* `Product`, `ProductInfo` e `ProductData` não tem diferença significativa nenhuma.

### Use Pronunceable Names
```java
/* Ruim */
class DtaRcrd102 {
	private Date genymdhms;
	private Date modymdhms;
	private final String pszqint = "102";
/* ... */
};

/* Bom */
class Customer {
	private Date generationTimestamp;
	private Date modificationTimestamp;;
	private final String recordId = "102";
	/* ... */
};
```

### Use Searchable Names
```java
/* Ruim */
for (int j=0; j<34; j++) {
	s += (t[j]*4)/5;
}

/* Bom */
int realDaysPerIdealDay = 4;
const int WORK_DAYS_PER_WEEK = 5;
int sum = 0;
for (int j=0; j < NUMBER_OF_TASKS; j++) {
	int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
	int realTaskWeeks = (realdays / WORK_DAYS_PER_WEEK);
sum += realTaskWeeks;
}
```

### Avoid Encodings
Em vez de chamar uma interface de `IShapeFactory` e a implementação de `ShapeFactory`, prefira nomear a implementação. Assim, prefira os nomes `ShapeFactory` e `ShapeFactoryImp`.

### Avoid Mental Mapping
Evite usar nomes que precisam ser pensados como sendo outra coisa. Um caso típico é utilizar variáveis com somente 1 letra. Por exemplo, associar a variável u para armazenar a url sem o host.

### Class Names
Utilize substantivos e frases substantivas. Use `Customer`, `WikiPage`, `Account` e `AddressParser`. Não use `Manager`, `Processor`, `Data` ou `Info`.

### Method Names
Utilize verbos e frases verbais. Use `postPayment`, `deletePage` ou `save`.
Acesso, mutação e predicado deve ter o valor e os prefixos: `get`, `set` e `is`.

```java
string name = employee.getName();
customer.setName("mike");
if (paycheck.isPosted())...
```

### Don't Be Cute
Não utilize termos engraçados ou com dependência cultural.
Em vez de `HolyHandGrenade` use `DeleteItems`.

> Escreva o que significa.

### Pick One Word per Concept
Utilize a mesma palavra para descrever o mesmo conceito durante o código. Não use `fetch`, `retrieve` e `get` com a mesma função em diferentes métodos.
É confuso ter `controller`, `manager` e `driver` no mesmo código.

### Don't pun
Evite usar a mesma palavra para 2 própósitos. Supondo que no seu código, existem várias classes com o método ```add``` que serve para concatenar 2 valores. Em uma nova classe existe a necessidade de ter um método que adiciona um novo item em uma coleção. Parece razoável usar `add` como nome, pois já existem outros métodos `add` no código. No entanto, um nome mais semântico seria `insert` ou `append`.

### Use Solution Domain Names
Quem lê o seu código é um programador. Então vá em frente e use termos de computação, nomes de algoritmos, nomes de padrões, termos matemáticos.

### Use Problem Domain Names
Utilize nomes que descrevam problemas do domínio quando não existir um termo computacional para descrever.

### Add Meaningful Context
Existem termos que por si só são explicativas.
Variáveis como: `firstName`, `lastName`, `street`, `houseNumber`, `city`, `state` e `zipcode`, quando utilizadas juntas remetem ao contexto de endereço. Já o uso separado não é claro o suficiente.

```java
/* Ruim - variáveis sem contexto claro */
private void printGuessStatistics(char candidate, int count) {
	String number;
	String verb;
	String pluralModifier;
	
	if (count == 0) {
		number = "no";
		verb = "are";
		pluralModifier = "s";
	} else if (count == 1) {
		number = "1";
		verb = "is";
		pluralModifier = "";
	} else {
		number = Integer.toString(count);
		verb = "are";
		pluralModifier = "s";
	}

	String guessMessage = String.format(
		"There %s %s %s%s", verb, number, candidate, pluralModifier
	);

	print(guessMessage);
}

/* Bom - variáveis têm um contexto */
public class GuessStatisticsMessage {
	private String number;
	private String verb;
	private String pluralModifier;

	public String make(char candidate, int count) {
		createPluralDependentMessageParts(count);
		return String.format(
			"There %s %s %s%s",
			verb, number, candidate, pluralModifier );
	}

	private void createPluralDependentMessageParts(int count) {
		if (count == 0) {
			thereAreNoLetters();
		} else if (count == 1) {
			thereIsOneLetter();
		} else {
			thereAreManyLetters(count);
		}
	}

	private void thereAreManyLetters(int count) {
		number = Integer.toString(count);
		verb = "are";
		pluralModifier = "s";
	}

	private void thereIsOneLetter() {
		number = "1";
		verb = "is";
		pluralModifier = "";
	}

	private void thereAreNoLetters() {
		number = "no";
		verb = "are";
		pluralModifier = "s";
	}
}
```

### Don't Add Gratuitous Context
* Não adicione mais contexto do que o necessário. Por exemplo, na aplicação "Gas Station Deluxe", todas as classes não precisam começar com GSD.
* Nomes curtos são melhores do que longos, desde que seja claro.
Os nomes `accountAddress` e `costumerAddress` são bons nomes para instâncias da classe `Address`. `Address` é um bom nome para uma classe.

### Final Words
> Não tenha medo de renomear sempre que for necessário.

## Functions