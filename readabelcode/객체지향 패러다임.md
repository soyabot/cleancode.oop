객체 지향 패러다임

뇌메모리 적게쓰기
사고의 depth줄이기
공백라인 , 부정어
해피케이스 , 예외처리 
stream optional

프로그램 = 데이터 + 코드 


객체 지향 패러다임 

추상의 관점으로 바라보는 객체지향

절차지향 객체지향 함수형

추상화된 
(데이터 + 코드)

(객체간의)협력과 (객체가 담당하는 )책임
캡추상다 

관심사의 분리 
- 유지보수가 원할 
- 높은 응집도 , 낮은 결합도 


객체설계하기 
추상화 레벨

관심사 분리 

비공개 필드(데이터)
비공개 로직(기능 구현부)
object 
<-> 공개메서드 선언부
객체의 책임 
객체의 협력

객체로 추상화하기 
- 비공개 필드 (데이터 ), 비공개 로직(코드)
- 공개 메서드 선언부를 통해 외부 세계와 소통 
	-> 각 메서드의 기능은 객체의 책임을 드러내는 창구
- 객체의 책임이 나뉨에 따라 객체간 협력이 발생


객체가 제공하는 것
절차 지향에서 잘 보이지 않았던 개념을 가시화
관심사가 한 군데로 모이기 때문에 유지보수성 증가
-> 객체 내부에서 객체가 가진 데이터의 유효성 검증 책임을 가짐
여러 객체를 사용하는 입장에서는, 구체적인 구현에 신경쓰지 않고 보다 높은 추상화 레벨에서 도메인 로직을 다룰수 있다

새로운 객체를 만들 때 주의할점

- 1개의 관심사로 명확하게 책임이 정의되었는지 확인하기
-메서드를 추상화할 때와 비슷하다
-객체를 만듦으로써 외부 세계와 어떤 소통을 하려고 하는지 생각해보자

생성자, 정적 팩토리 메서드에서 유효성 검증이 가능하다
- 도메인에 특화된 검증 로직이 들어갈 수 있다

setter 사용 자제
- 데이터는 불변이 최고다. 변하는 데이터라도 객체가 핸들링 할 수 있어야한다
- 객체 내부에서 외부 세계 개입없이 자체적인 변경/ 가공으로 처리할 수 있는지 확인
-만약 외부에서 가지고 있는 데이터로 데이터 변경 요청을 해야하는 겨우 set이라는 단순 이름보다는 update같이 의도를 드러내는 네이밍을 고려하자.

getter도 처음에는 사용자제 , 반드시 필요한 경우 추가 
외부에서 객체 내 데이터가 필요하다고 getter를 남발하는 것은 무례한 행동이다

*객체에 메시지를 보내라 !

새로운 객체를 만들때 주의할점
*필드의 수는 적을 수록 좋다*

- 불필요한 데이터가 많을수록 복잡도가 높아지고 대응할 변화가 많아진다
- 필드 A를 가지고 계산할 수 있는 A'필드가 있다면, 메서드기능으로 제공
- 단, 미리 가공하는 것이 성능상 이점이 있다면 필드로 가지고 잇는 것이 좋을 수 도 있다

```java

class Bill{
	private final List<Menu> menus;
	private final long totalPrices;

public long calculateTotalPrice(){
	return this.menus.stream()
	.mapToLong(Menu::getPrice)
	.sum();
	}
}

```

계산서에서 제공하는  계산서  
미리 가공하는 것이 성능 상 이점이 있다면, 필드로 가지고 있는 것이 좋을 수도 있다.

public static final String FLAG_SIGN =

sign을 cell안으로 가지고 오려고한다

```java

public class Cell{

	private final String sign;

	private Cell(String sign){
		this.sign = sign;
		}
		
	public static Cell of(String sign){
		return new Cell(sign);
	
	}// 밖에서는 정적팩토리만 사용할 수 있게 한다
	
}

```

```java
private static final String[][ ] BOARD = new String[BOARD_ROW_SIZE][BOARD_COL_SIZE]

private static cell String[][ ] BOARD2 = new String[BOARD_ROW_SIZE][BOARD_COL_SIZE] //리팩토링 

```


```java
//변수할당 바꿔주기

Cell.of(LAND_MINE_SIGN)
//

private static boolean isAllCellOpened(){
	return Arrays.stream(BOARD2)Stream<Cell[]>
		.flatMap(Arrays::stream)Stream<Cell>
		.noneMatch(cell
		//->cell.getSign().eqals(CLOSED_CELL_SIGN))
		//get 금지 
		->cell.getSign().eqals(CLOSED_CELL_SIGN))
}
// 게터를 만들지 말고 
```


```java

public class Cell{

	private final String sign;

	private Cell(String sign){
		this.sign = sign;
		}
		
	public static Cell of(String sign){
		return new Cell(sign);
	
	}// 밖에서는 정적팩토리만 사용할 수 있게 한다

	public boolean equlSign(String sign)
	return this.sign.equals(sign);///get xx 공개메서드로 외부세개와 소통을 한다 
	
	}

}
```
But 

콘솔에 데이터를 그릴려고한다, 셀은 데이터를 줘 그려줄게 라고 한다 
이것은 get을 처리해주는 것이 맞다

```java


private static void showBoard(){
		System.out.println(" a b c d e f g h j");
	for(int row = 0; row <BOARD_ROW_SIZE; row++)P
		System.out.printf("d ", row+1);
	for(int col =0; col <BOARD_COL_SIZE; col++){
		System.out.print(BOARD[row][col].getSign()+" ")
	}
	System.out.println();
	}
	System.out.println();
}


```


