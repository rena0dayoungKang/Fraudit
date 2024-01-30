EX1 ) <br>
[송장 부정 내역 파악] <br>
🔍거래처에 지불할 때 필요 이상의 많은 금액의 수표를 작성하는 경우 <br>
송장1 과 송장2 테이블을 송장번호로 inner join <br>
조인 테이블에서 수표금액 - 송장금액 인 차이 컬럼 생성, 차이 != 0 으로 필터조회<br>
![image](https://github.com/rena0dayoungKang/Fraudit/assets/127266915/6d5f1d53-2508-4b1e-a53a-668035edeb02)
<br>
<br>
EX2) <br>
[순차적인 송장번호가 많은 경우의 적발] <br>
🔍직원이 가상의 회사를 만들어 송장이나 청구서를 보내는 경우 이런 회사는 직원이 속해 있는 회사가 유일한 고객일 **가능성**이 있다. <br>
순차적으로 되어 있는 송장의 비율을 거래처별로 계산 후 이 비율을 결과 테이블에 추가 <br>
송장 테이블에서 Vendor 기준으로 group화 한다. 그룹화 된 테이블에서 Invoice_Shift 추가 <br>
차이 컬럼 생성, Invoice_Shift가 0인 경우 0으로 차이 값 입력, else  Invoice - Invoice_Shift == 1이라면 1으로 입력하고 아니라면 0<br>
Exisiting Table List 메뉴에서 그룹을 기준으로 summarize, 차이의 Sum 을 연속빈도, count(group['차이']) -1 을 차이빈도 로 하는 요약 테이블 생성 <br>
연속빈도 / 차이빈도 로 하는 연속비율 칼럼 생성 <br>
![image](https://github.com/rena0dayoungKang/Fraudit/assets/127266915/ba545564-2394-472b-9453-74da4addf555)
<br>
<br>
