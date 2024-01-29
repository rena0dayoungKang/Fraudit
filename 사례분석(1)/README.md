
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
step2. 원래의 분개장에서 전표번호, 전표일자 별로 group 
step3. 차변1억초과빈도.tbl에서 빈도가 1이상인 건들을 분개장예제_상세에서 상세조회<br>
![image](https://github.com/rena0dayoungKang/Fraudit/assets/127266915/89d585b8-fa11-4a1b-9249-0da9ca857ef9)
![image](https://github.com/rena0dayoungKang/Fraudit/assets/127266915/27345638-de81-44af-9c46-a768cf08c95b)

