
##<div align="center">Data Scheme for StarGate

- This document **only defines** the farming performance gauge data of the StarGate bridge.
- This document does not specify optimized algorithms that collect and compute the data.


#### 1. Block-level data

- **B-Average** of feature X in a block is defined to be $1/n * \sum_{i=0}^{n-1} x_i$, where $\{x_i | i = 0, 1, ..., n-1\}$ are values that are held by X sequentially in the block and $x_k \neq x_{k+1}$ for all $k$. **Example**: If Balance has a constant value 30 in the block, then the B-Average of Balance is 30. If Balance has two values 30 and 40 in total sequentially in the block, then the B-Average of Balance is $1/2 * (30+40) = 35$
<br/>
- **AvgBlockTime~c~**: The average time duration spent to mine a block on the chain c.
- **STGpB_c**: The value of STG-per-Block on the chain c, at a given time.
- **STGpB^b^~c~**: The B-Average of STGpB~c~
- **ALLOC~c,p~**: The value of AllocPoint for the pool p on the chain c, at a given time.
- **ALLOC^b^~c,p~**: The B-Average of ALLOC~c,p~
- **T_ALLOC~c~**: The value of Total AllocPoint on the chain c, at a given time.
- **T_ALLOC^b^~c~**: The B-Average of T_ALLOC~c~
- **LPpUSD~c,p~**: The value of LP-per-USD for the pool p on the chain c, at a given time.
- **LPpUSD^b^~c,p~**: The B-Average of LPpUSD~c,p~
- **STGP**: The value of STG price quote in USD
- **STGP^b^**: The B-Average of STGP
- **STGpB~c,p~**: The value of STG-per-Block for the pool p on the chain c, at a given time. Note: STGpB~c,p~ = STGpB~c~ * ALLOC~c,p~ /T_ALLOC~c~ at a given time.
- **STGpB^b^~c,p~**: The B-Average of STGpB~c,p~
- **SLP~c,p~**: The value of Staked LP for the pool p on the chain c, at a given time.
- **SLP^b^~c,p~**: The B-Average of SLP~c,p~
- **STGpLP~c,p~**: The value of STG-per-LP for the pool p on the chain c, at a given time. Note: STGpLP~c,p~ = STGpB~c,p~ /SLP~c,p~ at a given time.
- **STGpLP^b^~c,p~**: The B-Average of STGpLP~c,p~
- **ROI~c,p~**: The value of Return-On-Investment for the pool p on the chain c, at a given time. Note: ROI~c,p~ = STGP * STGpLP~c~ * LPpUSD~c,p~  at a given time.
- **ROI^b^~c,p~**: The B-Average of ROI~c,p~
- **APY~c,p~**: The value of Annual Profit Yield for the pool p on the chain c, at a given time. Note: APY~c,p~ = (1 + ROI~c,p~) ** (year / AvgBlockTime~c~) -1  at a given time.
- **APY^b^~c,p~**: The B-Average of APY~c,p~
<br/> <br/> <br/> <br/> <br/> <br/>


#### 2. Timeframe-level data
<br/>

- **Timeframe**: time interval $[T_a, T_b)$, where $T_a$ and $T_b$ are the Unix timestamp of an integer second. Note the interval is closed to the left, meaning $T_a$ belongs to the interval, and open to the right, meaning $T_b$ does not belong to the interval.
- **A block belongs to a timeframe** if and only if the timestamp of the block belongs to the timeframe.
  <br/>
- **BlockValue(X, B)** denotes the value of the feature X at the block B. Example: BlockValue(X, B) = X^b^ the B-Average of X.
<br/>
- **#-Average** of a feature X in a timeframe is defined to be $1/n * \sum_{i=0}^{n-1} BlockValue(X, B_i)$, <br />where $\{B_i | i = 0, 1, ..., n-1\}$ are all blocks that belong to the timeframe.
<br/>
- **Sum** of a feature X in a timeframe is defined to be $\sum_{i=0}^{n-1} BlockValue(X, B_i)$, <br />where $\{B_i | i = 0, 1, ..., n-1\}$ are all blocks that belong to the timeframe.
<br/>
- **STGpB^#^~c~**: The #-Average of STG-per-Block, on a given timeframe, on the chain c.
<br/>
- **ALLOC^#^~c,p~**: The #-Average of AllocPoint, on a given timeframe, on the chain c.
<br/>
- **T_ALLOC^#^~c~**: The #-Average of Total AllocPoint, on a given timeframe, on the chain c.
<br/>
- **STGpB^#^~c,p~**: The #-Average of STG-per-Block, on a given timeframe, for the pool p on the chain c.
<br/>
- **SLP^#^~c,p~**: The #-Average of Staked LP, on a given timeframe, for the pool p on the chain c.
<br/>
- **LPpUSD^#^~c,p~**: The #-Average of LP-per-USD, on a given timeframe, for the pool p on the chain c.
<br/>
- **STGpLP^#^~c,p~**: The #-Average of STG-per-LP, on a given timeframe, for the pool p on the chain c.
- **STGpLP^s^~c,p~**: The Sum of STG-per-LP, on a given timeframe, for the pool p on the chain c.
  <br/>
- **STGP^#^**: The #-Average of STG price quote in USD on the timeframe f.
<br/>
- **ROI^#^~c,p~**: The #-Average of Return-On-Investment, on a given timeframe, for the pool p on the chain c.
- **ROI^s^~c,p~**: The Sum of Return-On-Investment, on a given timeframe, for the pool p on the chain c.
<br/>
- **APY^#^~c,p~**: The #-Average of Annual Profit Yield, on a given timeframe, for the pool p on the chain c.
- **APY^s^~c,p~**: The Sum of Annual Profit Yield, on a given timeframe, for the pool p on the chain c.
<br/>





