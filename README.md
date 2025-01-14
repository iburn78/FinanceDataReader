# FinanceDataReader
[FinanceData.KR](FinanceData.KR) Open Source Financial data reader 

***2018-2022 [FinanceData.KR](http://financedata.kr)***

# Overview
The FinanceDataReader is financial data reader(crawler) for finance. <br>
The main functions are as follows.

* KRX Stock listings (시장별 상장 종목 리스팅): 'KRX', 'KOSPI', 'KODAQ', 'KONEX'
* Global Stock Symbol listings(해외 거래소 상장 종목 리스팅): 'NASDAQ', 'NYSE', 'AMEX', 'S&P500', 'SSE'(상해), 'SZSE'(심천), 'HKEX'(홍콩), 'TSE'(도쿄)
* KRX delistings: 'KRX-DELISTING'(상장폐지종목), 'KRX-ADMINISTRATIVE' (관리종목), 'KRX-MARCAP'(시가총액)
* ETF Symbol listings: 'ETF/KR'
* Stock price(개별종목 가격 데이터): '005930'(Samsung), '091990'(Celltrion Healthcare) ...
* Stock price(해외 거래소 개별종목 가격 데이터): 'AAPL', 'AMZN', 'GOOG' ... (you can specify exchange(market) and symbol)
* Indexes: 'KS11'(코스피지수), 'KQ11'(코스닥지수), 'DJI'(다우존스지수), 'IXIC'(나스닥지수), 'US500'(S&P 500지수) ...
* Exchanges: 'USD/KRX', 'USD/EUR', 'CNY/KRW' ... (조합가능한 화폐별 환율 데이터 일자별 데이터)
* Cryptocurrency price data (암호화폐 가격 데이터): 'BTC/USD', 'ETH/KRW'

    
# Install

```bash
pip install finance-datareader
```

# Quick Start
지원하는 거래소: KRX(한국거래소), NYSE(뉴욕증권거래소), NASDAQ(나스닥), AMEX(아멕스), SSE(상해), SZSE(심천), HKEX(홍콩), TSE(도쿄)

```python

import FinanceDataReader as fdr

# KOSPI Index 코스피 지수 데이터 
df = fdr.DataReader('KS11') # 전체(1996 ~ 현재)
df = fdr.DataReader('KS11', '2020') # 2020 ~ 현재
df = fdr.DataReader('KS11', '2020-01-01', '2020-12-31') # 2020-01-01 ~ 2020-12-31

# KRX Indices 국내 지수 데이터
df = fdr.DataReader('KS11') # KOSPI 지수 (KRX)
df = fdr.DataReader('KQ11') # KOSDAQ 지수 (KRX)
df = fdr.DataReader('KS200') # KOSPI 200 (KRX)

# US market Indices 미국 시장 지수 데이터
df = fdr.DataReader('DJI') # 다우존스 지수 (DJI - Dow Jones Industrial Average)
df = fdr.DataReader('IXIC') # 나스닥 종합지수 (IXIC - NASDAQ Composite)
df = fdr.DataReader('US500') # S&P 500 지수 (NYSE)
df = fdr.DataReader('RUT') # 러셀2000 지수 (RUT - US Small Cap 2000)
df = fdr.DataReader('VIX') # VIX지수 (VIX - CBOE Volatility Index)

# Global Indices 글로벌 지수 데이터
df = fdr.DataReader('SSEC') # 상해 종합지수 Shanghai (SSEC -Shanghai Composite)
df = fdr.DataReader('HSI') # 항셍지수 (HSI - Hang Seng)
df = fdr.DataReader('N225') # 일본 닛케이지수 (N225 - Nikkei 225)
df = fdr.DataReader('FTSE') # 영국 FTSE100 (FTSE 100 - Financial Times Stock Exchange)
df = fdr.DataReader('FCHI') # 프랑스 FCHI 지수 (CAC 40 - CAC quarante)
df = fdr.DataReader('GDAXI') # 독일 닥스지수  (DAX30 - germany-30)

# KRX stock price 국내 시장 개별종목
df = fdr.DataReader('005930') # 삼성전자 전체 (1998 ~ 현재)
df = fdr.DataReader('000660') # SK하이닉스
df = fdr.DataReader('068270') # 셀트리온

# 여러 종목 한번에 종가(Close) 데이터
삼성전자(005930), SK하이닉스(000660), 기아(000270), 카카오(035720), KB금융(105560)
df = fdr.DataReader('005930,000660,000270,035720,105560', '2020') 

# US stock price 미국 시장 개별종목
df = fdr.DataReader('AAPL', '2017') # Apple(AAPL), 2017-01-01 ~ Now
df = fdr.DataReader('F', '1980-01-01', '2022-10-01') # Ford 자동차(F) (40년)
df = fdr.DataReader('AMZN', '2017', '2019-12-31') # AMAZON(AMZN), 2017~2019 (3년)

# 여러종목 한번에 종가(Close) 데이터
df = fdr.DataReader('AAPL, TSLA, AMZN', '2020') # 애플, 테슬라, 아마존

# TSE (도쿄증권거래소)
fdr.DataReader('7203', '2020-01-01', exchange='TSE') # Toyota Motor Corp 토요타 자동차(7203)
fdr.DataReader('9984', '2020-01-01', exchange='TSE') # SoftBank Group Corp 소프트뱅크그룹(9984)

# HOSE (호치민증권거래소)
fdr.DataReader('VCB', '2020-01-01', exchange='HOSE') # 베트남 무역은행(VCB)
fdr.DataReader('VIC', '2020-01-01', exchange='HOSE') # Vingroup (JSC)

# 글로벌 동일한 종목코드 경우 거래소를 지정
df = fdr.DataReader('000150', '2020-01-01') # KRX 두산
df = fdr.DataReader('000150', '2020-01-01', exchange='KRX') # KRX 두산 (위와 동일)
df = fdr.DataReader('000150', '2020-01-01', exchange='SZSE') # Yihua Healthcare 심천거래소

# 상품 선물 가격 데이터
df = fdr.DataReader('CL=F') # WTI유 선물 Crude Oil (NYMEX)
df = fdr.DataReader('BZ=F') # 브렌트유 선물 Brent Oil (NYMEX)
df = fdr.DataReader('NG=F') # 천연가스 선물 (NYMEX)
df = fdr.DataReader('GC=F') # 금 선물 (COMEX)
df = fdr.DataReader('SI=F') # 은 선물 (COMEX)
df = fdr.DataReader('HG=F') # 구리 선물 (COMEX)

# 환율: 여러 조합 가능(지원 심볼: ['KRW', 'EUR', 'CNY', 'JPY', 'CHF'])
df = fdr.DataReader('USD/KRW') # 달러 원화
df = fdr.DataReader('USD/EUR') # 달러 유로화
df = fdr.DataReader('USD/CNY') # 달러 위엔화
df = fdr.DataReader('CNY/KRW') # 위엔화 원화
df = fdr.DataReader('EUR/CNY') # 유로화 위엔화

# 암호화폐 가격 데이터 (원화, 달러)
# (지원 심볼: ['BTC', 'ETH', 'USDT', 'BNB', 'USDC', 'XRP', 'BUSD', 'ADA', 'SOL', 'DOGE'])
df = fdr.DataReader('BTC/KRW') # 비트코인/원화
df = fdr.DataReader('ETH/KRW') # 이더리움/원화
df = fdr.DataReader('BTC/USD') # 비트코인/달러
df = fdr.DataReader('ETH/USD') # 이더리움/달러

# KRX delisting stock data 상장폐지 종목 전체 가격 데이터
df = fdr.DataReader('036360', exchange='KRX-DELISTING')

# 미국 국채 채권 수익률
df = fdr.DataReader('US5YT')   # 5년 만기 미국국채 수익률
df = fdr.DataReader('US10YT') # 10년 만기 미국국채 수익률
df = fdr.DataReader('US30YT') # 30년 만기 미국국채 수익률

# 종목 리스팅 (종목수는 2022년 10월 25일 기준, 시장 규모 가늠 용도)
# KRX 상장회사(발행회사)목록 (가격 중심, 주식 종목) - 시가총액순
stocks = fdr.StockListing('KRX') # KRX: 2,663 종목(=코스피+코스닥+코넥스)
stocks = fdr.StockListing('KOSPI') # KOSPI: 940 종목
stocks = fdr.StockListing('KOSDAQ') # KOSDAQ: 1,597 종목
stocks = fdr.StockListing('KONEX') # KONEX: 126 종목

# KRX 전종목 목록 (설명 중심, 주식+펀드등 전종목)
stocks = fdr.StockListing('KRX-DESC') # 한국거래소: 7,632 종목
stocks = fdr.StockListing('KOSPI-DESC') # KOSPI: 5,897 종목
stocks = fdr.StockListing('KOSDAQ-DESC') # KOSDAQ: 1,609 종목
stocks = fdr.StockListing('KONEX-DESC') # KONEX: 126 종목

# US Market listings 미국 시장 거래소별 전종목 리스팅
stocks = fdr.StockListing('S&P500') # S&P500: 503 종목  
stocks = fdr.StockListing('NASDAQ') # 나스닥 (NASDAQ): 4,607 종목
stocks = fdr.StockListing('NYSE') # 뉴욕증권거래소 (NYSE): 3,364 종목

# Global Market listings 글로벌 시장 거래소별 전종목 리스팅
stocks = fdr.StockListing('SSE') # 상하이 증권거래소 (Shanghai Stock Exchange: SSE): 1,060 종목
stocks = fdr.StockListing('SZSE') # 선전 증권거래소(Shenzhen Stock Exchange: SZSE): 1,441 종목
stocks = fdr.StockListing('HKEX') # 홍콩 증권거래소(Hong Kong Exchange: HKEX): 2,656 종목
stocks = fdr.StockListing('TSE') # 도쿄 증권거래소(Tokyo Stock Exchange: TSE): 3,944 종목
stocks = fdr.StockListing('HOSE') # 호찌민 증권거래소(Ho Chi Minh City Stock Exchange: HOSE): 404 종목

# KRX 특수종목
stocks = fdr.StockListing('KRX-DELISTING') # 3,449 종목 - KRX 상장폐지 종목 전체
stocks = fdr.StockListing('KRX-ADMINISTRATIVE') # 81 종목 - KRX 관리종목

# KRX ETFs
etfs = fdr.StockListing('ETF/KR') # 626 종목 - 한국 ETF

# FRED 데이터
df = fdr.DataReader('FRED:M2') #  M2 통화량
df = fdr.DataReader('FRED:NASDAQCOM') # NASDAQCOM 나스닥종합지수

# FRED 데이터 여러 항목 한번에 
df = fdr.DataReader('FRED:M2,HSN1F,NASDAQCOM')  # M2 통화량, HSN1F 주택판매지수, NASDAQCOM 나스닥종합지수

# 캔들차트 그리기
df = fdr.DataReader('005930', '2021-01-01', '2021-02-15')

fdr.chart.plot(df)
fdr.chart.plot(df, title='삼성전자(005930)')

# 차트 설정
config = {'title':'fdr.chart.config()를 사용하여 설정을 한번에 지정할 수 있습니다', 
          'width': 600, 
          'height': 300,
          'volume': True,
}

fdr.chart.config(config=config)
fdr.chart.plot(df)
```

## Using FinanceDataReader
* [Users-Guide](https://github.com/FinanceData/FinanceDataReader/wiki/Users-Guide)
* [Quick-Reference (Symbol List)](https://github.com/FinanceData/FinanceDataReader/wiki/Quick-Reference)

## Tutorials
* [FRED 주요 경기 선행 지표](https://nbviewer.jupyter.org/github/FinanceData/FinanceDataReader/blob/master/tutorial/FinanceDataReader%20Tutorial%20-%20FRED%20%EA%B2%BD%EA%B8%B0%20%EC%84%A0%ED%96%89%20%EC%A7%80%ED%91%9C.ipynb)
* [수정주가(Adjusted Price)란?](https://nbviewer.jupyter.org/github/FinanceData/FinanceDataReader/blob/master/tutorial/FinanceDataReader%20Tutorial%20-%20%EC%88%98%EC%A0%95%EC%A3%BC%EA%B0%80.ipynb)
* [여러 종목 가격을 한번에](https://nbviewer.jupyter.org/github/FinanceData/FinanceDataReader/blob/master/tutorial/FinanceDataReader%20Tutorial%20-%20%EC%97%AC%EB%9F%AC%20%EC%A2%85%EB%AA%A9%EC%9D%98%20%EA%B0%80%EA%B2%A9%EC%9D%84%20%ED%95%9C%EB%B2%88%EC%97%90.ipynb)
* [VIX 지수와 관련 종목](https://nbviewer.jupyter.org/github/FinanceData/FinanceDataReader/blob/master/tutorial/FinanceDataReader%20Tutorial%20-%20VIX%20%EC%A7%80%EC%88%98%EC%99%80%20%EA%B4%80%EB%A0%A8%20%EC%A2%85%EB%AA%A9.ipynb)
* [섹터 평균 수익률과 개별 종목의 수익률 구하기](https://nbviewer.jupyter.org/github/FinanceData/FinanceDataReader/blob/master/tutorial/FinanceDataReader%20Tutorial%20-%20%EC%84%B9%ED%84%B0%20%ED%8F%89%EA%B7%A0%20%EC%88%98%EC%9D%B5%EB%A5%A0%EA%B3%BC%20%EA%B0%9C%EB%B3%84%20%EC%A2%85%EB%AA%A9%EC%9D%98%20%EC%88%98%EC%9D%B5%EB%A5%A0.ipynb)
* [차트 그리기와 활용하기](http://nbviewer.jupyter.org/c6c336c4727386810bec9264e81f6bba)


## FinanceDataReader Notebooks
* [S&P500 가격 데이터 수집과 수익률 분석](https://nbviewer.jupyter.org/710b8f0a4bd9a8df91ae1be6c7e838b1) 
* [S&P500 팩터 데이터 수집과 분석](https://nbviewer.jupyter.org/35a1b0d5248bc9b09513e53be437ac42) 


***2018-2022 [FinanceData.KR](http://financedata.kr)***
