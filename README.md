# Summary of the book Clean Code: A Handbook of Agile Software Craftsmanship by Robert C. Martin

## Meaningful names

### Use Intention-Revealing Names

```java
	/* Bom */
	int d; // elapsed time in days

	/* Ruim */
	int elapsedTimeInDays;
	int daysSinceCreation;
	int daysSinceModification;
	int fileAgeInDays;
```

```java
	/* Bom */
	public List<int[]> getThem() {
		List<int[]> list1 = new ArrayList<int[]>();
		for (int[] x : theList)
			if (x[0] == 4)
				list1.add(x);
		return list1;
	}

	/* Ruim */
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
* Evite l minúsculo e O maiúsculo. Confunde com 1 e 0.

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