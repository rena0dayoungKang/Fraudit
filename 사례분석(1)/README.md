
EX1) <br>
*주말분개장입력파악.tbl<br>
[분개가 발생한 요일별 거래건수와 거래금액을 분석]<br>
내부통제가 취약한 주말거래에 회계처리한 건수와 금액을 파악 
![image](https://github.com/rena0dayoungKang/Fraudit/assets/127266915/0bc6dae0-a6de-4907-824f-2e7a79e18c44)

EX2) <br>
*차변과대변일치파악.tbl<br>
[분개장에서 차변합계와 대변합계가 일치하지 않은 거래 파악]<br>
정상적인 상황에서는 전표에서 차변합계와 대변합계가 일치해야 한다. 
![image](https://github.com/rena0dayoungKang/Fraudit/assets/127266915/9f3fde26-fdfa-4c5e-bdf3-94177e26c6a1)

EX3) <br>
*차변1억초과빈도.tbl, 분개장예제_상세.tbl<br>
[분개장에서 특정금액이 초과하는 경우가 포함되는 전표파악]<br>
특정금액을 초과하는 경우가 포함된 전표를 추가분석할 경우<br> 
**차변1억초과빈도.tbl <br>
step1. 분개장에서 filter() 함수 사용하여 차변합계가 1억초과인 레코드 빈도 summarize, 일자컬럼 ascending 후 index추가 <br> 
**분개장예제_상세.tbl <br>
step2. 원래의 분개장에서 전표번호, 전표일자 별로 group <br>
step3. 차변1억초과빈도.tbl에서 빈도가 1이상인 건들을 분개장예제_상세에서 상세조회<br>
![image](https://github.com/rena0dayoungKang/Fraudit/assets/127266915/89d585b8-fa11-4a1b-9249-0da9ca857ef9)
![image](https://github.com/rena0dayoungKang/Fraudit/assets/127266915/27345638-de81-44af-9c46-a768cf08c95b)
<br>
<br>
<br>
EX4) <br>
*계정과목빈도.tbl <br>
[분개장에서 계정과목이 모두 동일한 전표 파악]<br>
전표에 모든 계정과목이 동일한 경우는 흔하지 않음<br>
계정코드로 UniqueCount  이용하여 빈도 확인, 계정과목빈도_중복제외 칼럼에서 1인것들을 추가분석<br>
![image](https://github.com/rena0dayoungKang/Fraudit/assets/127266915/50294a78-8600-4e15-9156-eb64a7064b5d)
![image](https://github.com/rena0dayoungKang/Fraudit/assets/127266915/a3e7a9a6-a962-4fdd-b8b9-140996ec5944)
![image](https://github.com/rena0dayoungKang/Fraudit/assets/127266915/12392bbc-ec77-4d7f-a2a6-1fa152cb70c6)
<br>
<br>
<br>
EX5) <br>
*<br>
[분개장에서 특정 계정과목의 차변과 대변 조건이 충족하는 경우가 포함된 전표 파악]<br>
부가세예수금의 경우 차변과 대변이 모두 0인 것이 포함되는 경우 **영세율 매출 또는 면세매출일 가능성**이 있다. <br>
step1. 분개장에서 filter(lambda x : x , zip(group[])) 함수를 이용해 계정과목이 부가세예수금이면서 차변금액이 0, 대변금액이 0인 항목을 count하는 빈도 컬럼 생성<br>
![image](https://github.com/rena0dayoungKang/Fraudit/assets/127266915/dac390dd-8ce7-4cea-b3e4-a3b011d202bf)
![image](https://github.com/rena0dayoungKang/Fraudit/assets/127266915/2b320759-fdc3-416e-85a8-9b3b1077d2d1)
<br>

EX6) <br>
*<br>
[특정 계정과목의 레코드만 추출하기]
By Fraudit Expression 메뉴 이용, ***계정과목 in ['외상매출금', '상품매출', '제품매출'] <br>


<br>
<br>

EX7) <br>
[거래처별 매출거래 빈도 분석]<br>
거래처별 매출거래 빈도를 분석하여 매출거래가 자주 일어나는 거래처와 자주 일어나지 않는 거래처 구분<br>
step1. 분개장에서 레코드빈도, 차변합계, 대변합계를 계정과목과 계정코드로 구분하는 시산표 만들기 <br>
step2. 시산표에서 관련계정 컬럼을 새로 만들고, 외상매출금의 관련계정은 매출채권으로 입력, 상품매출과 제품매출의 관련계정을 매출로 입력 <br>
step3. 외상매출, 상품매출, 제품매출의 계정코드를 포함하는 통합_리스트 를 Script로 작성. -> 리스트 컴프리헨션으로 enumerate 사용 <br>
step4. By Fraudit Expression 메뉴에서 계정코드 in 통합_리스트로 , 통합리스트에 포함하는 계정코드만 따로 분개장에서 발췌한다<br>
step5. 위의 발췌 tbl에서 거래처로 summarize 하는 차변금액합, 대변금액합, 레코드빈도 를 나타내는 거래처_요약 생성 후 index 추가 후 빈도 컬럼으로 descending <br>
step6. 발췌 tbl에서 거래처로 구분하는 group을 따로 생성 하고 거래처_상세를 생성 <br>
![image](https://github.com/rena0dayoungKang/Fraudit/assets/127266915/f79e2d60-ce80-4f40-b56c-e5b9cf707df7)
![image](https://github.com/rena0dayoungKang/Fraudit/assets/127266915/5dd4829a-1962-4c89-80b4-2e4d328d2eed)





