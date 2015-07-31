# Summary of the book Clean Code: A Handbook of Agile Software Craftsmanship by Robert C. Martin

## Meaningful names

### Use Intention-Revealing Names

```java
	/* Bad */
	int d; // elapsed time in days

	/* Good */
	int elapsedTimeInDays;
	int daysSinceCreation;
	int daysSinceModification;
	int fileAgeInDays;
```

```java
	/* Bad */
	public List<int[]> getThem() {
		List<int[]> list1 = new ArrayList<int[]>();
		for (int[] x : theList)
			if (x[0] == 4)
				list1.add(x);
		return list1;
	}

	/* Good */
	public List<Cell> getFlaggedCells() {
		List<Cell> flaggedCells = new ArrayList<Cell>();
		for (Cell cell : gameBoard)
			if (cell.isFlagged())
				flaggedCells.add(cell);
		return flaggedCells;
	}
```