```java

public class Cell{

	private final String sign;

	private Cell(String sign){
		this.sign = sign;
		}
		
	public static Cell of(String sign){
		return new Cell(sign);
	
	}// 밖에서는 정적팩토리만 사용할 수 있게 한다

	public String getSign(){
		return sign; // 여기서 게터를 만들어준다 
	}


	public boolean doesNotEqulaSign(String sign){
		return !equalSign(sign); //부정연산자
	}
}
```


//점진적인 리팩토링이 중요하다


```java


if(doesUserChooseToPlanFlag(userActionInput)){
	BOARD[selectRowIndex][selectedColIndex] = Cell.ofFlag();
	checkIfGameOver();
	return

}
.
.
.

```



```java

public class Cell{

	private final String sign;


	private int nearbyLandMineCount;

	private blooen isLandMine;




//cell이 가진 속성: 근처 지뢰 숫자, 지뢰여부
// cell의 상태: 깃발 유무 열렷다 / 닫혔다 , 사용자가 확인함은 전혀 다른것이다 . 

	private Cell(String sign, int nearbyLandMineCount,      boolean isLandMine){
	this.sign =sign;
	this.nearbyLandMineCoutn = nearbyLandMineCount;
	this.isLandMine = isLandMine;
	}

	private Cell(String sign, int nearvyLandMineCount, blooean isLandMine){
		
		
	public static Cell of(String sign){
		return new Cell(sign, nearbyLabdMineCount, isLandMine);
	}// 밖에서는 정적팩토리만 사용할 수 있게 한다
	



	public static Cell ofFlag(){
		return of(LAND_MINE_SIGN,0 ,false);
	}

	public static Cell ofFlag(){
		return of(CLOSED_CELL_SIGN,0 ,false);
	}

	public static Cell ofFlag(){
		return of(OPEND_CELL_SIGN, 0 ,false);
	}

	public String getSign(){
		return sign; // 여기서 게터를 만들어준다 
	}


	public boolean doesNotEqulaSign(String sign){
		return !equalSign(sign); //부정연산자 로직이 직관적이니깐 
	}


	public boolean isClosed(){
		return CLOSED_CELL_SIGN.equals9this.sign
		}
//





	public static Cell ofNearbyLandMineCount(int count){
	return of(String.valueOf(count)); 
}

	public static Cell ofFlag(){
	}

```


```java

if(NEARBY_LAND_N)..
	BOARD[row][col] = //Cell.ofNearbyandMine(String.valueOf(NEARBY_LAND_MINE_COUNTS[row][col])); //숫자만을 위한 리팩토링 메서드
Cell.ofNearbyLandMineCount(NEARBY_LAND_MINE_COUNTS[row][col]);
//숫자만을 받도록한다 
	return;
	}else{
		BOARD[row][col]=Cell.ofOpened();
	}

```



도메인 지식을 얻었다 

- 열렸다/ 닫혔다 는 개념과 사용자가 체크했다는 개념과 ' 사용자가 체크했다는 '개념은 다르다 
-> ex) 깃발: 닫혀있지만 체크했으므로 게임 종료 조건의 일부가 된다.

기존 board 
sign기반의 board가 있고, 이를 상황에 따라 표시할 sign을 갈아끼우는 형태에서, 이제 'Cell'이라는 정보를 담을 공간, 객체가 생겼다. Board는 cell을 갈아끼우는 곳이 아니라, 사용자 행위에 따라 cell상태를 변화시키는 방향으로 가야함

->지뢰 여부와 주변 지뢰 개수는 별도의 공간에 있었기에 가능했던 것

*도메인 지식은 만드는 것이 아니라 발견하는 것*
```java

public class Cell{
	private static final String FLAG_SIGN="깃발"
     private sttatic final String UNCHECKED_SIGN= "ㅁ"
}

```

```java
private static void initalizeGame(){
	for(int row =0; row<BOARD_ROW_SIZE;row++){
		for(int col =0; col<BOARD_COL_SIZE; col++){
		BOARD[row][col] =Cell.create();	
		
	}
}
```


```java

for(int i =0; i< LAND_MINE_COUNT; i++){
	int col = new Random.nextInt(BOARD_COL_SIZE);
	int row = new Random().nextInt(BOARD_ROW_SIZE);
	//BOARD[row][col]=true;
	BOARD[row][col]=turnOnLandMine();
}
```



```java

public void turnOnLandMine(){
	this.isLandMine =true;
}//지뢰셀 

```

```java

for(int row= 0; row< BOARD_ROW_SIZE; row++){
	for(int col = 0; col < BOARD_COL_SIZE; col++){
		if(isLandMineCell(row,col)){
		continue;
		}
	  int count = countNearbyLandMines(row, col);
		BOARD[row][col] =0;
		countine;
	  }
	  int count = countNearbyLandMines(row, col);
	  NEARBY_LAND_MINE_COUNTS[row][col] =count;
	}
}

```

---> 잘못생각한 부분 고치기 


```java
	public String getSign(){
		if(isOpened){
		if(isLandMine){
			return LAND_MINE_SIGN;
		}
		is(hasLandMineCount())
			return String.valueOf(nearbyLandMineCount);
		}
		return EMPTY_SIGN;
	}
	return sign;
	}

	if(isFlagged){
		return FLAG_SIGN;
		}
	return UNCHECKED_SIGN;	
	}
	
}

```

-> sign의 존재를 없애기


-> 데이터를 조작하며, 지금 셀의 상태가 뭐야? -> getsign에서 조작하였다

