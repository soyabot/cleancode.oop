srp : single resposibility principle
ocp: open-close principle
lsp: liskov substitution principle
isp: interfase segregation principle
dip : dependency inversion principle

SRP:단일 책임 원칙

세모 별 책임을 가질때 = 별/ 세모 원칙을 갖게
- 하나의 클래스는 단 한가지의 변경 이유만을 가져야한다.
-> 변경 이유 = 책임

- 객체가 가진 공개 메서드, 필드, 상수 등은 해당 객체의 단일 책임에 의해서만 변경되는가?

- 관심사의 분리

- 높은 응집도, 낮은 결합도

---
'책임'을 볼 줄 아는 눈이 필요하다

```java
public static void main(String[] args){
	showGameStartComments();
	initializeGame();

}

```


게임을 실행하는 main 과
// 지뢰찾기를 실행하는 클래스를 별도로 두면 어떨까?


```java
	public class Minesweeper{
	
	}
//모든 함수를 위 클래스에 둘것이다
``` 

```java

public static void main(String[] args){
	Minesweeper minesweeper = new Minesweeper();
	minesweeper.run();
}

```
->  static 없애주기 


입력 핸들러 분리

```java


private final ConsoleInputHandler consoleInputHandler = new CosoleInputHandler();


private final ConsoleOutputHandler consoleOutputHandler = new CosoleOutputHandler();



```


```java

public class ConsoleOutPutHandler{
	void showGameStartComments(){
	sout..
	sout..
	sout...
	}
}
```


```java
public void run(){
	consoleOutputHandler.showGameStartComments();
	initializeGame();
}
	while(true){
		try{
			consoleOutputHandler.showBoard(BOARD);

		if(doesUserWinTheGame()){
			
		}

		if(doesIserLoseTheGame()){			consoleOutputHandler.printGameLosingComment();
			break;
			}
	String cellInput = getCellInputFromUser();
	String userAcctionInput = getUserActionInputFromUser();
	actInCell(cellInput,userActionInput);
	}catch (AppException e){
		consoleOutputHandler.printExceptionMessage(e);
//consoleOutputHandler.printExceptionMessage(e.getMessage());
}
	
	}
	
	}
}

```


```java

public class GameBoard{

	private final Cell[][] board = new Cell[BOARD_ROW_SIZE][BOARD_COL_SIZE];
	
	public GameBoard(int rowSize, intk colSize){
	
	board = new Cell[rowSize][colSize]
		
	}
	
}
```


