
#Data Scheme for StarGate

- This document **defines** the StarGate performance data set.
- This document does not specify algorithms that create the data set.
- 

#### Terminology

- Block: Block on a blockchain.
- Timeframe: time interval $[T_a, T_b)$, where $T_a$ and $T_b$ are the Unix timestamp of an integer second. Note the interval is closed to the left and open to the right.


#### 1. Block-level data

- **Block Average** of feature X in a block is defined to be $1/n * \sum_{i=0}^{n-1} x_i$, <br />where $\{x_i | i = 0, 1, ..., n-1\}$ are values that are held by X sequentially in the block <br />and $x_k \neq x_{k+1}$ for all $k$.
<br/>
- **Example**: If Balance has a constant value 30 in the block, then the Block Average of Balance is 30. If Balance has two values 30 and 40 in total sequentially in the block, then the Block Average of Balance is $1/2 * (30+40) = 35$
<br/>
- **STGpB~c~**: The value of STG-per-Block on the chain c, at a given time.
- **STGpB^b^~c~**: The Block Average of STGpB~c~
<br/>
- **ALLOC~c,p~**: The value of AllocPoint for the pool p on the chain c, at a given time.
- **ALLOC^b^~c,p~**: The Block Average of ALLOC~c,p~
<br/>
- **T_ALLOC~c~**: The value of Total AllocPoint on the chain c, at a given time.
- **T_ALLOC^b^~c~**: The Block Average of T_ALLOC~c~
<br/>
- **STGpB~c,p~**: The value of STG-per-Block for the pool p on the chain c, at a given time. Note: STGpB~c,p~ = STGpB~c~ * ALLOC~c,p~ /T_ALLOC~c~ at a given time.
- **STGpB^b^~c,p~**: The Block Average of STGpB~c,p~
<br/>
- **SLP~c,p~**: The value of Staked LP for the pool p on the chain c, at a given time.
- **SLP^b^~c,p~**: The Block Average of SLP~c,p~
<br/>
- **LPpUSD~c,p~**: The value of LP-per-USD for the pool p on the chain c, at a given time.
- **LPpUSD^b^~c,p~**: The Block Average of LPpUSD~c,p~
<br/>
- **STGpLP~c,p~**: The value of STG-per-LP for the pool p on the chain c, at a given time. Note: STGpLP~c,p~ = STGpB~c,p~ /SLP~c,p~ at a given time.
- **STGpLP^b^~c,p~**: The Block Average of STGpLP~c,p~
<br/>
- **STGP**: The value of STG price quote in USD
- **STGP^b^**: The Block Average of STGP
  <br/>
- **ROI~c,p~**: The value of Return-On-Investment for the pool p on the chain c, at a given time. Note: ROI~c,p~ = STGP * STGpLP~c~ * LPpUSD~c,p~  at a given time.
- **ROI^b^~c,p~**: The Block Average of ROI~c,p~
<br/>
- **AvgBlockTime~c~**: The average time duration spent to mine a block on the chain c.
<br/>
- **APY~c,p~**: The value of Annual Profit Yield for the pool p on the chain c, at a given time. Note: APY~c,p~ = (1 + ROI~c,p~) ** (year / AvgBlockTime~c~) -1  at a given time.
- **ROI^b^~c,p~**: The Block Average of ROI~c,p~
<br/>





#### 2. Timeframe-level data










