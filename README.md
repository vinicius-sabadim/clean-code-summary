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

* Produto, ProductInfo e ProductData não tem diferença significativa nenhuma.

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