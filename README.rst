BTC Annuity
===========

Simulates two possible approaches for implementing an annuity that starts with 
an initial investment in bitcoin, and then converts a small amount each year to 
dollars.  In both scenarios you start with 10 BTC from which you draw out $100k 
per year to live on.  The first is a tax free scenario where each year you 
simply take a loan against your bitcoin on BlockFi.  This approach does not 
consume the bitcoin but builds up debt. The second is where you sell enough 
bitcoin every year to cover your expenses.  This does not build up debt, but 
does consume the bitcoin.

**Assumptions**::

    annual draw = $100k     -- amount borrowed per year

    interest rate = 4.5%    -- interest rate on borrowed dollars
    origination fee = 2%    -- relative loan fees
    fees = $650             -- absolute loan fees
    max LTV = 50%           -- maximum allowed loan to value of BTC

    collateral = 10 BTC     -- amount of bitcoin used as collateral
    BTC price = $60k        -- starting price of bitcoin
    BTC growth rate = 25%   -- expected annual growth rate of bitcoin price

    tax rate = 25%          -- tax rate

To adjust the assumptions, simply change the values in the source and re-run.

And here is the result of simulating the two scenarios.

**Scenario 1: Tax Free Living on $100k per year**::

    Year:   Draw    Owed     LTV     Net  |    BTC
       0:  $108k   $108k   17.9%   $492k  | $60.0k
       1:  $113k   $220k   29.4%   $530k  | $75.0k
       2:  $118k   $339k   36.1%   $599k  | $93.8k
       3:  $124k   $463k   39.5%   $709k  |  $117k
       4:  $130k   $593k   40.5%   $872k  |  $146k
       5:  $136k   $729k   39.8%  $1.10M  |  $183k
       6:  $143k   $871k   38.1%  $1.42M  |  $229k
       7:  $150k  $1.02M   35.7%  $1.84M  |  $286k
       8:  $157k  $1.18M   32.9%  $2.40M  |  $358k
       9:  $164k  $1.34M   30.0%  $3.13M  |  $447k
      10:  $172k  $1.51M   27.1%  $4.07M  |  $559k
      11:  $181k  $1.69M   24.3%  $5.29M  |  $698k
      12:  $189k  $1.88M   21.6%  $6.85M  |  $873k
      13:  $198k  $2.08M   19.1%  $8.83M  | $1.09M
      14:  $208k  $2.29M   16.8%  $11.4M  | $1.36M
      15:  $218k  $2.51M   14.7%  $14.5M  | $1.71M
      16:  $228k  $2.74M   12.8%  $18.6M  | $2.13M
      17:  $239k  $2.98M   11.2%  $23.7M  | $2.66M
      18:  $251k  $3.23M    9.7%  $30.1M  | $3.33M
      19:  $263k  $3.49M    8.4%  $38.1M  | $4.16M

**Taxed Living on $100k per year**::

    Year:   Draw         Left        Net  |    BTC
       0:  $133k     7.78 BTC      $467k  | $60.0k
       1:  $133k     6.00 BTC      $450k  | $75.0k
       2:  $133k     4.58 BTC      $429k  | $93.8k
       3:  $133k     3.44 BTC      $403k  |  $117k
       4:  $133k     2.53 BTC      $371k  |  $146k
       5:  $133k     1.80 BTC      $330k  |  $183k
       6:  $133k     1.22 BTC      $279k  |  $229k
       7:  $133k     0.75 BTC      $215k  |  $286k
       8:  $133k     0.38 BTC      $136k  |  $358k
       9:  $133k     0.08 BTC     $36.6k  |  $447k
      10:  $133k    -0.16 BTC    -$87.5k  |  $559k
      11:  $133k    -0.35 BTC     -$243k  |  $698k
      12:  $133k    -0.50 BTC     -$437k  |  $873k
      13:  $133k    -0.62 BTC     -$679k  | $1.09M
      14:  $133k    -0.72 BTC     -$982k  | $1.36M
      15:  $133k    -0.80 BTC    -$1.36M  | $1.71M
      16:  $133k    -0.86 BTC    -$1.84M  | $2.13M
      17:  $133k    -0.91 BTC    -$2.43M  | $2.66M
      18:  $133k    -0.95 BTC    -$3.17M  | $3.33M
      19:  $133k    -0.98 BTC    -$4.09M  | $4.16M

As you can see this scenario runs out of BTC at year 10 and fails.

Here are the meanings of the various columns.

Draw:
    Is the actual draw from reserves, amount over annual draw is additional
    amount needed to cover cost of loans and taxes.
Owed:
    The total accumulated amount borrowed assuming you never repay your 
    loans.
LTV:
    Loan to value of collateral.
Left:
    Number of bitcoin remaining from initial BTC investment.
Net:
    Value of your remaining collateral minus any amount owed in loans.
BTC:
    Price of bitcoin.
