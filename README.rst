BTC Annuity
===========

The *btc_annuity* program allows you to simulate and compares two possible 
approaches for implementing an annuity that starts with an initial investment in 
bitcoin, and then converts a small amount each year to dollars.  In both 
scenarios you start with 10 BTC from which you draw out $100k per year to live 
on.  The first is a tax free scenario where each year you simply take a loan 
against your bitcoin and never pay it back.  This approach does not consume the 
bitcoin but builds up debt. The second is where you sell enough bitcoin every 
year to cover your expenses.  This does not build up debt, but does consume the 
bitcoin.

In 2025 Coinbase offers Morpho, a program that allows you to borrow against 
bitcoin collateral.  It allows you to borrow up to $1M at rate as low as 5% with 
no fees with no repayment schedules or deadlines.  The following assumptions 
assume such a loan.

**Assumptions**::

    annual draw = $100k     -- initial amount borrowed per year
    inflation rate = 3%     -- the amount the draw increases each year

    interest rate = 7.5%    -- interest rate on borrowed dollars
    origination fee = 0%    -- relative loan fees
    fees = $0               -- absolute loan fees
    max LTV = 86%           -- maximum allowed loan to value of BTC

    collateral = 10 BTC     -- amount of bitcoin used as collateral
    BTC price = $120k       -- starting price of bitcoin
    BTC growth rate = 15%   -- expected annual growth rate of bitcoin price

    tax rate = 25%          -- tax rate

To adjust the assumptions, simply change the values in the source and re-run.

And here is the result of simulating the two scenarios.

**Scenario 1: Tax Free Living on $100k per year**::

    Year:   Draw    Owed     LTV     Net  |  $/BTC
       1:  $100k      $0   0.0 %   $1.2M  |  $120k
       2:  $103k   $100k   7.2 %  $1.28M  |  $138k
       3:  $106k   $203k  12.8 %  $1.38M  |  $159k
       4:  $109k   $309k  16.9 %  $1.52M  |  $183k
       5:  $113k   $418k  19.9 %  $1.68M  |  $210k
       6:  $116k   $531k  22.0 %  $1.88M  |  $241k
       7:  $119k   $647k  23.3 %  $2.13M  |  $278k
       8:  $123k   $766k  24.0 %  $2.43M  |  $319k
       9:  $127k   $889k  24.2 %  $2.78M  |  $367k
      10:  $130k  $1.02M  24.1 %  $3.21M  |  $422k
      11:  $134k  $1.15M  23.6 %  $3.71M  |  $485k
      12:  $138k  $1.28M  22.9 %   $4.3M  |  $558k
      13:  $143k  $1.42M  22.1 %     $5M  |  $642k
      14:  $147k  $1.56M  21.2 %  $5.82M  |  $738k
      15:  $151k  $1.71M  20.1 %  $6.78M  |  $849k
      16:  $156k  $1.86M  19.0 %   $7.9M  |  $976k
      17:  $160k  $2.02M  18.0 %  $9.21M  | $1.12M
      18:  $165k  $2.18M  16.9 %  $10.7M  | $1.29M
      19:  $170k  $2.34M  15.8 %  $12.5M  | $1.49M
      20:  $175k  $2.51M  14.7 %  $14.6M  | $1.71M

**Taxed Living on $100k per year**::

    Year:   Draw         Left        Net  |  $/BTC
       1:  $133k     8.89 BTC     $1.07M  |  $120k
       2:  $137k     7.89 BTC     $1.09M  |  $138k
       3:  $141k     7.00 BTC     $1.11M  |  $159k
       4:  $146k     6.20 BTC     $1.13M  |  $183k
       5:  $150k     5.49 BTC     $1.15M  |  $210k
       6:  $155k     4.85 BTC     $1.17M  |  $241k
       7:  $159k     4.28 BTC     $1.19M  |  $278k
       8:  $164k     3.76 BTC      $1.2M  |  $319k
       9:  $169k     3.30 BTC     $1.21M  |  $367k
      10:  $174k     2.89 BTC     $1.22M  |  $422k
      11:  $179k     2.52 BTC     $1.22M  |  $485k
      12:  $185k     2.19 BTC     $1.22M  |  $558k
      13:  $190k     1.89 BTC     $1.22M  |  $642k
      14:  $196k     1.63 BTC      $1.2M  |  $738k
      15:  $202k     1.39 BTC     $1.18M  |  $849k
      16:  $208k     1.18 BTC     $1.15M  |  $976k
      17:  $214k     0.99 BTC     $1.11M  | $1.12M
      18:  $220k     0.82 BTC     $1.05M  | $1.29M
      19:  $227k     0.66 BTC      $986k  | $1.49M
      20:  $234k     0.53 BTC      $900k  | $1.71M

As you can see this scenario slowly consumes the BTC.  Eventually the net value 
of your savings goes to zero, at which point the payout terminates.  Contrast 
this with the strategy of borrowing against your BTC where the net value of your 
savings continues to increase over time.

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
    Dollar value of your remaining BTC minus any amount owed in loans.
$/BTC:
    Price of one bitcoin.


Comments
--------
Coinbase uses the `Morpho platform <morpho.org>`_ for lending.  The interest 
rate varies over time.  At the moment the rate is 6.22%.
