
##<div align="center">Data Scheme for StarGate</div>

- This document **only defines** the farming performance gauge data of the StarGate bridge.
- This document does not specify optimized algorithms that collect and compute the data.


#### 1. Block-level data

- **B-Average** of feature X in a block is defined to be $1/n * \sum_{i=0}^{n-1} x_i$, where $\{x_i | i = 0, 1, ..., n-1\}$ are values that are held by X sequentially in the block and $x_k \neq x_{k+1}$ for all $k$. **Example**: If Balance has a constant value 30 in the block, then the B-Average of Balance is 30. If Balance has two values 30 and 40 in total sequentially in the block, then the B-Average of Balance is $1/2 * (30+40) = 35$
<br/>
- **AvgBlockTime~c~**: The average time duration spent to mine a block on the chain c. (Chain-level)
- **STGpB~c~**: The value of STG-per-Block on the chain c, at a given time.
- **STGpB^b^~c~**: The B-Average of STGpB~c~
- **ALLOC~c,p~**: The value of AllocPoint for the pool p on the chain c, at a given time.
- **ALLOC^b^~c,p~**: The B-Average of ALLOC~c,p~
- **T_ALLOC~c~**: The value of Total AllocPoint on the chain c, at a given time.
- **T_ALLOC^b^~c~**: The B-Average of T_ALLOC~c~
- **LPpUSD~c,p~**: The value of LP-per-USD for the pool p on the chain c, at a given time.
- **LPpUSD^b^~c,p~**: The B-Average of LPpUSD~c,p~
- **STGP**: The value of STG price quote in USD
- **STGP^b^**: The B-Average of STGP
- **STGpB~c,p~**: The value of STG-per-Block for the pool p on the chain c, at a given time. <br/>Note: STGpB~c,p~ = STGpB~c~ * ALLOC~c,p~ /T_ALLOC~c~ at a given time.
- **STGpB^b^~c,p~**: The B-Average of STGpB~c,p~
- **SLP~c,p~**: The value of Staked LP for the pool p on the chain c, at a given time.
- **SLP^b^~c,p~**: The B-Average of SLP~c,p~
- **STGpLP~c,p~**: The value of STG-per-LP for the pool p on the chain c, at a given time. <br/>Note: STGpLP~c,p~ = STGpB~c,p~ /SLP~c,p~ at a given time.
- **STGpLP^b^~c,p~**: The B-Average of STGpLP~c,p~
- **ROI~c,p~**: The value of Return-On-Investment for the pool p on the chain c, at a given time. <br/>Note: ROI~c,p~ = STGP * STGpLP~c~ * LPpUSD~c,p~  at a given time.
- **ROI^b^~c,p~**: The B-Average of ROI~c,p~
- **APY~c,p~**: The value of Annual Profit Yield for the pool p on the chain c, at a given time. <br/>Note: APY~c,p~ = (1 + ROI~c,p~) ** (year / AvgBlockTime~c~) - 1  at a given time.
- **APY^b^~c,p~**: The B-Average of APY~c,p~
<br/> <br/> <br/> <br/> <br/> <br/>


#### 2. Timeframe-level data
<br/>

- **Timeframe**: time interval $[T_a, T_b)$, where $T_a$ and $T_b$ are the Unix timestamp of an integer second. Note $T_b$ does *not* belong to the interval.
- **A block belongs to a timeframe** if and only if the timestamp of the block belongs to the timeframe.
- **BlockValue(X, B)** denotes the value of a feature X on the block B. **Examples** of BlockValue(X, B) are the B-Average, defined in the above section, and snapshot, which is the value of X at a opening/closing time of the block.
- Some concepts of around a feature X on a timeframe are defined as follow: <br/>**#-Sum** of X on a timeframe = $\sum_{i=0}^{n-1} BlockValue(X, B_i)$, <br/>**#-Product** of X on a timeframe = $\prod_{i=0}^{n-1} BlockValue(X, B_i)$, <br />**#-Average** of X a timeframe = $1/n * \sum_{i=0}^{n-1} BlockValue(X, B_i)$, <br/>where $\{B_i | i = 0, 1, ..., n-1\}$ are all blocks that belong to the timeframe.
<br/>
- **STGpB^a^~c~**: The #-Average of STGpB^b^~c~, on a timeframe, on the chain c.
- **ALLOC^a^~c,p~**: The #-Average of ALLOC^b^~c,p~, on a timeframe, on the chain c.
- **T_ALLOC^a^~c~**: The #-Average of T_ALLOC^b^~c~, on a timeframe, on the chain c.
- **STGpB^a^~c,p~**: The #-Average of STGpB^b^~c,p~, on a timeframe, for the pool p on the chain c.
- **SLP^a^~c,p~**: The #-Average of SLP^b^~c,p~, on a timeframe, for the pool p on the chain c.
- **LPpUSD^a^~c,p~**: The #-Average of LPpUSD^b^~c,p~, on a timeframe, for the pool p on the chain c.
- **STGpLP^a^~c,p~**: The #-Average of STGpB^b^~c,p~, on a timeframe, for the pool p on the chain c.
- **STGpLP^s^~c,p~**: The Sum of STGpB^b^~c,p~, on a timeframe, for the pool p on the chain c.
- **STGP^a^**: The #-Average of STGP^b^ on a timeframe.
<br/>
- **Average ROI~c,p~** := #-Average of ROI^b^~c,p~ the block-level Return-On-Investment, on a timeframe, for the pool p on the chain c.
- **Sum ROI~c,p~** :=  #-Sum of ROI^b^~c,p~ the block-level Return-On-Investment, on a timeframe, for the pool p on the chain c.
- **Compound ROI~c,p~** := #-Product of (ROI^b^~c,p~ +1) - 1. *This is meant to work as the **compound ROI** on the timeframe, compounded along the blocks.*
<br/>
- **Average APY~c,p~**:= #-Average of APY^b^~c,p~, on a timeframe, for the pool p on the chain c.
- **Sum APY~c,p~**:= #-Sum of APY^b^~c,p~, on a timeframe, for the pool p on the chain c.
- **Compound APY~c,p~** := (1+Compound ROI~c,p~)**(year/frametime) - 1, on a timeframe, for the pool p on the chain c.
<br/>

**Attention**: Compound ROI~c,p~, Compound APY~c~





